## Useful pyjetty notes
[Back to table of Contents](../README.md)

### Merging, Scaling, and Merging pThard - MC

The MC files are produced in separate $p_{\rm T, \, hard}$ bins. This is done to focus the generation in different bins and accrue similar amount of statistics even in the bins where the cross section is small. Consequently, these files need to be scaled by the cross section before combining them.

#### 1. Merging all files from the same $p_{\rm T, \, hard}$ bin

hadd all root files corresponding to the same $p_{\rm T, \, hard}$ bin. See, for example: ```slurm_merge_LHC18b8.sh``` and ```merge_LHC18b8.sh``` in ```pyjetty/pyjetty/alice_analysis/slurm/utils/rey/```. Edit both files and replace ```rey``` with the appropriate username. Also, modify the number in ```JOB_ID=209384``` in merge_LHC18b8.sh to reflect the right job number. Then execute:

```
sbatch slurm_merge_LHC18b8.sh
```

This is for ```LHC18b8``` (the pp MC dataset). For ```LHC20g4``` (the PbPb MC dataset) do:

```
sbatch slurm_merge_LHC20g4.sh
```

#### 2. Scaling by sigma/N

cd into the directory containing the 1/, 2/, ... sub-directories and scale the combined files corresponding to a given pThard bin by the appropriate scale factor. To do so, run scaleHistograms.py (with the correct file path) and config file associated with the simulation:

```
python /home/rey/pyjetty/pyjetty/alice_analysis/slurm/utils/rey/scaleHistograms.py -c /rstorage/alice/data/LHC18b8/scaleFactors.yaml
```

The path given above is for the PYTHIA8 + GEANT3 simulations. The paths for the fast PYTHIA8 and fast Herwig7 simulations are:

```
/rstorage/generators/pythia_alice/tree_fastsim/scaleFactors.yaml
/rstorage/generators/herwig_alice/tree_fastsim/scaleFactors.yaml
```

respectively. For the Pb-Pb full simulations, the scale factors are here:

```
/rstorage/alice/data/LHC20g4/scaleFactors.yaml
```
