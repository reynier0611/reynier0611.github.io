## Pandas
[Back to table of Contents](../README.md)

[Back to Machine Learning](ml.md)

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