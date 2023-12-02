---
share: "true"
---

Objective: Learn how to build a basic neural network by building a cat recognizer.

**Structure**
1. Week 1 - Introduction
2. Week 2 - Basics of NN + Exercise 
3. Week 3 - One Hidden layer network code 
4. Week 4 - Deep Neural Network 

What is a [[Neural Network|Neural Network]]? 
A trainable system that takes an input and provides an output based on previously trained data. 

Each unit is called a [[neuron|neuron]].

Neurons are arranged in layers. 

[[Dense layer|Dense layer]] - All input features are connected to all nodes in that layer. 
[[Densely connected layers|Densely connected layers]] - When the outputs of layer1 are connected to all nodes of layer2, we call that layer2 is connected densely with layer1. 

### Supervised Learning with Neural Networks
[[Supervised Learning|Supervised Learning]] - A type of learning where we have an input x and we learn to predict the output y. 

> Example: Housing Prices, Online Advertising, Photo Tagging (CNNs), Speech Recognition (RNN), Machine Translation (RNN), Autonomous Driving (Image + Radar Info)(Custom Architectures)

Clever selection of `x` and `y` is really important. 

Structured data - Data in tabular format, with columns being each feature. 
Unstructured data - Non-tabular data, like Images, Raw Audio 

In general, machines are better with structured data. Humans are better with unstructured data. Deep Learning starts to level the playing field. 

Throwing more data at a neural network generally helps, until you run out of data. 
Making the network larger generally helps, until you run out of space/time-to-train. 

**Notations for the course:** 
- m - size of data
[[Gradient Descent|Gradient Descent]] work much faster with [[ReLU - Rectified Linear Unit|ReLU - Rectified Linear Unit]] compared to [[Sigmoid Activation Function|Sigmoid Activation Function]]. 

What are [[Boltzmann Machines|Boltzmann Machines]]? It was mentioned by [[Geoffrey Hinton|Geoffrey Hinton]] in the interview. 
What is [[Bayesian Learning|Bayesian Learning]]? 

---

[[Forward Propagation|Forward Propagation]] and [[Backward Propagation|Backward Propagation]] are two steps.  

[[./Logistic Regression|Logistic Regression]] - solves binary classification. 
[[Feature Vector|Feature Vector]] 

If the input feature matrix is a set of columns instead of a row, it becomes much easier to pass them through neural networks. (why?). This is why Andrew Ng uses columns instead of rows (which some others prefer). $m = \text{number of training examples}$ 
$X \in \mathbb{R}^{n \times m}$
$X.shape = (n, m)$
$Y = [y^1, y^2, y^3, \dots, y^m]$
$Y \in \mathbb{R}^{1 \times m}$
$Y.shape = (1,m)$



Terms learnt (to be used later):
[[ReLU - Rectified Linear Unit|ReLU - Rectified Linear Unit]]