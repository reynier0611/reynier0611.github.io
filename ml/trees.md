## Decision Trees, Random Forests, Boosting

<a><button name="button" style = "color:red;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a> <a><button name="button" style = "color:blue;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io/ml/ml.html';">**Back to ML**</button></a>

#### Decision trees

```python
from sklearn.tree import DecisionTreeClassifier

from sklearn.tree import plot_tree

plt.figure(figsize=(10,8))
plot_tree(model, feature_names=X.columns, filled=True)
```

#### Random Forest 

###### Classifier

```python
from sklearn.ensemble import RandomForestClassifiera
```

###### Regressor

```python
from sklearn.ensemble import RandomForestRegressor
```

#### Boosted trees

```python
from sklearn.ensemble import GradientBoostingRegressor, AdaBoostRegressor
from sklearn.ensemble import GradientBoostingClassifier, AdaBoostClassifier
```