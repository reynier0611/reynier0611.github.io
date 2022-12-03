## Scaling the data
[Back to table of Contents](../README.md)

[Back to Machine Learning](ml.md)

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