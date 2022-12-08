## Pipelines, Saving and Loading models
[Back to table of Contents](../README.md)

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