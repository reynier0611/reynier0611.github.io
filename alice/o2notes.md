## O2 Notes

<a><button name="button" style = "color:red;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a>

I am working on this in my ```WORK/ALICE/O2/``` directory.

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
