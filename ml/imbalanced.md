## Dealing with mbalanced datasets

<a><button name="button" style = "color:red;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a> <a><button name="button" style = "color:blue;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io/ml/ml.html';">**Back to ML**</button></a>

- Loading more data
- Changing perfomance metrics
- Resampling (undersampling or oversampling)
- Changing the algorithm (e.g. using penalized models)

### Stratifying with test_train_split

```python
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X,y,test_size=0.3, 
                                                    stratify=y)
```

### Undersampling majority class

```python
!pip install imblearn
from imblearn.under_sampling import RandomUnderSampler

rus = RandomUnderSampler(random_state=0)
x_resampled,y_resampled = rus.fit_resample(x,y)
```

### Oversampling minority class

Can use a package like ```SMOTE```, which involves the following steps:
- Find difference between a point and its nearest neighbor
- Multiply difference by random number between 0 and 1
- Add this difference to original point to create a new synthetic example
- Continue with your next-nearest neighbor until you reach the desired number of iterations

### Combination of oversampling and undersampling

With ```SMOTETomek``` we can first oversample minority class and then undersample to remove samples close to the class boundary.

```python
from imblearn.combine import SMOTETomek
from imblearn.over_sampling import SMOTE
from imblearn.under_sampling import TomekLinks

## Oversampling
s= SMOTE()
X_res, y_res= s.fit_resample(X_train, y_train)


## Undersampling
tk= TomekLinks()
X_res2, y_res2= tk.fit_resample(X_train, y_train)

## Combination
smt= SMOTETomek()
X_res1, y_res1= smt.fit_resample(X_train, y_train)
```

### Weighted models

```python
# define class weights
w = {0:1, 1:99}

# define model
lg2 = LogisticRegression(random_state=13, class_weight=w)
```