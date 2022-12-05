## Decision Trees, Random Forests, Boosting
[Back to table of Contents](../README.md)

[Back to Machine Learning](ml.md)

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

###### Random Forest Regressor

```python
from sklearn.ensemble import RandomForestRegressor
```

#### Boosted trees

```python
from sklearn.ensemble import GradientBoostingRegressor, AdaBoostRegressor
from sklearn.ensemble import GradientBoostingClassifier, AdaBoostClassifier
```