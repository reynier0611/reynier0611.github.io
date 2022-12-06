## ML shortcuts on Perlmutter
[Back to table of Contents](../README.md)

ML repo is [here](https://github.com/jdmulligan/ml-hadronization).

### Important directories on Perlmutter

- training input data: ```/pscratch/sd/r/reynier/training_data/```

- training output data ```/pscratch/sd/r/reynier/training_output/```

### Data generation on hiccup

```bash
ssh -Y rey@hic.lbl.gov
srun -N 1 -n 20 -t 2:00:00 -p quick --pty bash
cd ml_hadronization/ml-hadronization/
source init.sh
cd ml_hadronization/ml-hadronization/ # previous line kicks me back to home directory
python steer_analysis.py --generate --write --outputDir /rstorage/alice/AnalysisResults/rey/ml/data
scp /rstorage/alice/AnalysisResults/rey/ml/data/results.h5 reynier@perlmutter-p1.nersc.gov:/pscratch/sd/r/reynier/
```

if need more time than two hours:

```bash
srun -N 1 -n 20 -t 24:00:00 -p std --pty bash # request standard node
srun -N 1 -n 20 -t 72:00:00 -p long --pty bash # request long node
```

### Training on perlmutter

```bash
ssh reynier@perlmutter-p1.nersc.gov
screen -S ML
salloc --nodes 1 --qos interactive --time 04:00:00 --constraint gpu --gpus 4 --account=alice_g
cd ml-hadronization/;source init_perlmutter.sh
python steer_analysis.py --read /pscratch/sd/r/reynier/data_jets_1M_events.h5 --analyze --outputDir /pscratch/sd/r/reynier/training_output/ --configFile config.yaml
```

then press Ctrl+A Ctrl+D to exit the screen session.

###### Script for interactive job:
can be found [here](https://github.com/jdmulligan/ml-hadronization/blob/main/sample_interactive_job.sh). Execute by doing:

```bash
sample_interactive_job.sh some_output_folder_name config_filename
```

###### Script for slurm job:
can be found [here](https://github.com/jdmulligan/ml-hadronization/blob/main/slurm/slurm.sh). Open script, change name for output directory and point to right config file, and then do:

```bash
sbatch slurm.sh
```

### Testing trained model:

Generate new events:

```bash
python steer_analysis.py --generate --inspect
```

or read already generated events:

```bash
python steer_analysis.py --read /pscratch/sd/r/reynier/training_data/data_1k_events.h5 --inspect --configFile config.yaml
```

### Some notes on the results:

Training a NN with z in all three channels (r,g,b) takes:

- 45 min (when generating 10k events) n_epochs: 30
- 73 min (when generating 40k events) n_epochs: 30
- 142 min (2.3h) (when generating 10k events) n_epochs: 100

### Current settings in config:
```yaml
n_events: see above
n_particles_max_per_event: 200
n_jets_per_event: 5
n_particles_max_per_jet: 50

jetR: [0.4]

#------------------------------------------------------------------
# These parameters are used only in ML analysis
#------------------------------------------------------------------

# Size of labeled data to load
n_train: 1500
n_val: 300
n_test: 300

# Select model: pix2pix_Brownlee_jetimage, pix2pix_Brownlee_4xNimage
models: [pix2pix_Brownlee_jetimage]

pix2pix_Brownlee_jetimage:
  image_granularity: 256
  n_epochs: see above
  n_batch: 1
  learning_rate: 0.0002
  beta_1: 0.5
  observables_per_pixel: ['constit_z','constit_z','constit_z']
```

### Copying files back to hiccup:

```bash
scp reynier@perlmutter-p1.nersc.gov:~/ml-hadronization/*.h5 .
scp reynier@perlmutter-p1.nersc.gov:~/ml-hadronization/*.txt .
```
