# Machine learning

* finds rules based on data
* AI > ML > NN

## basics
* `feature` - input data, what we feed to the label to get the output
* `label` - output data, what we are looking for
* `feature` --> label
* `training data`- what we feed to the model so that it can develop and learn. It is usually a much larger size than the testing data
* `testing data`- seperate set of data to evaulate the model, and see how well it is performing
 
### learning
* `supervised` - tweaks algorithms with entered data
* `unsupervised` - don't have labels, algorithm figures it out
* `reinforcement` - train model through rewards in uncertain environment

### tensor basics
* `rank / degree` - number of dimentions involved in the tensor
  * `tf.rank(tf.Variable())` to get the rank
  * rank 0 (scalor) - `tf.Variable("something", tf.string)`
  * rank 1 - `tf.Variable(["something", "another"], tf.string)`
  * rak 2 - `tf.Variable([["something", "another"], ["one", "two"]], tf.string)`

* `shape` - the amount of elements in each dimention
  * `tf.Variable().shape`
  * `TensorShape[2,3]` - `tf.Variable([["something", "another", "anything"], ["one", "two", "three"]], tf.string)`
  * `reshape` - modify the shape of the tensor
    * number of elements in a tensor is the product of the sizes of all its shapes

## algorithms

### useful libraries
* `tensorflow as tf`
* `matplotlib.pyplot as plt`
* `numpy as np`
* `pandas as pd`
* `sklearn`

### feature columns
* list of categorical and numeric data points
* create object that our model can use to map categorical data points (strings) to integer values

### training process
* stream batch of 32
* `epochs` - number of times we send the same data batch to the model

### input function
* convert `pandas` dataframe into `tf.data.Dataset` object that is required for `tensorflow` to make a model

### linear regression
* regression is used to predict a numeric value
* `y = mx + b`
  * (x, y) - data point
  * m = slope
  * b = y value when x=0

### classification
* used to separate data points into classes of different labels

### clustering
* unsupervised
* grouping of data points based on similar properties and features
* **K-Means**
  1. randomly place `K` centroid points
  1. assign all data points to a centoid based on closest distance
  1. find the center of all data point belonging to a centroid (center of mass), and re-draw the centroid
  1. reassign every point to the closest centroid
  1. repeat 3-4 until no point changes centroid
* **Hidden Markov Model**
  * a finite set of states, each of which is associated with a (generally multidimensional) probability distribution []. Transitions among the states are governed by a set of probabilities called transition probabilities
  * works with probabilities to predict future events or states
  * `states`
    * finite set of states
      *"warm" and "cold"
      * "high" and "low"
      * "red", "green" and "blue"
    * "hidden" within the model, which means we do not direcly observe them
  * `observations`
    * each state has a particular outcome or observation associated with it based on a probability distribution
      * on a hot day Tim has a 80% chance of being happy and a 20% chance of being sad
  * `transitions`
    * each state has a probability of transitioning to a different state
      * a cold day has a 30% chance of being followed by a hot day and a 70% chance of being follwed by another cold day

## Nueral Network
