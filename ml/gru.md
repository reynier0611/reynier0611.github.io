## Gated Recurrent Unit ([GRU](https://keras.io/api/layers/recurrent_layers/gru/)) for NLP

<a><button name="button" style = "color:red;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a> <a><button name="button" style = "color:blue;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io/ml/ml.html';">**Back to ML**</button></a>

1. Load the data, get all unique characters, create variables to go from characters to their assigned indices and from indices to characters, and then encode text into integers:

```python
text = open('path/to/file.txt','r').read()
vocab = sorted(set(text))
char_to_ind = {char:ind for ind,char in enumerate(vocab)}
ind_to_char = np.array(vocab)
encoded_text = np.array([char_to_ind[c] for c in text])
```

2. Create data batches:

```python
seq_len = 120
total_num_seq = len(text) // (seq_len+1)

import tensorflow as tf
char_dataset = tf.data.Dataset.from_tensor_slices(encoded_text)
sequences = char_dataset.batch(seq_len+1,drop_remainder=True)

def create_seq_targets(seq):
    input_txt = seq[:-1] # e.g. "Hello my nam"
    target_txt = seq[1:] # e.g. "ello my name"
    return input_txt, target_txt

dataset = sequences.map(create_seq_targets)

batch_size = 128
buffer_size = 10000
dataset = dataset.shuffle(buffer_size).batch(batch_size,drop_remainder=True)
```

3. Create the model:

```python
vocab_size = len(vocab)
embed_dim = 64 # Same order of mag as vocab size
rnn_neurons = 1026
```

- Create a custom loss function:

```python
from tensorflow.keras.losses import sparse_categorical_crossentropy

def sparse_cat_loss(y_true,y_pred):
    return sparse_categorical_crossentropy(y_true,y_pred,from_logits=True)
```

- Here's where we actually create the model:

```python
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Embedding, GRU, Dense

def create_model(vocab_size,embed_dim,rnn_neurons,batch_size):
    model = Sequential()
    model.add(Embedding(vocab_size,embed_dim,batch_input_shape=[batch_size,None]))
    model.add(GRU(rnn_neurons,return_sequences=True,stateful=True,
                 recurrent_initializer='glorot_uniform'))
    model.add(Dense(vocab_size))
    model.compile('adam',loss=sparse_cat_loss)
    return model

model = create_model(vocab_size=vocab_size,embed_dim=embed_dim,rnn_neurons=rnn_neurons,batch_size=batch_size)
```

4. Train the model:

```python
model.fit(dataset,epochs=30)
```

5. Load the model:
This consumed lots of resources, so the class had the model already saved and we loaded it to see what it did. But instead of loading the whole model, we created a new instance of the untrained model and then only loaded the weights from the trained model. Finally we need to build the model.

```python
from tensorflow.keras.models import load_model

model = create_model(vocab_size=vocab_size,embed_dim=embed_dim,rnn_neurons=rnn_neurons,batch_size=1)
model.load_weights('path/to/previously_trained_model.h5')
model.build(tf.TensorShape([1,None]))
```

6. Create a function to generate new text and use it:

```python
def generate_text(model,start_seed,gen_size=500,temp=1.0):
    num_generate = gen_size
    input_eval = [char_to_ind[s] for s in start_seed]
    input_eval = tf.expand_dims(input_eval,0)
    text_generated = []
    temperature = temp
    model.reset_states()
    
    for i in range(num_generate):
        predictions = model(input_eval)
        predictions = tf.squeeze(predictions,0)
        predictions = predictions/temperature
        predicted_id = tf.random.categorical(predictions,num_samples=1)[-1,0].numpy()
        input_eval = tf.expand_dims([predicted_id],0)
        text_generated.append(ind_to_char[predicted_id])
    return (start_seed+"".join(text_generated))
```

```python
print(generate_text(model,"JULIET",gen_size=1000))
```



