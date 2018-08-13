---
layout: post
title:  "validation error vs trainng error"
date:   2018-08-09 10:48:37 +0100
categories: jekyll update
---
# **introduction: what's Tensorboard ?**

## *TensorBoard: Visualizing Learning*

![Tensor][logoT]

[logoT]: https://chabbiyosr.github.io/images/post4/tensorboard_logo.png

#### The computations you'll use TensorFlow for - like training a massive deep neural network - can be complex and confusing. To make it easier to understand, debug, and optimize TensorFlow programs, we've included a suite of visualization tools called TensorBoard. You can use TensorBoard to visualize your TensorFlow graph, plot quantitative metrics about the execution of your graph, and show additional data like images that pass through it. When TensorBoard is fully configured, it looks like this:

# **validation error vs training error**

![Error][logoE]

[logoE]:https://chabbiyosr.github.io/images/post4/IpI8U.png


#### It is very important to understand the difference between a training error and a test error. Remember that the training error is calculated by using the same data for training the model and calculating its error rate. For calculating the test error, you are using completely disjoint data sets for both tasks.



**loss and accurcy errors**


![Error2][logoE2]

[logoE2]: https://chabbiyosr.github.io/images/post4/tensorboard.png


#### The lower the loss, the better a model (unless the model has over-fitted to the training data). The loss is calculated on training and validation and its interperation is how well the model is doing for these two sets. Unlike accuracy, loss is not a percentage. It is a summation of the errors made for each example in training or validation sets.

In the case of neural networks, the loss is usually negative log-likelihood and residual sum of squares for classification and regression respectively. Then naturally, the main objective in a learning model is to reduce (minimize) the loss function's value with respect to the model's parameters by changing the weight vector values through different optimization methods, such as backpropagation in neural networks.

Loss value implies how well or poorly a certain model behaves after each iteration of optimization. Ideally, one would expect the reduction of loss after each, or several, iteration(s).

The accuracy of a model is usually determined after the model parameters are learned and fixed and no learning is taking place. Then the test samples are fed to the model and the number of mistakes (zero-one loss) the model makes are recorded, after comparison to the true targets. Then the percentage of misclassification is calculated.

For example, if the number of test samples is 1000 and model classifies 952 of those correctly, then the model's accuracy is 95.2%.