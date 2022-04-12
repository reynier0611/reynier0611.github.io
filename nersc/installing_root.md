## Installing different software
[Back to table of Contents](../README.md)

```
ssh username@cori.nersc.gov
```

### Installing ROOT

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

### Installing FastJet

I mainly followed the instructions from [http://fastjet.fr/quickstart.html](http://fastjet.fr/quickstart.html) with only a minimal tweak.

I began by creating a directory called ```install``` in my home directory, and modified my ```.bash_profile``` to include:

```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/global/homes/r/reynier/install
export MYINSTALL=/global/homes/r/reynier/install
export PATH=$PATH:/global/homes/r/reynier/install/bin/
```

Then I copied fastjet and installed it:

```
curl -O http://fastjet.fr/repo/fastjet-3.4.0.tar.gz 
tar zxvf fastjet-3.4.0.tar.gz
cd fastjet-3.4.0/

./configure --prefix=$MYINSTALL
make 
make install
```

### Installing FastJet Contrib

I mainly followed the instructions from [https://fastjet.hepforge.org/contrib/](https://fastjet.hepforge.org/contrib/).

```
./configure --prefix=$MYINSTALL --fastjet-config=/project/projectdirs/alice/reynier/fastjet/fastjet-3.4.0/fastjet-config
make
make install
```
