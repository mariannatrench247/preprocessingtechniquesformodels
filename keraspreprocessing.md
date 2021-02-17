# QUESTIONS TO ASK MYSELF BEFORE PREPROCESSING ?
### What kind of data am I working with ? (images, text, audio, etc)
### What kind of outcome am I seeking with data? 
### How / where will the data work with the model ? 
### 
### Feature Selection : selecting/discarding relevant / irrelevant features 
### Feature Extraction : (m) attributes --> (n) attributes


Available preprocessing layers

Core preprocessing layers
TextVectorization layer: turns raw strings into an encoded representation that can be read by an Embedding layer or Dense layer.
Normalization layer: performs feature-wise normalize of input features.


# Preprocessing data before model or inside 

### Part of model 
##### preprocessing will happen on device, benefit from GPU accleration

inputs = keras.Input(shape=input_shape)
x = processing_layer(inputs)
outputs = rest_of_the_model(x)
model = keras.Model(inputs, outputs)

### Apply it to tf.data.Dataset 
##### obtain dataset that yields batches of preprocessed data 
##### preprocessing will happen on CPU, buffered more before going into model
##### may want to export infered only end2end model, will include preprocessing
###### makes model portable and reduce training/serving skew 

dataset = dataset.map(lambda x, y:(preprocessing_layer(x), y))
  
