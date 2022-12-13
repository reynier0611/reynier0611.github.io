## Performance Metrics

<a><button name="button" style = "color:red;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a> <a><button name="button" style = "color:blue;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io/ml/ml.html';">**Back to ML**</button></a>

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

- F1 score = 2 * precision * recall / (precision + recall)