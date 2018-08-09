---
layout: post
title:  "Basics of Image Classification"
date:   2018-08-01 10:48:37 +0100
categories: jekyll update
---

## **Introduction**

![Intro] [logoc]

[logoc]: https://chabbiyosr.github.io/images/post2/techniques.jpg


### Image classification has become one of the key pilot use-cases for demonstrating machine learning. In the previous article, I introduced machine learning, IBM PowerAI, compared GPU and CPU performances while running image classification programs on the IBM Power platform. In this article, let’s take a look at how to check the output at any inner layer of a neural network and train your own model by working with Nvidia DIGITS.




# ***Observing hidden layer parameters***
![AI][logo1]

[logo1]: https://chabbiyosr.github.io/images/post2/nn_blog.png 

#### It wasn’t till the 1980s that researchers discovered adding more layers to a neural network vastly improved its performance. Such neural networks with several hidden layers are common today in several use cases including image classification. Contrary to what the name indicates, it is possible to observe relevant parameters in the hidden layers.



## The process of building a Convolutional Neural Network always involves four major steps.

# **Step - 1 : Convolution**
# **Step - 2 : Pooling**
# **Step - 3 : Flattening**
# **Step - 4 : Full connection**




#### *first of all*, we should **Import the framework and the API needed** like tensorflow, numpy, Keras and Matplotlib  (to learn more about them  [the framework and the API needed in the basics images classification](https://github.com/chabbiyosr/chabbiyosr.github.io/blob/master/_posts/2018-08-01-les%20biblioth%C3%A9ques-utilis%C3%A9es-dans-notre-environement-de-travail.markdown)) and this is the code  :


```python
# TensorFlow and tf.keras
import tensorflow as tf
from tensorflow import keras

# Helper libraries
import numpy as np
import matplotlib.pyplot as plt

print(tf.__version__)
``` 

#### *then*, we should **import the dataset** :
### the code :
```python
fashion_mnist = keras.datasets.fashion_mnist

(train_images, train_labels), (test_images, test_labels) = fashion_mnist.load_data()
````
#### and store them like these for example:
```python
class_names = ['T-shirt/top', 'Trouser', 'Pullover', 'Dress', 'Coat', 
               'Sandal', 'Shirt', 'Sneaker', 'Bag', 'Ankle boot']
               ```

#### *next*, **Explore the data** to put the images in the training set :
### the code :
```python
train_images.shape
len(train_labels)
test_images.shape
len(test_labels)
```

#### **Preprocess the data** : 
#### The data must be preprocessed before training the network. If you inspect the first image in the training

### the code :

```python
plt.figure()
plt.imshow(train_images[0])
plt.colorbar()
plt.gca().grid(False)
train_images = train_images / 255.0

test_images = test_images / 255.0
import matplotlib.pyplot as plt
%matplotlib inline

plt.figure(figsize=(10,10))
for i in range(25):
    plt.subplot(5,5,i+1)
    plt.xticks([])
    plt.yticks([])
    plt.grid('off')
    plt.imshow(train_images[i], cmap=plt.cm.binary)
    plt.xlabel(class_names[train_labels[i]])

```

#### **Build the model**:
#### Building the neural network requires configuring the layers of the model, then compiling the model.

### the code :

```python
# here we can add the hidden layers neural
model = keras.Sequential([
    keras.layers.Flatten(input_shape=(28, 28)),
    keras.layers.Dense(128, activation=tf.nn.relu),
    keras.layers.Dense(10, activation=tf.nn.softmax)
])
# here we can compile the model 
model.compile(optimizer=tf.train.AdamOptimizer(), 
              loss='sparse_categorical_crossentropy',
              metrics=['accuracy']) 
              ```
#### **Train the model**
#### To start training, we sould  call the model.fit method—the model is "fit" to the training data:
### the code:
```python
model.fit(train_images, train_labels, epochs=5)
```

#### **Evaluate accuracy**
#### compare how the model performs on the test dataset:

### the code :
```python
test_loss, test_acc = model.evaluate(test_images, test_labels)

print('Test accuracy:', test_acc)
```

#### *finally*, **Make predictions**
#### With the model trained, we can use it to make predictions about some images. 
### the code :
```python
predictions = model.predict(test_images)
predictions[0]
np.argmax(predictions[0])
test_labels[0]
# Plot the first 25 test images, their predicted label, and the true label
# Color correct predictions in green, incorrect predictions in red
plt.figure(figsize=(10,10))
for i in range(25):
    plt.subplot(5,5,i+1)
    plt.xticks([])
    plt.yticks([])
    plt.grid('off')
    plt.imshow(test_images[i], cmap=plt.cm.binary)
    predicted_label = np.argmax(predictions[i])
    true_label = test_labels[i]
    if predicted_label == true_label:
      color = 'green'
    else:
      color = 'red'
    plt.xlabel("{} ({})".format(class_names[predicted_label], 
                                  class_names[true_label]),
                                  color=color)
      
    # Grab an image from the test dataset
img = test_images[0]

print(img.shape)
# Add the image to a batch where it's the only member.
img = (np.expand_dims(img,0))
​
print(img.shape)
#Now predict the image:
predictions = model.predict(img)

print(predictions)
prediction = predictions[0]

np.argmax(prediction)
```
