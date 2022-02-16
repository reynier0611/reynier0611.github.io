# QC and EPN/PDP Shift Instructions

[Back to table of Contents](../README.md)

[Hyperloop](https://alimonitor.cern.ch/hyperloop/)

## Training

The hyperloop training event can be found [here](https://indico.cern.ch/event/1122163/).

The prerequisites for the training can be found [here](https://docs.google.com/document/d/1ZLGyHL5eUsYWQUJzI7Nt_l5218UIw8lzyWf0SohoQNA/edit).

### Development version of hyperloop

This was used for the training. Basically, this is a local version of hyperloop and tests done here don't affect the actual hyperloop operation. To access if follow the steps below:

First of all, connect via proxy. Instructions can be found [here](https://security.web.cern.ch/recommendations/en/ssh_browsing.shtml).
After proxy has been properly setup, go to a terminal and enter:

```ssh -D 8080 lxtunnel.cern.ch -N -l username```, followed by the password.

Now you should be able to access [https://alihyperloop.cern.ch/dev/](https://alihyperloop.cern.ch/dev/)