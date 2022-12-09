## Pipelines, Saving and Loading models

<a><button name="button" style = "color:red;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a> <a><button name="button" style = "color:blue;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io/ml/ml.html';">**Back to ML**</button></a>

### Pipelines


### Saving and loading models

Saving:

```python
from joblib import dump
dump(final_model,'trained_model.joblib')
```

```python
from joblib import load
loaded_model = load('trained_model.joblib')
```