## Principal Component Analysis

<a><button name="button" style = "color:red;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a> <a><button name="button" style = "color:blue;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io/ml/ml.html';">**Back to ML**</button></a>

```pythia
from sklearn.decomposition import PCA

pca_model = PCA(n_components=2)
principal_components = pca_model.fit_transform(scaled_X)
pca_model.components_
pca_model.explained_variance_ratio_
```

Elbow method to determine optimal number of components

```pythia
explained_variance = []

for n in range(1,30):
    pca = PCA(n_components=n)
    pca.fit(scaled_X)
    
    explained_variance.append(np.sum(pca.explained_variance_ratio_))

plt.plot(list(range(1,30)),explained_variance)
plt.xlabel('Num of components')
plt.ylabel('Variance Explained')
```
