## Autoencoders

<a><button name="button" style = "color:red;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a> <a><button name="button" style = "color:blue;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io/ml/ml.html';">**Back to ML**</button></a>

#### Autoencoder for simple 3-feature data

- Instead of the Adam optimizer, with autoencoders we want to use Stochastic Gradient Descent so that we can play with the learning rate.

```python
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense
from tensorflow.keras.optimizers import SGD
```

This model will have an encoder that compresses the data from 3 dimensions to 2, and then a decoder that expands from 2 back to 3 dimensions, as shown in the diagram below:

<img src="img/autoencoder.jpg" width="300" height="200" style="float: center;" />