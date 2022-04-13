## ITS3 Test Beam Analysis
[Back to table of Contents](../README.md)

* Wiki with all relevant information to get started is [here](https://twiki.cern.ch/twiki/bin/viewauth/ALICE/GettingStartedWithTestbeamAnalysis).

### Running the example:
```
./pull_container.sh
./run_container.sh
./run_analysis_example.sh
```

Upon inspection of ```./run_analysis_example.sh``` one sees there are four main steps in the chain:

1. ```corry -c configs/createmask.conf```
2. ```corry -c configs/prealign.conf```
3. ```corry -c configs/align.conf```
4. ```corry -c configs/analyse.conf```

The first one basically removes the noisy and dead pixels from the sample.

The secound one gathers the information necessary to align the layers.