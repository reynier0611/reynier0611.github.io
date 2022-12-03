## Machine Learning
[Back to table of Contents](../README.md)

- [Selecting number of layers and nodes in feed-forward NN](https://stats.stackexchange.com/questions/181/how-to-choose-the-number-of-hidden-layers-and-nodes-in-a-feedforward-neural-netw).

### Scikit Learn

- [Scaling data (Standard and MinMax scalers)](scaling_data.md)

- [Splitting data](splitting_data.md)

### Keras / Tensorflow

### Choosing an optimizer and loss

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