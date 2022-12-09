## Pandas <img src="../img/pandas_logo.jpg" width="38" height="40" style="float: right;" />

<a><button name="button" style = "color:red;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a> <a><button name="button" style = "color:blue;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io/ml/ml.html';">**Back to ML**</button></a>

- Selecting a specific type category

```python
df.dtypes
df.select_dtypes(include=[object])
```

- Grabbing a sample of a dataframe

```python
df = df.sample(frac=0.1,random_state=101)
```

- [replace](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.replace.html)