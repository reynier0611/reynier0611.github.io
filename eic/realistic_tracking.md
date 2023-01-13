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