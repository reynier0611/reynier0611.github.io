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

[This](https://twiki.cern.ch/twiki/bin/view/ALICE/ITS3WP3DESY2020August?id=1&filename=IMG_2726.jpg#igp1) is the page where you can find the details of the setup for the example.

All test beam runs in the past are [here](https://twiki.cern.ch/twiki/bin/view/ALICE/ITS3WP3).


#### Output log (after changing the number of events to 1000):
- Step 1: see [here](its3_test_beam_step1.md)
- Step 2: see [here](its3_test_beam_step2.md)
- Step 3: see [here](its3_test_beam_step3.md)
- Step 4: see [here](its3_test_beam_step4.md)