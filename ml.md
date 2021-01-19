# Machine learning

* finds rules based on data
* AI > ML > NN

* feature - input data, what we feed to the label to get the output
* label - output data, what we are looking for
* feature --> label

* supervised - tweaks algorithms with entered data
* unsupervised - don't have labels, algorithm figures it out
* reinforcement - train model through rewards in uncertain environment

* Scalor (rank 0 representation) - one dimentional value

* rank / degree - number of dimentions involved in the tensor
  * `tf.rank(tf.Variable())` to get the rank
  * rank 0 - `tf.Variable("something", tf.string)`
  * rank 1 - `tf.Variable(["something", "another"], tf.string)`
  * rak 2 - `tf.Variable([["something", "another"], ["one", "two"]], tf.string)`

* shape - the amount of elements in each dimention
  * `tf.Variable().shape`
  * `TensorShape[2,3]` - `tf.Variable([["something", "another", "anything"], ["one", "two", "three"]], tf.string)`

* reshape - modify the shape of the tensor
  * number of elements in a tensor is the product of the sizes of all its shapes