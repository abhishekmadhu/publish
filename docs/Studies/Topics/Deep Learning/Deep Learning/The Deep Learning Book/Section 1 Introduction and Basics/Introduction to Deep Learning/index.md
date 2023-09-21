---
share: "true"
---

# Introduction to Deep Learning

Just a fancy name for Artificial Neural Networks with many Layers

# Questions related to this chapter

- How does deep learning differ from machine learning?

    Deep learning is a subset of machine learning, where we do not need to hand-craft the features of the dataset. Instead, the model "learns" to identify those complex intrinsic features of its own from the dataset.

- What does the word "deep" mean in deep learning?

    The word "deep" in deep learning refers to the number of layers in a neural network. The more the number of layers, the "deeper" the learning model is.

- Why do we use activation functions?

    We use activation functions to introduce non-linearity in the neural networks. Otherwise, the equation of a perceptron $z = (weights * inputs) + bias$ is essentially same as linear regression. Making $output = f(z)$  introduces much needed non-linearity in the equations so that the model can actually learn non-linear patterns in the data. (data is not always linearly separable/classifiable/predictable)

- Explain dying ReLU problem.

    When the input is negative, the ReLU function gives 0 as the output. If most of the inputs are negative, the neuron has the output 0 most of the time. A neuron that outputs 0 all the time is called a dead neuron. A neuron that increasingly has output as 0, is called a dying ReLU. This is a problem because this neuron does not contribute much to the learning process anymore.

    This is caused by

    1. High learning rate
    2. Large negative bias

    This can be avoided by:

    1. Smaller learning rate
    2. Variations of ReLU like Leaky ReLU
    3. Weight initialisation techniques like Randomised Asymmetric Initialisation

    [Dying ReLU and Initialization: Theory and Numerical Examples](https://arxiv.org/abs/1903.06733)

- Define forward propagation.

    Forward propagation is the process of taking a set of inputs and predicting the output based on the current biases and weights in a neural network. The outputs from the previous layers act as the input to the next layers.

- What is back propagation?

    Back-propagation is a widely used algorithm for training feed forward networks. After the forward pass, the errors in the predictions are calculated using the cost function, and the weights are changed accordingly in each of the layers from the output towards the input layers to minimise the cost/error in prediction by calculating the gradient of the cost function with respect to the weights in the layer. This algorithm is known as back propagation.

- Explain gradient checking.

    Gradient checking is used to validate implementations of gradient descent algorithm by comparing **numerical** (the numerical approximation of gradients) and **analytical** (the ones given by the implementation of the algorithm) gradients.

    [[../../../../../../../Untitled.png|Untitled]]




# Study Notes

## Activation Functions

### Sigmoid

### tanh

### ReLu

### Exponential Linear Unit (ELU)

### Swish

### Softmax

## Forward Propagation in ANN

The process of propagating from the input layer to the output layer is called forward propagation.

The outputs of each neuron is calculated in each layer, and then those outputs are fed/assumed as inputs of the next layer, and the outputs of those layers are calaulated again.

The network does not learn anything during this step. It just tries to predict an output based on the current inputs, weights and bias elements present in the network.

### Backward propagation

The whole process of backpropagating the network from the output layer to the input layer and updating the weights of the network using gradient descent to minimize the loss is called backpropagation.

We use the following rule to update our weights:

$$
weights=weights - \alpha * \frac{\delta J}{\delta W}
$$

Here, alpha is the “learning rate”, that denotes how fast the neural network will learn stuff.

Calculus steps:

1. Cost function, $J = \frac{1}{n}\sum_{i=1}^{n}({y_i - \hat{y_i}})^2$
2. the cost function cannot directly help us in calculating the derivative as there is no $W_{hy}$ term
3. From the forward propagation equation, we get  $\hat{y} = \sigma(z_2)$
4. We also know, from forward propagation that  $z_2 = a_1 W_{hy} + b_y$
5. Using chain rule, we get:

$$
\frac{\delta J}{\delta{W_{hy}}} = \frac{\delta J}{\delta \hat{y}} * \frac{\delta \hat y}{\delta z_2} * \frac{d z_2}{d W_{hy}}
$$

6. Clearly, $\frac{\delta J} {\delta\hat y} = (y - \hat y)$ and $\frac{\delta \hat y}{\delta z_2} = \sigma'(z_2)$   (from #3)
...where $\sigma'$ is the derivative of our sigmoid activation function

7. Therefore, we can write the derivative as
$\sigma'(z) = \frac {e^{-z}}{(1 + e^{-z})^2}$

8. let us assume $\frac{d z_2}{d W_{hy}} = a_1$

9. Therefore, our chain equation (from #5) becomes:

$$
\frac{\delta J}{\delta{W_{hy}}} = (y-\hat y)\space.\space \sigma'(z_2) \space.\space a_1
$$

10. Similarly, for the next layer, we can calculate the weights as:

$$
\frac{\delta J}{\delta w_{xh}} = (y-\hat y) \space.\space \sigma'(z_2) \space.\space W_{hy} \space.\space \sigma'(z_1) \space.\space x
$$

### Building a Neural Network from scratch

This is in a ipynb in .dev@gmail account. Add notes form there.
