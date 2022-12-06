## DD4HEP
[Back to table of Contents](../README.md)

---

See more details [here](https://github.com/bschmookler/athena_ana) and [here](https://demo.hedgedoc.org/s/Dm9DG1oi7).

### Getting DD4HEP working on Cori

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
git clone https://eicweb.phy.anl.gov/EIC/benchmarks/reconstruction_benchmarks.git # ONLY THE FIRST TIME
```

#### Subsequent times:

```bash
shifterimg pull eicweb/jug_xl:nightly # From time to time, to update the image
shifter --image=eicweb/jug_xl:nightly /bin/bash
eic-shell
source /opt/detector/setup.sh
cd /global/project/projectdirs/m3763/reynier/DD4HEP
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

### Modify and compile juggler

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

### Running a batch job

```bash
cd /global/project/projectdirs/m3763/reynier/DD4HEP/reconstruction_benchmarks/slurm_scripts
sbatch 1_slurm_test.sh
```

This script collects all the necessary slurm information and runs ```2_run_test_pions.sh```. This runs ```benchmarks/tracking/central_pions.sh```. This script collects a series of arguments (e.g. number of events) and then:

* generates events: ```root -b -q "benchmarks/tracking/scripts/gen_central_pions.cxx+(...")"```
* runs the Geant4 simulation: ```ddsim --runType batch ...```
* reconstructs events: ```benchmarks/tracking/scripts/rec_central_pions.cxx+```


### Tests

```bash
time bash benchmarks/tracking/RCT_pions.sh
```

100 pions takes approximately 1 min 40 sec

### Passing background hepmc file to DD4HEP GEANT simulation

```bash
npsim --runType batch --numberOfEvents 100000 --compactFile ${DETECTOR_PATH}/epic.xml --inputFiles ./out_int_window_100.0ns_nevents_100000.hepmc --outputFile out_0um_new.edm4hep.root --random.seed 42
```

### Changing beampipe thickness

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

### DD4HEP tutorials

All links can be found [here](https://indico.bnl.gov/category/443/)

- [1. Setting up the EIC software environment](https://www.youtube.com/watch?v=Y0Mg24XLomY)

- [2. Geometry development using DD4hep: how to modify or add detector description](https://www.youtube.com/watch?v=RJAHnEW9cYk)
