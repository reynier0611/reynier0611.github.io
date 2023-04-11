## O2 Notes

<a><button name="button" style = "color:red;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a>

I am working on this in my ```WORK/ALICE/O2/``` directory in my computer.

### Some useful links

- See chapter 4 of Matteo's [PhD thesis](https://iris.polito.it/retrieve/e384c432-395f-d4b2-e053-9f05fe0a1d67/conv_phdthesis.pdf).

- Default tracking configuration parameters [here](https://github.com/AliceO2Group/AliceO2/blob/dev/Detectors/ITSMFT/ITS/tracking/include/ITStracking/TrackingConfigParam.h).


### Simulations for ITS studies:

First do:

```shell
alienv enter O2sim/latest-o2
```

Running the simulation (generating particles and propagating them through Geant)

```shell
o2-sim -n 10000 -m PIPE ITS -g pythia8pp -e TGeant4 -j 2
```

Then we should run the digitization:

```shell
o2-sim-digitizer-workflow
```

Finally run the reconstruction:

```shell
o2-its-reco-workflow  --trackerCA --tracking-mode sync --configKeyValues "fastMultConfig.cutMultClusLow=-1;fastMultConfig.cutMultClusHigh=-1;fastMultConfig.cutMultVtxHigh=-1;ITSVertexerParam.phiCut=0.5;ITSVertexerParam.clusterContributorsCut=3;ITSVertexerParam.tanLambdaCut=0.2;;"
```

### Scripts Matteo recommended to see how the data is accessed

```bash
O2/Detectors/ITSMFT/ITS/macros/test/CheckTracksCA.C
```

```bash
O2/Detectors/ITSMFT/ITS/macros/test/CheckVertices.C
```

### Meeting with Matteo Concas on April 3, 2023:

#### Steps to install O2:

1. Install aliBuild and prerequisites described in analysis tutorial page: [https://alice-doc.github.io/alice-analysis-tutorial/building/prereq-macos.html](https://alice-doc.github.io/alice-analysis-tutorial/building/prereq-macos.html)

2. Get both O2DPG and O2 in development mode:

```bash
git clone https://github.com/AliceO2Group/AliceO2.git O2
git clone https://github.com/AliceO2Group/O2DPG.git O2DPG
```

3. Initialize the environment:

```bash
aliBuild init
```

4. Build:

```bash
aliBuild build O2sim --defaults o2 -d
```
