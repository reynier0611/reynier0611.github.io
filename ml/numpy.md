## Numpy <img src="../img/numpy_logo.jpg" width="40" height="40" style="float: right;" />

<a><button name="button" style = "color:red;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a> <a><button name="button" style = "color:blue;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io/ml/ml.html';">**Back to ML**</button></a>

```python
import numpy as np
```

- Casting list to a np array:

```python
np.array([1,2,3])
```

#### arange

Returns integers given a start, stop (not included), and stepsize (default is 1):

```python
np.arange(start=0,stop=10,step=2)
```

returns: ```array([0,2,4,6,8])```

#### zeros and ones:

* zeros

```python
np.zeros((3,4))
```

returns:

```
array([[0.,0.,0.,0.],
	[0.,0.,0.,0.],
	[0.,0.,0.,0.]])
```

* ones

```python
np.ones((3))
```

returns:

```
array([1.,1.,1.])
```

* another arbitrary number by multiplying times ones

```python
np.ones((4))*5
```

returns:

```
array([5.,5.,5.,5.])
```

#### linspace:

Evenly spaced numbers over a specified interval. Includes stop value.

```python
np.linspace(0,10,3)
```

returns

```
array([0., 5., 10.])
```

#### Identity matrix:

```python
np.eye(3)
```

returns

```
array([[1., 0., 0.],
	[0., 1., 0.],
	[0., 0., 1.]])
```

#### Percentiles

```python
q75, q25 = np.percentile(sample,[75,25])
```

#### Reshaping

```python
arr = np.arange(24)
arr.shape # --> (25,)
arr = arr.reshape(5,5) # Not permanent. Need to reassign.
arr.shape # --> (5,5)
```

### max and argmax:

```python
arr.max() # --> Returns max value in the array
arr.argmax() # --> Returns the index location of the max value in the array
```

- similar with min and argmin.

### Data types:

```python
arr.dtype # --> Returns, e.g.dtype('int32')
```

### Random sampling

#### Seed

```python
np.random.seed(101)
```

#### Uniform sampling:

The line below returns three random numbers in the range ```[0,1)``` sampled uniformly:

```python
np.random.rand(3)
```

- The following gives a shape of 3 rows by 4 columns:

```python
np.random.rand(3,4)
```

#### Normal sampling:

* standard normal distribution (mean=0, variance=1):

```python
np.random.randn(3)
```

* more general normal distribution:

```python
np.random.normal(mean,std_dev,shape)
```

#### Random integers:

```python
np.random.randint(start,stop,shape)
```

### Numpy operations

```python
arr = np.array(0,1,2)
arr + 5
```

this returns ```array([5,6,7])``` as the operation is done on an element-by-element basis.

- Similar with array-array operations:

```python
arr = np.array(2,3,4)
arr*arr
```

this returns: ```array([4,9,16])```.

* [Universal array functions](https://numpy.org/doc/stable/reference/ufuncs.html)