## Using Jupyter Notebooks  on Cori
[Back to table of Contents](../README.md)

ML repo is [here](https://github.com/jdmulligan/ml-hadronization).

Logon to perlmutter:

```
ssh reynier@perlmutter-p1.nersc.gov
```

Request an interactive node from the slurm batch system:

```
salloc --nodes 1 --qos interactive --time 04:00:00 --constraint gpu --gpus 4 --account=alice_g
```