## Grid search and cross validation
[Back to table of Contents](../README.md)

[Back to Machine Learning](ml.md)

#### Example with an elastic net model

Import the model for which parameters are to be optimized and create an instance.

```python
from sklearn.linear_model import ElasticNet
base_elastic_net_model = ElasticNet()
```

Create a dictionary with the parameters to test. The strings must match hyperparams in the model being optimized.

```python
param_grid = {'alpha':[0.1,1,5,10,50,100],'l1_ratio':[.1,.5,.7,.95,.99,1]}
```

Pass all this into a ```GridSearchCV``` object, and then treat the object like the model itself:

```python
from sklearn.model_selection import GridSearchCV
grid_model = GridSearchCV(estimator=base_elastic_net_model,
                         param_grid=param_grid,
                         scoring='neg_mean_squared_error',
                         cv=5,verbose=2)

grid_model.fit(X_train,y_train)
```

We can then check which of the provided parameters performed better in the cross validation.

```python
grid_model.best_estimator_
grid_model.best_params_
```

Checking the results

```python
pd.DataFrame(grid_model.cv_results_)
```