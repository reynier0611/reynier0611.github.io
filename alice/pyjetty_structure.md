## Notes on pyjetty structure
[Back to table of Contents](../README.md)

* plots found in ```performance/mc_projections_both```, ```performance/mc_projections_det```, and ```performance/mc_projections_truth``` are put together in:
```analysis/user/rey/plotting_utils.py```

the function ```plot_obs_projection``` gets called in ```plot_obs_projections``` (note s at the end) a couple of times.

* plots found in ```main/Unfolded_...``` are put together in:
```analysis/user/substructure/roounfold_obs.py```

* prior scaling is done in: ```/home/rey/pyjetty/cpptools/src/rutil/rutil.cxx```

## Closure Tests:

* closure tests done in: ```analysis/user/substructure/roounfold_obs.py``` in the function ```unfolding_checks```

   - refolding test: ```refolding_test```
   - and statistical closure test: ```statistical_closure_test```
   - shape closure test done in function: ```shape_closure_test```
      - the shape closure test uses the function ```scale_by_prior``` defined in ```analysis/base/analysis_utils.py```
   - thermal closure test: ```plot_thermal_closure_test```

## Response-Matrix Slices:

* response-matrix slices plotted in: ```analysis/user/substructure/roounfold_obs.py``` (see function ```plot_RM_slices```)

## Unfolding

Done in ```analysis/user/substructure/roounfold_obs.py```. Search the code for the line that reads ```unfold_bayes = ROOT.RooUnfoldBayes(response, hData, i)```. The unfolded (truth) distribution is then obtained by doing: ```hUnfolded = unfold_bayes.Hreco(self.errorType)```. See documentation for these functions [here](https://hepunx.rl.ac.uk/~adye/software/unfold/htmldoc-dev/RooUnfoldBayes.html). The RooUnfold source code is [here](https://github.com/skluth/RooUnfold/blob/master/src/RooUnfoldBayes.cxx). Additional notes are [here](https://gitlab.cern.ch/RooUnfold/RooUnfold/-/blob/master/README.md) and a practical example is [here](https://gitlab.cern.ch/RooUnfold/RooUnfold/blob/master/examples/RooUnfoldExample.py).
