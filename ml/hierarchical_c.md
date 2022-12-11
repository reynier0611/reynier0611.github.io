## Hierarchical Clustering

<a><button name="button" style = "color:red;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a> <a><button name="button" style = "color:blue;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io/ml/ml.html';">**Back to ML**</button></a>

```python
from sklearn.cluster import AgglomerativeClustering
model = AgglomerativeClustering(n_clusters=4)
cluster_labels = model.fit_predict(scaled_df)

from scipy.cluster.hierarchy import dendrogram
from scipy.cluster import hierarchy 
linkage_matrix = hierarchy.linkage(model.children_)
dendro = dendrogram(linkage_matrix)
```
