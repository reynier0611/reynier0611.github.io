## Naive Bayes for features from text data

<a><button name="button" style = "color:red;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a> <a><button name="button" style = "color:blue;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io/ml/ml.html';">**Back to ML**</button></a>

```python
from sklearn.feature_extraction.text import CountVectorizer

text = ['This is a line',
       'This is another line',
       'Completely different line']
cv = CountVectorizer(stop_words='english')
sparse_matrix = cv.fit_transform(text)
sparse_matrix.todense()
cv.vocabulary_
```

```python
from sklearn.feature_extraction.text import TfidfTransformer
tfidf = TfidfTransformer()
results = tfidf.fit_transform(sparse_matrix)
results.todense()
```

```python
from sklearn.feature_extraction.text import TfidfVectorizer
tv = TfidfVectorizer(stop_words='english')
X_train_tfidf = tv.fit_transform(X_train)
X_test_tfidf = tv.transform(X_test)
```

```python
from sklearn.naive_bayes import MultinomialNB
nb = MultinomialNB()
nb.fit(X_train_tfidf,y_train)
```