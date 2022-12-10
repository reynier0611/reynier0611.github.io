## Pipelines, Saving and Loading models

<a><button name="button" style = "color:red;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a> <a><button name="button" style = "color:blue;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io/ml/ml.html';">**Back to ML**</button></a>

### Pipelines

```python
from sklearn.pipeline import Pipeline
operations = [('scaler',scaler),('knn',knn)]
pipe = Pipeline(operations)
k_values=list(range(1,20))
param_grid = {'knn__n_neighbors':k_values}

from sklearn.model_selection import GridSearchCV
full_cv_classifier = GridSearchCV(pipe,param_grid,cv=5,scoring='accuracy')
full_cv_classifier.fit(scaled_X_train,y_train)
```

### Saving and loading models

Saving:

```python
from joblib import dump
dump(final_model,'trained_model.joblib')
dump(list(X.columns),'colnames.pkl')
```

Loading:

```python
from joblib import load
loaded_model = load('trained_model.joblib')
new_columns = joblib.load('colnames.pkl')
```

* sometimes it is useful to save the column names for the dataframe. This is not strictly needed though.