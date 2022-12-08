## Performance Metrics
[Back to table of Contents](../README.md)

[Back to Machine Learning](ml.md)

Create an array with model predictions ```y_pred``` by passing the test set ```X_test``` after the model has been trained, e.g.:

```python
y_pred = model.predict(X_test)
```

This array is to be compared with the actual labels from the test set ```y_test```.

### Regression Performance Metrics

```python
from sklearn.metrics import mean_absolute_error, mean_squared_error
mean_absolute_error(y_test,y_pred)
np.sqrt(mean_squared_error(y_test,y_pred))
```

### Classification Performance Metrics

- Receiver operating characteristic [ROC](https://en.wikipedia.org/wiki/Receiver_operating_characteristic) curve (only for binary classification):

```python
from sklearn.metrics import roc_curve, RocCurveDisplay
fpr, tpr, thresholds = roc_curve(y_true,y_pred)
RocCurveDisplay(fpr=fpr, tpr=tpr).plot()
```

fpr and tpr stand for false and true positive rates.

- Confusion matrix:

```python
from sklearn.metrics import confusion_matrix,ConfusionMatrixDisplay

cm = confusion_matrix(y_test,y_pred)
ConfusionMatrixDisplay(cm).plot()
```

- Classification report:

```python
from sklearn.metrics import classification_report
print(classification_report(y_test,y_pred))
```

- Accuracy score:

```python
from sklearn.metrics import accuracy_score
accuracy_score(y_test,y_pred)
```

- Other metrics for classification:

```python
from sklearn.metrics import precision_score, recall_score
```