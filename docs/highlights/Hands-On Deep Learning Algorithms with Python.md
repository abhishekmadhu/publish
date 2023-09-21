---
kindle-sync:
  bookId: "47660"
  title: "Hands-On Deep Learning Algorithms with Python: Master deep learning algorithms with extensive math by implementing them using TensorFlow"
  author: Sudharsan Ravichandiran
  asin: B07LH43V8P
  lastAnnotatedDate: 2021-05-26
  bookImageUrl: https://m.media-amazon.com/images/I/810ZDKiQtsL._SY160.jpg
  highlightsCount: 20
type: bookHighlight
startDate: 2022
endDate: 
share: "true"
---
# Hands-On Deep Learning Algorithms with Python
## Metadata
* Author: [Sudharsan Ravichandiran](https://www.amazon.com/Sudharsan-Ravichandiran/e/B07F1PBWJH/ref=dp_byline_cont_ebooks_1)
* ASIN: B07LH43V8P
* Reference: https://www.amazon.com/dp/B07LH43V8P
* [Kindle link](kindle://book?action=open&asin=B07LH43V8P)

## Highlights
what is the difference between neurons and linear regression? In neurons, we introduce non-linearity to the result, , by applying a function called the activation or transfer function. — location: [604](kindle://book?action=open&asin=B07LH43V8P&location=604) ^ref-23412

---
The number of neurons in the output layer is based on the type of problem we want our network to solve. If it is a binary classification, then the number of neurons in the output layer is one that tells us which class the input belongs to. If it is a multi-class classification say, with five classes, and if we want to get the probability of each class as an output, then the number of neurons in the output layer is five, each emitting the probability. If it is a regression problem, then we have one neuron in the output layer. — location: [631](kindle://book?action=open&asin=B07LH43V8P&location=631) ^ref-44958

---
If we do not apply the activation function, then a neuron simply resembles the linear regression. — location: [639](kindle://book?action=open&asin=B07LH43V8P&location=639) ^ref-39984

This is because the activation function introduces the non linearity in the mechanism

---
Leaky ReLU is a variant of the ReLU function that solves the dying ReLU problem. Instead of converting every negative input to zero, it has a small slope for a negative value — location: [670](kindle://book?action=open&asin=B07LH43V8P&location=670) ^ref-40475

---
We can also set the value of to some random value and it is called as Randomized ReLU function. — location: [678](kindle://book?action=open&asin=B07LH43V8P&location=678) ^ref-24689

We can also set the value of alpha to some random value, and it is called as Rnadomized ReLU function.

---
Swish is a non-monotonic function, which means it is neither always non-increasing nor non-decreasing. It provides better performance than ReLU. It is simple and can be expressed as follows: Here, is the sigmoid function. The Swish function is shown in the following diagram: — location: [689](kindle://book?action=open&asin=B07LH43V8P&location=689) ^ref-52610

Check the function images in the Kindle book

---
The softmax function is basically the generalization of the sigmoid function. It is usually applied to the final layer of the network and while performing multi-class classification tasks. It gives the probabilities of each class for being output and thus, the sum of softmax values will always equal 1. — location: [700](kindle://book?action=open&asin=B07LH43V8P&location=700) ^ref-37759

---
The dimensions of the weight matrix must be number of neurons in the current layer x number of neurons in the next layer. Why is that? Because it is a basic matrix multiplication rule. To multiply any two matrices, AB, the number of columns in matrix A must be equal to the number of rows in matrix B. So, the dimension of the weight matrix, , should be number of neurons in the input layer x number of neurons in the hidden layer, — location: [720](kindle://book?action=open&asin=B07LH43V8P&location=720) ^ref-8322

---
Gradient descent is a first-order optimization algorithm, which means we only take into account the first derivative when performing the updates: — location: [778](kindle://book?action=open&asin=B07LH43V8P&location=778) ^ref-53691

---
This whole process of backpropagating the network from the output layer to the input layer and updating the weights of the network using gradient descent to minimize the loss is called backpropagation. — location: [788](kindle://book?action=open&asin=B07LH43V8P&location=788) ^ref-28594

---
Before moving on, let's familiarize ourselves with some of the frequently used terminologies in neural networks: Forward pass: Forward pass implies forward propagating from the input layer to the output layer. Backward pass: Backward pass implies backpropagating from the output layer to the input layer. Epoch: The epoch specifies the number of times the neural network sees our whole training data. So, we can say one epoch is equal to one forward pass and one backward pass for all training samples. Batch size: The batch size specifies the number of training samples we use in one forward pass and one backward pass. Number of iterations: The number of iterations implies the number of passes where one pass = one forward pass + one backward pass. — location: [844](kindle://book?action=open&asin=B07LH43V8P&location=844) ^ref-61469

---
in order to compute anything on TensorFlow, we need to create a TensorFlow session. — location: [1031](kindle://book?action=open&asin=B07LH43V8P&location=1031) ^ref-23301

---
Unlike tf.Variable(), we cannot pass the value directly to tf.get_variable(); instead, we use initializer. — location: [1072](kindle://book?action=open&asin=B07LH43V8P&location=1072) ^ref-38744

---
Variables created using tf.Variable() cannot be shared, and every time we call tf.Variable(), it will create a new variable. But tf.get_variable() checks the computational graph for an existing variable with the specified parameter. If the variable already exists, then it will be reused; otherwise, a new variable will be created: — location: [1077](kindle://book?action=open&asin=B07LH43V8P&location=1077) ^ref-8920

---
In order to visualize in TensorBoard, we first need to save our event files. It can be done using tf.summary.FileWriter(). It takes two important parameters, logdir and graph. — location: [1161](kindle://book?action=open&asin=B07LH43V8P&location=1161) ^ref-4102

---
tensorboard --logdir=graphs --port=8000 — location: [1172](kindle://book?action=open&asin=B07LH43V8P&location=1172) ^ref-25777

---
model.compile(loss='binary_crossentropy', optimizer='sgd', metrics=['accuracy']) — location: [1528](kindle://book?action=open&asin=B07LH43V8P&location=1528) ^ref-8273

---
model.fit(x=data, y=labels, epochs=100, batch_size=10) — location: [1535](kindle://book?action=open&asin=B07LH43V8P&location=1535) ^ref-8981

---
model.evaluate(x=data_test,y=labels_test) — location: [1540](kindle://book?action=open&asin=B07LH43V8P&location=1540) ^ref-60376

---
model.evaluate(x=data,y=labels) — location: [1542](kindle://book?action=open&asin=B07LH43V8P&location=1542) ^ref-55446

---
