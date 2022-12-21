## Pandas <img src="../img/pandas_logo.jpg" width="38" height="40" style="float: right;" />

<a><button name="button" style = "color:red;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a> <a><button name="button" style = "color:blue;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io/ml/ml.html';">**Back to ML**</button></a>

### Series

```python
mySeries = pd.Series(data=[1,2,3],index=['A','B','C'])
```

or

```python
mydict = {'A':1,'B':2,'C':3}
mySeries = pd.Series(mydict)
```

### Selecting a specific type category

```python
df.dtypes
my_object_df = df.select_dtypes(include=['object'])
my_numeric_df = df.select_dtypes(exclude=['object'])
```

### One-hot encoding categorical data:

```python
df_objects_dummies = pd.get_dummies(my_object_df,drop_first=True)
```

### Grabbing a sample of a dataframe

```python
df = df.sample(frac=0.1,random_state=101)
```

### Apply and lambda expression:

```python
def multiply(x,y): return x*y
df['A_x_B'] = df.apply(lambda x: multiply(x['A'],x['B']),axis=1)
```

### DataFrame indices

```python
df = df.set_index('col_name')
df = df.reset_index()
```

### Useful commands:

```python
df.head()
df.tail()
df.info()
df.describe.transpose()
```

### Handling missing data:

```python
df.dropna()
df.dropna(axis=1)
df.fillna()
df['A'] = df['A'].fillna(value=0.0)
df['B'] = df['B'].fillna(value=df['B'].mean())
df = df.fillna(value=df.mean())
```

### groupby:

```python
df.groupby('Year').sum(numeric_only=True).sort_index(ascending=False)
```

- Multi-index groupby:

```python
df.groupby(['Year','Sector']).sum(numeric_only=True)
```

- Grouped summary statistics

```python
df.groupby('Year').describe()
```

* [13 functions to aggregate](https://cmdlinetips.com/2019/10/pandas-groupby-13-functions-to-aggregate/)

### Other operations:

```python
df['Year'].unique()
df['Year'].nunique()
df['Year'].value_counts()
```

- Max value and index of this max value (similar with min):

```python
df['col1'].max()
df['col1'].idxmax()
```

- Sort values:

```python
df.sort_values('col1',ascending=False)
```

### Joining dataframes:

```python
df_new = pd.concatenate([df1,df2],axis=1)
```

```python
df_new = pd.merge(left=df1,right=df2,on='col1',how='inner')
```

### drop rows with all zeros

```python
df.loc[~(df==0).all(axis=1)]
df.loc[(df!=0).any(axis=1)]
```

see discussion [here](https://stackoverflow.com/questions/22649693/drop-rows-with-all-zeros-in-pandas-data-frame).

### Useful links:

- [Pandas Documentation](https://pandas.pydata.org/docs/user_guide/index.html)

- [Input / Output](https://pandas.pydata.org/docs/user_guide/io.html)

- [replace](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.replace.html)