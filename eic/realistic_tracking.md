## Realistic tracking

<a><button name="button" style = "color:red;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a>

### Chat with Joe Osborn (23/01/13):

- Joe is working on an orthogonal seeder based on EICrecon (similar to what Yue Shi is doing, but Yue Shi uses Juggler). Joe modified the code so that parameters can be input from the command line without need to recompile the code.

- The first step is to generate events up to but not including the reconstruction step. Info about EICrecon can be found [here](https://eic.github.io/EICrecon/#/). And details on how to run DD4HEP simulations can be found [here](https://eic.github.io/EICrecon/#/howto/run_dd4hep_simulation). He, for instance, ran negative pions and stored them in a root file called: ```negpions.edm4hep.root```, which will be the input for the next step.

- seeder parameters that need to be tuned can be found [here](https://github.com/eic/EICrecon/blob/main/src/algorithms/tracking/OrthogonalTrackSeedingConfig.h). A bit more info on what these parameters are can be found [here](https://github.com/acts-project/acts/blob/3b4b5c741c8541491d496a36b917b00b344d52d1/Core/include/Acts/Seeding/SeedFinderOrthogonalConfig.hpp).

- The command Joe used to reconstruct seeds is:

```shell
eicrecon -Pjana:plugin_path=/gpfs01/eic/data/osbornjd/EPIC/git/EICrecon/lib/EICrecon/plugins -Pjana:debug_plugin_loading=1 -Ptracking:CentralTrackSeedingResults:impactMax=5 negpions.edm4hep.root
```

- Joe says that maybe the part:

```shell
-Pjana:plugin_path=/gpfs01/eic/data/osbornjd/EPIC/git/EICrecon/lib/EICrecon/plugins -Pjana:debug_plugin_loading=1
```

won't be needed at the time I start using the code. The output of this command is a root file called ```podio_output.root```. There, we need to find a branch called ```CentralTrackSeedingResults```.

### Files that I have generated:

- ```sim_pions_p_0_10_GeV_eta_-4_4_10000.edm4hep.root```

- ```sim_pions_p_1_3_GeV_eta_-4_4_10000.edm4hep.root```

Located in: ```/global/project/projectdirs/m3763/reynier/DD4HEP/reconstruction_benchmarks/``` on Cori.

### Generating new events:

```bash
cd /global/project/projectdirs/m3763/reynier/DD4HEP/reconstruction_benchmarks
````

Edit the following file: 
```bash
vim benchmarks/tracking/scripts/gen_central_pions.cxx
```

for example, the generation part:

```c++
Double_t p     = r1->Uniform(1.,3.0);
Double_t phi   = r1->Uniform(0.0, 2.0 * M_PI);
//Double_t costh = r1->Uniform(cos_theta_min, cos_theta_max);
//Double_t th    = std::acos(costh);
Double_t eta   = r1->Uniform(-4.0,4.0);
Double_t th    = 2.*std::atan(std::exp(-eta));
Double_t px    = p * std::cos(phi) * std::sin(th);
Double_t py    = p * std::sin(phi) * std::sin(th);
Double_t pz    = p * std::cos(th);
```

Then, modify this one:

```bash
vim benchmarks/tracking/central_pions.sh
```

Mainly, add the number of events (although it does not have to be hardcoded and can be passed as an argument)


```shell
if [[ ! -n  "${JUGGLER_N_EVENTS}" ]] ; then
  export JUGGLER_N_EVENTS=10000
fi
```

```bash
bash benchmarks/tracking/central_pions.sh
```

### Shell script to explore params:

See ```sourceme_param_exploration.sh``` in: ```/global/project/projectdirs/m3763/reynier/DD4HEP/reconstruction_benchmarks/``` on Cori.

```bash
parname="cotThetaMax"
infname=sim_pions_p_0_10_GeV_eta_-4_4_10000.edm4hep.root

for par in {0.52,1.18,3.63,10.02,16.54,27.29}
do
        outfname=podio_output_$parname"_"$par".root"

        eicrecon \
        -Ppodio:output_file=$outfname \
        -Ptracking:CentralTrackSeedingResults:bFieldInZ=1.7*Acts::UnitConstants::T \
        -Ptracking:CentralTrackSeedingResults:rMax=440.*Acts::UnitConstants::mm \
        -Ptracking:CentralTrackSeedingResults:rMin=33.*Acts::UnitConstants::mm \
        -Ptracking:CentralTrackSeedingResults:zMin=-1500.*Acts::UnitConstants::mm \
        -Ptracking:CentralTrackSeedingResults:zMax=1700.*Acts::UnitConstants::mm \
        -Ptracking:CentralTrackSeedingResults:beamPosX=0 \
        -Ptracking:CentralTrackSeedingResults:beamPosY=0 \
        -Ptracking:CentralTrackSeedingResults:deltaRMinTopSP=50.*Acts::UnitConstants::mm \
        -Ptracking:CentralTrackSeedingResults:deltaRMinBottomSP=50.*Acts::UnitConstants::mm \
        -Ptracking:CentralTrackSeedingResults:deltaRMaxTopSP=220.*Acts::UnitConstants::mm \
        -Ptracking:CentralTrackSeedingResults:deltaRMaxBottomSP=220.*Acts::UnitConstants::mm \
        -Ptracking:CentralTrackSeedingResults:collisionRegionMin=-250*Acts::UnitConstants::mm \
        -Ptracking:CentralTrackSeedingResults:collisionRegionMax=250*Acts::UnitConstants::mm \
        -Ptracking:CentralTrackSeedingResults:cotThetaMax=$par \
        -Ptracking:CentralTrackSeedingResults:minPt=6*Acts::UnitConstants::MeV \
        -Ptracking:CentralTrackSeedingResults:maxSeedsPerSpM=0 \
        -Ptracking:CentralTrackSeedingResults:sigmaScattering=5 \
        -Ptracking:CentralTrackSeedingResults:radLengthPerSeed=0.1 \
        -Ptracking:CentralTrackSeedingResults:impactMax=3*Acts::UnitConstants::mm \
        -Ptracking:CentralTrackSeedingResults:bFieldMin=0.1*Acts::UnitConstants::T \
        $infname
done
```