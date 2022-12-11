## Numpy <img src="../img/numpy_logo.jpg" width="40" height="40" style="float: right;" />

<a><button name="button" style = "color:red;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a> <a><button name="button" style = "color:blue;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io/ml/ml.html';">**Back to ML**</button></a>

```python
import numpy as np
```

- Casting list to a np array: ```np.array([1,2,3])```

#### arange

```python
np.arange(start=0,stop=10,step=2)
```

returns: ```array([0,2,4,6,8])```

#### Zeros and Ones:

```python
np.zeros((3,4))
```

returns:

```
array([[0.,0.,0.,0.],
	   [0.,0.,0.,0.],
 	   [0.,0.,0.,0.]])
```

returns

#### Seed

```python
np.random.seed(101)
```

#### Percentiles

```python
q75, q25 = np.percentile(sample,[75,25])
```