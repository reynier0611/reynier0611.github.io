## DD4HEP

<a><button name="button" style = "color:red;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a>

---

See more details [here](https://github.com/bschmookler/athena_ana) and [here](https://demo.hedgedoc.org/s/Dm9DG1oi7).

## Getting DD4HEP working on Cori

#### First time:

ssh into Cori, go to a convenient directory, and run:
```bash
shifterimg pull eicweb/jug_xl:nightly
shifter --image=eicweb/jug_xl:nightly /bin/bash
eic-shell
source /opt/detector/setup.sh
cd /global/project/projectdirs/m3763/reynier/
mkdir DD4HEP # ONLY THE FIRST TIME
cd DD4HEP
git clone https://eicweb.phy.anl.gov/EIC/benchmarks/reconstruction_benchmarks.git
```

#### Subsequent times:

```bash
shifter --image=eicweb/jug_xl:nightly /bin/bash
eic-shell
source /opt/detector/setup.sh
cd /global/project/projectdirs/m3763/reynier/DD4HEP
```

- From time to time update the image by doing:

```bash
shifterimg pull eicweb/jug_xl:nightly
```

#### Testing:

Try the following commands, which run 100 pions:
```bash
cd reconstruction_benchmarks/
bash benchmarks/tracking/central_pions.sh
```

This produces several root files, e.g.:
- central_pions.hepmc -> generated events
- sim_central_pions.edm4hep.root -> Geant4 hit-level information
- rec_central_pions.root -> reconstructed (+generated) information

In the events tree we can find some of the useful variables:

Generated:
```bash
MCParticles.momentum.x = 0.000000, 0.000000, -2.105457
MCParticles.momentum.y = 0.000000, 0.000000, 1.102192
MCParticles.momentum.z = 10.000000, 0.000000, -0.241078
```

The first two entries are the electron and proton kinematics. Here are the reconstructed ones:
```bash
ReconstructedParticles.p.x = -2.093476
ReconstructedParticles.p.y = 1.124782
ReconstructedParticles.p.z = -0.241075
```

## Running a batch job

```bash
cd /global/project/projectdirs/m3763/reynier/DD4HEP/reconstruction_benchmarks/slurm_scripts
sbatch 1_slurm_test.sh
```

This script collects all the necessary slurm information and runs ```2_run_test_pions.sh```. This runs ```benchmarks/tracking/central_pions.sh```. This script collects a series of arguments (e.g. number of events) and then:

* generates events: ```root -b -q "benchmarks/tracking/scripts/gen_central_pions.cxx+(...")"```
* runs the Geant4 simulation: ```ddsim --runType batch ...```
* reconstructs events: ```benchmarks/tracking/scripts/rec_central_pions.cxx+```


## Passing background hepmc file to DD4HEP GEANT simulation

```bash
npsim --runType batch --numberOfEvents -1 --compactFile ${DETECTOR_PATH}/epic.xml --inputFiles ./out_int_window_100.0ns_nevents_100000.hepmc --outputFile out_0um_new.edm4hep.root --random.seed 42
```

## Compiling EICrecon

- If you want to contribute (push) code:

```bash
git clone git@github.com:eic/EICrecon
```

- you may need to be added to some list. Alternatively, do:

```bash
git clone https://github.com/eic/EICrecon
```

- Afterwards:

```bash
cd EICrecon
cmake -S . -B build
cmake --build build --target install -- -j8
source ./bin/eicrecon-this.sh
```

- Check that DD4HEP is using this repo rather than the default one:

```bash
which eicrecon
```

### Using Barak's plug-in

##### Step 1:

- Check which branch we are currently in:

```bash
git branch -a
```

We may see by default that we are using the main branch, but we want to use ```track-qa-barak```. To use that branch instead do:

```bash
git checkout track-qa-barak
```

then recompile EICrecon:

```bash
cmake -S . -B build; cmake --build build --target install -- -j8
```

##### Step 2: 

Use this command to run the simulation and reconstruction: 

[EICrecon/blob/track-qa-barak/src/tests/track_qa/run_sim.sh](https://github.com/eic/EICrecon/blob/track-qa-barak/src/tests/track_qa/run_sim.sh)

You'll need to adjust the steering file to generate the particle eta, momentum range you want.

##### Step 3: 

To switch between truth seeded and real seeded tracks, toggle this line in [EICrecon/blob/track-qa-barak/src/tests/track_qa/trackqa_processor.cc](https://github.com/eic/EICrecon/blob/track-qa-barak/src/tests/track_qa/trackqa_processor.cc)

Truth seeding for track reconstruction:

```c++
auto trajectories = event->Get<eicrecon::TrackingResultTrajectory>("CentralCKFTrajectories");
```

Realistic seeding for track reconstruction:
```c++
auto trajectories = event->Get<eicrecon::TrackingResultTrajectory>("CentralCKFSeededTrajectories");
```

## Changing beampipe thickness

#### First time

```bash
cd /project/projectdirs/alice/reynier/eic/
mkdir repos
cd /project/projectdirs/alice/reynier/eic/repos/
```

- From the same directory, make an install directory and link properly:

```bash
mkdir install
export EIC_SHELL_PREFIX=/project/projectdirs/alice/reynier/eic/repos/install
export LD_LIBRARY_PATH=$EIC_SHELL_PREFIX/lib:$LD_LIBRARY_PATH
source $EIC_SHELL_PREFIX/setup.sh
```

- From the same directory clone the epic repo and edit beampipe gold coating thickness:

```bash
git clone https://github.com/eic/epic
cd epic
vim compact/central_beampipe.xml
```

- For example, set:

```bash
gold_thickness="1e-10*um"
```

- Then compile this change:

```bash
mkdir build; cd build
cmake .. -DCMAKE_INSTALL_PREFIX=$EIC_SHELL_PREFIX; make; make install; source setup.sh
```

- Test these changes with a material scan:

```bash
cd /global/project/projectdirs/m3763/reynier/DD4HEP/
materialScan ${DETECTOR_PATH}/epic.xml 0 0 0 0 50 0
```

#### Subsequent times

```bash
export EIC_SHELL_PREFIX=/project/projectdirs/alice/reynier/eic/repos/install
export LD_LIBRARY_PATH=$EIC_SHELL_PREFIX/lib:$LD_LIBRARY_PATH
source $EIC_SHELL_PREFIX/setup.sh
cd /project/projectdirs/alice/reynier/eic/repos/epic/build/
```

- If you change the beampipe thickness, do:

```bash
cmake .. -DCMAKE_INSTALL_PREFIX=$EIC_SHELL_PREFIX; make; make install; source setup.sh
```

- otherwise just do:

```bash
source setup.sh
```

- Finally check that it worked:

```bash
cd /global/project/projectdirs/m3763/reynier/DD4HEP/
materialScan ${DETECTOR_PATH}/epic.xml 0 0 0 0 50 0
```

#### Old method (deprecated)

```bash
cd /project/projectdirs/alice/reynier/eic
mkdir repos; cd repos
git clone https://github.com/eic/ip6.git
cd /project/projectdirs/alice/reynier/eic/repos/ip6
vim ip6/central_beampipe.xml
```
change the gold coating. For example, set:
```bash
gold_thickness="1e-10*um"
```
Then compile this change:
```bash
cmake -B build -S . -DCMAKE_INSTALL_PREFIX=install -DEPIC_ECCE_LEGACY_COMPAT=OFF;cmake --build build;cmake --install build
```
These commands are explained [here](https://github.com/eic/epic). Then source:
```bash
source install/setup.sh
```
And finally run a material scan to see if the change shows up:
```bash
materialScan ${DETECTOR_PATH}/epic.xml 0 0 0 0 50 0
```

## Synchrotron radiation files

input hepmc files stored on Cori in ```/global/project/projectdirs/m3763/reynier/DD4HEP/input_hepmc``` under the filename: ```out_int_window_100.0ns_nevents_100000_pid_22_Escale_x1.0_status_4_1_seed_1.hepmc``` where the last number before the ```.hepmc``` extension. These files are about 9 Gb each. The output Geant hit files are stored in ```/global/project/projectdirs/m3763/reynier/DD4HEP/generated_SR_background```.

## Admixing signal and backgrounds:

Copied hepmc file from central data storage:

```bash
mc cp -r --insecure S3/eictest/EPIC/EVGEN/DIS/NC/10x275/minQ2=1/pythia8NCDIS_10x275_minQ2=1_beamEffects_xAngle=-0.025_hiDiv_1.hepmc .
```

Passed these events through Geant to generate hits:

```bash
npsim --runType batch --numberOfEvents 10000 --compactFile ${DETECTOR_PATH}/epic.xml --inputFiles ./dis_events/pythia8NCDIS_10x275_minQ2\=1_beamEffects_xAngle\=-0.025_hiDiv_1.hepmc --outputFile dis_events/dis_for_background_test_10000.edm4hep.root
```

```bash
eicrecon dis_for_background_test.edm4hep.root -Ppodio:background_filename=generated_SR_background/geant_out_int_window_100.0ns_nevents_100000_pid_22_Escale_x1.0_status_4_1_seed_1.edm4hep.root -Ppodio:num_background_events=1
```


## Modify and compile juggler

Yue Shi sent us two codes for the updated realistic seeding: ```TrackParamACTSSeeding.cpp``` and ```track_reconstruction.py```. We need to do

1. Get a copy of Juggler:
```cd /project/projectdirs/alice/reynier/eic```
2. Update ```TrackParamACTSSeeding.cpp``` with the file from Yue Shi:
```cp ~/TrackParamACTSSeeding.cpp juggler/JugTrack/src/components/```
3. Compile this new juggler version:
```bash
mkdir local
ATHENA_PREFIX=/project/projectdirs/alice/reynier/eic/
mkdir build; cd build
cmake ../juggler/ -DCMAKE_INSTALL_PREFIX=$ATHENA_PREFIX
make
make install
export JUGGLER_INSTALL_PREFIX=$ATHENA_PREFIX
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:${ATHENA_PREFIX}/lib
```
4. Also copy ```track_reconstruction.py``` from Yue Shi:
```
mv ../track_reconstruction.py reconstruction_benchmarks/benchmarks/tracking/options/track_reconstruction.py
```

## DD4HEP tutorials

All links can be found [here](https://indico.bnl.gov/category/443/)

- [1. Setting up the EIC software environment](https://www.youtube.com/watch?v=Y0Mg24XLomY)

- [2. Geometry development using DD4hep: how to modify or add detector description](https://www.youtube.com/watch?v=RJAHnEW9cYk)