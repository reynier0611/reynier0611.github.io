## Linear regression, Ridge, Lasso, Elastic net. Polynomial features
[Back to table of Contents](../README.md)

[Back to Machine Learning](ml.md)

#### Linear regression

```python
from sklearn.linear_model import LinearRegression
model = LinearRegression()
model.fit(X_train,y_train)
predictions = model.predict(X_test)
```

#### Ridge, Lasso, Elastic net

```python
from sklearn.linear_model import Ridge
from sklearn.linear_model import Lasso
from sklearn.linear_model import ElasticNet
```

and with cross-validation:

```python
from sklearn.linear_model import RidgeCV
from sklearn.linear_model import LassoCV
from sklearn.linear_model import ElasticNetCV
```

#### Adding polynomial features to the data

```python
from sklearn.preprocessing import PolynomialFeatures
polynomial_converter = PolynomialFeatures(degree=2,include_bias=False)
polynomial_converter.fit_transform(X)
```