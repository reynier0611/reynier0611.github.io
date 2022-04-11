## Installing ROOT
[Back to table of Contents](../README.md)

```
ssh username@cori.nersc.gov
```

First time:

```
module load python
conda config --set channel_priority strict
mamba create -c conda-forge --name cernroot root==6.24.6
conda activate cernroot
```

After that only do the last step:

```
module load python
conda activate cernroot
```

and then, to deactivate the environment do:

```
conda deactivate
```