## Installing software on my computer
[Back to table of Contents](../README.md)

```
pip install jupyter
pip install pandas
pip install numpy
pip install scikit-learn
python3 -m pip install tensorflow-macos
pip install PyYAML
```

### TensorFlow

When I was trying to install TensorFlow on my mac M1 (```pip install tensorflow```), I was getting the error:

```
Failed to build h5py
ERROR: Could not build wheels for h5py, which is required to install pyproject.toml-based projects
```

I was able to get this fixed following the instructions from [https://www.logcg.com/en/archives/3548.html](https://www.logcg.com/en/archives/3548.html). First I did:

```
brew install hdf5
```

I then did:

```
find /opt -iname "*hdf5.h*"
```

and based on the information prompted on the screen, I edited by ```.bash_profile``` and added:

```
export CPATH="/opt/homebrew/include/"
export HDF5_DIR=/opt/homebrew/
```

After that I did:

```
python3 -m pip install tensorflow-macos
```

and TensorFlow was properly installed.