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

[logoE]: https://chabbiyosr.github.io/images/post4/IpI8U.png


#### It is very important to understand the difference between a training error and a test error. Remember that the training error is calculated by using the same data for training the model and calculating its error rate. For calculating the test error, you are using completely disjoint data sets for both tasks.

