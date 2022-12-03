## Scaling the data
[Back to table of Contents](../README.md)

[Back to Machine Learning](ml.md)

We can first fit the scaler (with the training data only) and the fit the training and testing data, or we can directy fit the scaler and transform the training data in one step, and then transform the test data. I show an example of each method below.

#### Standard Scaler

```python
from sklearn.preprocessing import Standard Scaler
scaler = StandardScaler()
scaler.fit(X_train)
X_train = scaler.transform(X_train)
X_test = scaler.transform(X_test)
```

#### Min-Max Scaler

```python
from sklearn.preprocessing import MinMaxScaler
scaler = MinMaxScaler()
X_train = scaler.fit_transform(X_train)
X_test = scaler.transform(X_test)
```