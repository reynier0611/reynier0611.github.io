## Using Jupyter Notebooks  on Cori
[Back to table of Contents](../README.md)

ML repo is [here](https://github.com/jdmulligan/ml-hadronization).

Logon to perlmutter:

```
ssh reynier@perlmutter-p1.nersc.gov
```

Start a screen session:

```
screen -S ML
```

Request an interactive node from the slurm batch system:

```
salloc --nodes 1 --qos interactive --time 04:00:00 --constraint gpu --gpus 4 --account=alice_g
```

Run code:
```
python steer_analysis.py --read /pscratch/sd/r/reynier/results.h5 --analyze
```

### Data generation on hiccup

```
ssh -Y rey@hic.lbl.gov
srun -N 1 -n 20 -t 2:00:00 -p quick --pty bash # request quick node
srun -N 1 -n 20 -t 24:00:00 -p std --pty bash # request standard node
srun -N 1 -n 20 -t 72:00:00 -p long --pty bash # request long node
cd ml_hadronization/ml-hadronization/
source init.sh
cd ml_hadronization/ml-hadronization/ # previous line kicks me back to home directory
python steer_analysis.py --generate --write
scp TestOutput/results.h5 reynier@perlmutter-p1.nersc.gov:/pscratch/sd/r/reynier/
```

### Some notes on the results:

Training a NN with z in all three channels (r,g,b) takes:

- 45 min (when generating 10k events)
- 73 min (when generating 40k events)