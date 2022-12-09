## Convolutional NN (CNN)

<a><button name="button" style = "color:red;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a> <a><button name="button" style = "color:blue;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io/ml/ml.html';">**Back to ML**</button></a>

### Example on the MNIST dataset (B&W)

Load the data:

```python
from tensorflow.keras.datasets import mnist
(X_train,y_train),(X_test,y_test) = mnist.load_data()
```

The categories in this case come as 1,7,0,3,5,... but we need to one-hot encode these, and that can be done with tensorflow:

```python
from tensorflow.keras.utils import to_categorical
y_cat_train = to_categorical(y_train,num_classes=10)
y_cat_test = to_categorical(y_test,num_classes=10)
```

Then we need to scale the pixel intensities (from 0 to 255) to be between 0 and 1:

```python
X_train = X_train/255
X_test = X_test/255
```

The shape of X is: ```(N,W,H)``` where N is the number of images (60000 in train, 10000 in test sets), and W and H are the width and height (28x28 in these images). We need to change this to: ```(N,W,H,1)```, which is the format expected by the convolutional layers:

```python
X_train = X_train.reshape(60000,28,28,1)
X_test = X_test.reshape(10000,28,28,1)
```

Now build the model and compile it:

```python
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense, Conv2D, MaxPool2D, Flatten

model = Sequential()
model.add(Conv2D(filters=32,kernel_size=(4,4),padding='same',input_shape=(28,28,1),activation='relu'))
model.add(MaxPool2D(pool_size=(2,2)))
model.add(Flatten())
model.add(Dense(128,activation='relu'))
model.add(Dense(10,activation='softmax'))

model.compile(loss='categorical_crossentropy', optimizer='adam',metrics=['accuracy'])
```

The input shape in the convolutional layer, the flattening layer before feeding to dense layers, and the softmax activation function (because of multi-class classification) are not parts of the architecture we can mess with. The number of convolutional and pooling layers, filters, kernel sizes, pool sizes, etc are parameters we can experiment with.

We can now train the model:

```python
from tensorflow.keras.callbacks import EarlyStopping
early_stop = EarlyStopping(monitor='val_loss',patience=1)

model.fit(X_train,y_cat_train,epochs=10,validation_data=(X_test,y_cat_test),callbacks=[early_stop])
```

And finally we can evaluate (e.g. using scikit-learn's classification report and confusion matrix) it and use it to make predictions:

```python
model.metrics_names

metrics[['loss','val_loss']].plot()
metrics[['accuracy','val_accuracy']].plot()

predictions = np.argmax(model.predict(X_test),axis=-1)
```

### Example on CIFAR-10 dataset (color)

```python
model = Sequential()

model.add(Conv2D(filters=32,kernel_size=(4,4),input_shape=(32,32,3), activation='relu'))
model.add(MaxPool2D(pool_size=(2,2)))

model.add(Conv2D(filters=32,kernel_size=(4,4),input_shape=(32,32,3), activation='relu'))
model.add(MaxPool2D(pool_size=(2,2)))

model.add(Flatten())
model.add(Dense(256,activation='relu'))
model.add(Dense(10,activation='softmax'))

model.compile(loss='categorical_crossentropy',optimizer='adam',metrics=['accuracy'])

model.summary()

from tensorflow.keras.callbacks import EarlyStopping
early_stop = EarlyStopping(monitor='val_loss',patience=2)

model.fit(X_train,y_cat_train,epochs=15, validation_data=(X_test,y_cat_test), callbacks=[early_stop])
```
