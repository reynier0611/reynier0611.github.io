## Useful analysis notes
[Back to table of Contents](../README.md)

### Merging, Scaling, and Merging pThard - MC

#### Scaling by sigma/N

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
