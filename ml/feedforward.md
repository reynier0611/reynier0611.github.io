## Feed-Forward NN
[Back to table of Contents](../README.md)

[Back to Machine Learning](ml.md)

Here we need the training and testing data as numpy arrays, not as pandas dataframes, for instance. Thus, if we have our data as pandas dataframes can do something like:

```python
X_train = X_train.values
y_train = y_train.values
X_test = X_test.values
y_test = y_test.values
```

Below we create and compile the model, and then train it.

```python
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense,Dropout

model = Sequential()
model.add(Dense(79,'relu'))
model.add(Dropout(0.5))
model.add(Dense(39,'relu'))
model.add(Dropout(0.5))
model.add(Dense(19,'relu'))
model.add(Dense(1,'sigmoid'))

model.compile(loss='binary_crossentropy',optimizer='adam')

model.fit(x=X_train,y=y_train,epochs=30,verbose=0,batch_size=256,
	      validation_data=(X_test,y_test))
```

##### Saving the model

```python
from tensorflow.keras.models import load_model
model.save('my_03_model.h5')
```

##### Predictions

- If your model does binary classification (e.g. if it uses a sigmoid last-layer activation):

```python
predictions = (model.predict(X_test) > 0.5).astype(int)
```

- If your model does multi-class classification: (e.g. if it uses a softmax last-layer activation):

```python
predictions = np.argmax(model.predict(X_test), axis=-1)
```

See discussion [here](https://discuss.tensorflow.org/t/sequential-object-has-no-attribute-predict-classes/10157/3).
