## Fun4All
[Back to table of Contents](../README.md)

---

### Using the Fun4All event display

Run the code with no events generated, load the DisplpayOn.C macro, and create a PHG4Reco object:
```
.x Fun4All_macro(-1)
.L DisplayOn.C
PHG4Reco *g4 = DisplayOn()
```
You can ask Fun4All for some commands to change properties of the event display by typing:
```
displaycmd()
```
Here are a few examples. For instance, to rotate the scene, you can do:
```
g4->ApplyCommand("/vis/viewer/set/viewpointThetaPhi 270 0") // this is a side view of the detector
g4->ApplyCommand("/vis/viewer/set/viewpointThetaPhi 270 -89.9") // top-down view.
```
You can run an event by doing:
```
g4->ApplyCommand("/Fun4All/set_field 1.5”)
g4->ApplyCommand("/Fun4All/run 1")
```
Saving the event display can be done with:
```
g4->ApplyCommand("/vis/ogl/set/printMode pixmap")
g4->ApplyCommand("/vis/ogl/set/printSize 2880 1800")
g4->ApplyCommand("/vis/ogl/printEPS")
```
To zoom in or out, execute the following command. Using a number > 1 (e.g. zoom 1.5) zooms in. Using a number 0 < number < 1 (e.g. zoom 0.5) zooms out.
```
g4->ApplyCommand("/vis/viewer/zoom 1")
```

---

### Useful presentations related to Fun4All
['Detector Configurations in Simulations' by Friederike Bock & Nicolas Schmidt](https://indico.bnl.gov/event/11112/contributions/47261/attachments/33424/53719/ECCE_Ornl.pdf)
