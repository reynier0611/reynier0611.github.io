## Machine Learning

<button onclick="window.location.href='https://reynier0611.github.io';">Back to Table of Content</button>

<a><button name="button" style = "color:red;width:100px;height:30px" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a>

### Scikit Learn <img src="../img/sklearn_logo.jpg" width="70" height="40" style="float: right;" />

- [Splitting and scaling the data (Standard and MinMax scalers)](scaling_data.md)

- [Grid search and cross validation](gridsearch.md)

- [Pipelines, saving and loading models](pipe.md)

- Supervised Learning

    - [Linear regression, Ridge, Lasso, Elastic net. Polynomial features](linear.md)
    
    - [Logistic regression](logistic.md)
    
    - [K Nearest Neighbors](knn.md)
    
    - [Support Vector Machines (SVM)](svm.md)
    
    - [Decision Trees, Random Forests, Boosting](trees.md)

    - Naive Bayes
    
    - [Regression and classification performance metrics](supervised_metrics.md)

- Unsupervised Learning

    - K means clustering

    - Hierarchical clustering

    - DBSCAN

    - Principal Component Analysis (PCA)

##### Generic code:
```python
from sklearn.model_family import ModelAlgo
mymodel = ModelAlgo(param1,param2)
mymodel.fit(X_train,y_train)
predictions = mymodel.predict(X_test)

from sklearn.metrics import error_metric
performance = error_metric(y_test,predictions)
```

### Keras / Tensorflow <img src="../img/tf_logo.jpg" width="40" height="40" style="float: right;" />

##### Choosing the activation function of the last layer

Last layer of network:

- Regression: no activation function with one neuron

- Binary classification: ```sigmoid``` with one neuron

- Multi-class classification: ```softmax``` with as many neurons as classes to predict

##### Choosing an optimizer and loss

Keep in mind what kind of problem you are trying to solve:

```python
# For a multi-class classification problem
model.compile(optimizer='rmsprop',
              loss='categorical_crossentropy',
              metrics=['accuracy'])

# For a binary classification problem
model.compile(optimizer='rmsprop',
              loss='binary_crossentropy',
              metrics=['accuracy'])

# For a mean squared error regression problem
model.compile(optimizer='rmsprop',
              loss='mse')
```


- [Feed-forward NN and saving model](feedforward.md)

- [Convolutional NN (CNN)](cnn.md)

- [Recurring NN (RNN)](rnn.md)

### Important Libraries

- [Pandas](pandas.md)

- Numpy

- Matplotlib

- Seaborn

### Other useful links

- [Selecting number of layers and nodes in feed-forward NN](https://stats.stackexchange.com/questions/181/how-to-choose-the-number-of-hidden-layers-and-nodes-in-a-feedforward-neural-netw).

- [Selecting hyperparameters for convolutional NN](https://stats.stackexchange.com/questions/148139/rules-for-selecting-convolutional-neural-network-hyperparameters)

- [Activation functions](https://www.v7labs.com/blog/neural-networks-activation-functions)

- [(YOUTUBE) Data Analysis with Python Course - Numpy, Pandas, Data Visualization](https://www.youtube.com/watch?v=GPVsHOlRBBI)

- [Universal Approximation Theorem](https://en.wikipedia.org/wiki/Universal_approximation_theorem)