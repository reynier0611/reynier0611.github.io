## Seaborn <img src="../img/seaborn_logo.jpg" width="40" height="40" style="float: right;" />

<a><button name="button" style = "color:red;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a> <a><button name="button" style = "color:blue;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io/ml/ml.html';">**Back to ML**</button></a>

```python
import seaborn as sns
```

```python
scat = sns.scatterplot(x='A',y='B',data=df,hue='C')
```

<img src="img/sns_scatterplot.jpg" width="300" height="200" style="float: center;" />

```python
sns.rugplot(x='A',data=df)
sns.displot(data=df,x='A',bins=20)
sns.histplot(data=df,x='A',bins=20,kde=True)
sns.kdeplot(data=df,x='A')
```

<img src="img/sns_hists.jpg" width="650" height="160" style="float: center;" />

```python
sns.countplot(data=df,x='A')
sns.barplot(data=df,x='A',y='B',estimator=np.mean,ci='sd')
```

<img src="img/sns_count.jpg" width="500" height="180" style="float: center;" />

```python
sns.boxplot(data=df,y='numerical data',x='categories')
sns.violinplot(data=df,y='numerical data',x='categories')
sns.swarmplot(data=df,x='numerical data',y='categories')
sns.boxenplot(data=df,x='numerical data',y='categories')
```

<img src="img/sns_box.jpg" width="500" height="300" style="float: center;" />

### Comparison plots

```python
sns.jointplot(data=df,x='A',y='B',kind='scatter') # or kind hex, hist, kde
```

<img src="img/sns_jointplot.jpg" width="200" height="200" style="float: center;" />

```python
sns.pairplot(data=df)
```

<img src="img/sns_pairplot.jpg" width="500" height="500" style="float: center;" />

```python
sns.catplot(data=df,x='numerical var',y='cat 1',kind='box',row='cat 2',col='cat 3')


g = sns.PairGrid(df)
g = g.map_upper(sns.scatterplot)
g = g.map_lower(sns.kdeplot)
g = g.map_diag(sns.histplot)

sns.heatmap(data=df,linewidth=0.5,annot=True, cmap='viridis')

sns.clustermap(data=df,linewidth=0.5,annot=True, cmap='viridis')
```
