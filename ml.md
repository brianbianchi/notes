# Machine learning
* [TensorFlow](https://www.tensorflow.org/)
* [cheat sheet](https://ml-cheatsheet.readthedocs.io/en/latest/)
* finds rules based on data
* AI > ML > NN

## [basics](https://colab.research.google.com/drive/1F_EWVKa8rbMXi3_fG0w7AtcscFq7Hi7B#forceEdit=true&sandboxMode=true)
* `feature` - input data, what we feed the model to get an output
* `label` - output data, what we are looking for
* `feature` --> `label`
* `training data`- what we feed to the model so that it can develop and learn. It is usually a much larger size than the testing data
* `testing data`- seperate set of data to evaulate the model, and see how well it is performing
 
## [learning](https://colab.research.google.com/drive/15Cyy2H7nT40sGR7TBN5wBvgTd57mVKay#forceEdit=true&sandboxMode=true)
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

## [Nueral Networks](https://colab.research.google.com/drive/1m2cg3D1x3j5vrFc-Cu0gMvc48gWyCOuG#forceEdit=true&sandboxMode=true)
* ![](img/nn_equation.png)
* summation of neuron value multiplied by weight, added to the bias
* [TensorFlow tutorial](https://www.tensorflow.org/tutorials/keras/classification)

### data
* Vector Data (2D)
* Timeseries or Sequence (3D)
* Image Data (4D)
* Video Data (5D)

### layers
* `input` - first layer, initial data is passed to
* `hidden`
  * in between layers, can be unlimited in amount
  * not observed
* `output` - last layer, retrive our results from

### neurons
* each layer is made up of `neurons`
* several properties, but responsible for generating/holding/passing one numeric value
* `dense layer` - when each neuron in one layer is connected to every neuron in the next layer

### weights
* `neurons` of one layer are connected to the next through numeric values named `weights`
* associated with each connection in our neural network. Every pair of connected nodes will have one weight that denotes the strength of the connection between them
* value is tweaked as the neural network is trained
* model will try to determine what these weights should be to achieve the best result
* start out at a constant or random value, and will change as the network sees training data

### biases
* one constant value associated with each layer, extra neuron with no connections
* shifts an entire activation function by a constant value
* value is tweaked as the neural network is trained

### activation functions
* a function that is applied to the weighed sum of a neuron
* higher order/degree functions that aim to add a higher dimension to our data to make better predictions
* examples
  * rectifized linar unit (`Relu`) - any negative numbers -> 0
  * hyperbolic tangent (`Tanh`) - more negative, closer to -1, more positive, closer to 1
  * Sigmoid - more negative, closer to 0, more positive, closer to 1

### backpropagation
* fundemental algorithm behind training neural networks, changing the `weights` and `biases` of our network

### loss/cost function
* a way of evaluating how well the network is doing
* based on our training data, we can compare the output from our network to the expected output
* based on the result, we will make changes to the weights and biases
* if predictions deviates too much from actual results, loss function returnas larger value
* examples
  * `Mean Squared Error`
  * `Mean Absolute Error`
  * `Hinge Loss`

### gradient descent
* "Gradient descent is an optimization algorithm used to minimize some function by iteratively moving in the direction of steepest descent as defined by the negative of the gradient. In machine learning, we use gradient descent to update the parameters of our model."
* algorithm used to find the optimal paramaters (`weights` and `biases`) for our network, while `backpropagation` is the process of calculating the gradient that is used in the gradient descent step

### [optimizer / optimization functions](https://medium.com/@sdoshi579/optimizers-for-training-neural-network-59450d71caf6) 
* function that implements the backpropagation algorithm described above
* examples
  * Gradient Descent
  * Stochastic Gradient Descent
  * Mini-Batch Gradient Descent
  * Momentum
  * Nesterov Accelerated Gradient

## [Deep computer vision](https://colab.research.google.com/drive/1ZZXnCjFEOkp_KdNcNabd14yok0BAIuwS#forceEdit=true&sandboxMode=true)

### image data
* 3 dimentional
  * image width
  * image height
  * color channels (3, rgb)

### Convolutional neural network
* `dense layer` - entire image
* `convolutional layer` - specific parts of an image where patterns exist
  * layers work together by increasing complexity and abstraction at each subsequent layer
  * feature map -> response map
  * first layer might be responsible for picking up edges and short lines
  * second layer might take as input these lines and start forming shapes or polygons
  * last layer might take these shapes and determine which combiantions make up a specific image
* `feature map`
  * 3 dimentional tensor with 2 spacial axes (width, height, depth)
* `response map`
  * feature map with pattern filters
* convolutional layer `parameters`
  * filters - m x n pattern of pixels we are looking for in an image
  * sample size - size of a filter
* `padding` - the addition of the appropriate number of rows and/or columns to your input data such that each pixel can be centered by the filter
* `strides` - how many rows/cols we will move the filter each time
* `pooling`
  * downsample our feature maps and reduce their dimensions
  * extract windows from the feature map and return a response map of the max, min or average values of each channel
  * usually done using windows of size 2x2 and a stride of 2
  * reduce the size of the feature map by a factor of two and return a response map that is 2x smaller



## [Natural language processing(NLP)](https://colab.research.google.com/drive/1ysEKrw_LE2jMndo1snrZUh5w87LQsCxk#forceEdit=true&sandboxMode=true)
* `recurrent neural network (RNN)` - processing sequential data like text or characters
  * `sentiment analysis`
  * `character generation`
* `feed-forward neural network` - data is fed forwards, all at once, from left to right

### encoding 
* ML models only take numeric inputs, so text needs to be encoded
* order of words is an important property of textual data
* `bag of words`
  * each word is encoded as an integer
  * tracks frequency but not order
* `integer encoding`
  * each word or character is encoded as a unique integer
  * maintains order
* `word embeddings`
  * keeps order and encodes similar words with similar labels
  * encodes frequency, order, and meaning
  * encodes each word as a dense vector that represents context
  * add embedding layer to the beggining of your model and while your model trains your embedding layer will learn the correct embeddings for words

### recurrent neural network (RNN)
* `simple RNN layer`
  * processes words or input one at a time in a combination with the output from the previous iteration
  * only effective at processing shorter sequences of text
* `long short-term memory (LSTM)`
  * simpleRNN + can access inputs from any timestep in the past

## [Reinforcement learning](https://colab.research.google.com/drive/1IlrlS3bB8t1Gd5Pogol4MIwUxlAjhWOQ#forceEdit=true&sandboxMode=true)
* rather than feeding our machine learning model millions of examples, we let our model come up with its own examples by exploring an enviornemt
  * learning by exploring, from mistakes and past experiences
* `environment` - what the agent will explore
* `agent` - entity that is exploring the environment
* `state` - status of an agent
* `action` - interaction between agent and environment
* `reward`
  * every action of the agent will result in a reward of some magnitude (positive or negative)
  * goal of agent is to maximize its reward in an environment
  * most important part of RL is determining how to reward agent

### Q-Learning
* based on a matrix of action-reward values (aka `Q-table` or `Q-matrix`)
* matrix is in a shape (num possible states, num possible actions) where each value at matrix [n,m] represents the agents expected reward given they are in state n and take action m
* Q-learning algorithm defines the way we update the values in the matrix and decide what action to take at each state
* after a succesful training/learning of this Q-Table/matrix we can determine the action an agent should take in any state by looking at that states row in the matrix and taking the maximium value column as the action
* `learning rate`
  * how much change is permitted on each QTable update
  * modifying the learning rate will change how the agent explores the enviornment and how quickly it determines the final values in the QTable
* `discount factor`
  * balance how much focus is put on the current and future reward