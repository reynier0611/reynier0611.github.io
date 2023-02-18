## Python <img src="img/python_logo.jpg" width="40" height="40" style="float: right;" />

<a><button name="button" style = "color:red;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a> 

- [5 ways to Fibonacci in Python](https://technobeans.com/2012/04/16/5-ways-of-fibonacci-in-python/)

### Collections

[Python collections](https://docs.python.org/3/library/collections.html)

```python
import collections
```

### Default dictionary

dict subclass that calls a factory function to supply missing values

```python
ans = collections.defaultdict()
```

#### Counter

dict subclass for counting hashable objects

```python
word = 'weerrtyuy'
count = collections.Counter(word)
```

```python
Counter({'w': 1, 'e': 2, 'r': 2, 't': 1, 'y': 2, 'u': 1})
```

Here's an implementation:

```python
mydict = {}
for let in word:
    if let in mydict: mydict[let] += 1
    else: mydict[let] = 1
mydict
```