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

### Fastsim

The slurm script we use for fast simulations can be found [here](https://github.com/matplo/pyjetty/blob/master/pyjetty/alice_analysis/slurm/sbatch/fastsim/slurm_fastsim_jewel.sh).

This script writes out to ```/rstorage/generators/jewel_alice/tree_fastsim```.
