## Logistic regression
[Back to table of Contents](../README.md)

[Back to Machine Learning](ml.md)

```python
from sklearn.linear_model import LogisticRegression
log_model = LogisticRegression()
log_model.fit(X_train,y_train)
log_model.coef_
y_pred = log_model.predict(X_test)
log_model.predict_proba(X_test)
```