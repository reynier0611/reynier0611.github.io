<style TYPE="text/css">
code.has-jax {font: inherit; font-size: 100%; background: inherit; border: inherit;}
</style>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
    tex2jax: {
        inlineMath: [['$','$'], ['\\(','\\)']],
        skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'] // removed 'code' entry
    }
});
MathJax.Hub.Queue(function() {
    var all = MathJax.Hub.getAllJax(), i;
    for(i = 0; i < all.length; i += 1) {
        all[i].SourceElement().parentNode.className += ' has-jax';
    }
});
</script>
<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.4/MathJax.js?config=TeX-AMS_HTML-full"></script>

## Useful pyjetty notes
[Back to table of Contents](../README.md)

### Merging, Scaling, and Merging pThard - MC

The MC files are produced in separate $p_{\rm T, \, hard}$ bins. This is done to focus the generation in different bins and accrue similar amount of statistics even in the bins where the cross section is small. Consequently, these files need to be scaled by the cross section before combining them.

#### 1. Merging all files from the same $p_{\rm T, \, hard}$ bin

hadd all root files corresponding to the same $p_{\rm T, \, hard}$ bin. See, for example: ```slurm_merge_LHC18b8.sh``` and ```merge_LHC18b8.sh``` in ```pyjetty/pyjetty/alice_analysis/slurm/utils/rey/```. Edit both files and replace ```rey``` with the appropriate username. Also, modify the number in ```JOB_ID=209384``` in ```merge_LHC18b8.sh``` to reflect the right job number. Then execute:

```
sbatch slurm_merge_LHC18b8.sh
```

This is for ```LHC18b8``` (the pp MC dataset). For ```LHC20g4``` (the PbPb MC dataset) do: ```sbatch slurm_merge_LHC20g4.sh```. For merging pp fast simulation with Herwig7 use: ```sbatch slurm_merge_LHC18b8_fastsim_herwig.sh```. For merging pp or PbPb fast simulation with PYTHIA8 use: ```sbatch slurm_merge_LHC18b8_fastsim_pythia.sh```. For merging PbPb fast simulation with JEWEL use: ```sbatch slurm_merge_fastsim_PbPb_jewel.sh```.

#### 2. Scaling by $\sigma/N$

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

#### 3. Final merge of all $p_{\rm T, \, hard}$ splits into one file:

After the histograms have been scaled, you should merge the $p_{\rm T, \, hard}$ bins. See for example ```merge_pthat.sh```. The number in the line ```JOB_ID=209384``` and paths should be updated. Then do:

```
source merge_pthat.sh
```
