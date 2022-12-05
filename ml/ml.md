## Machine Learning
[Back to table of Contents](../README.md)

## [Pandas](pandas.md)

## Scikit Learn

- [Splitting and scaling the data (Standard and MinMax scalers)](scaling_data.md)

- Grid search and cross validation

- Pipelines, saving and loading models

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

## Keras / Tensorflow

##### Choosing an optimizer and loss

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

## Other useful links

- [Selecting number of layers and nodes in feed-forward NN](https://stats.stackexchange.com/questions/181/how-to-choose-the-number-of-hidden-layers-and-nodes-in-a-feedforward-neural-netw).