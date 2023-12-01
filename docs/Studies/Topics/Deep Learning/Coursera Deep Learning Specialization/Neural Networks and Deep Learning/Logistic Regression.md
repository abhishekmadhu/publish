---
share: "true"
---


Solves $\text{given x, we want } \hat{y}$ problems. 

We make the result (`y`) boolean (yes/no, or 1 or 0), and then see if the model can learn the cases where `y == 1`. In other words: 

$\hat{y} = P(y=1|x)$ where $\hat{y}$ is the probability that y = 1 given feature vector x. 
where $x \in \mathbb{R}^{n_{x}}$

Parameters $w \in \mathbb{R}^{n_{x}}, b \in \mathbb{R}$ - w in an nx dimentional vector in real numbers. 

Output for linear regression: $\hat{y} = w^{T_{x}} + b$
Logistic Regression - 
Predicted class, $\hat{y} = \sigma({w^{T_{x}} + b})$

![[Logistic Regression 2023-12-01 16.16.33.excalidraw|Logistic Regression 2023-12-01 16.16.33.excalidraw]]
Here, we use the sigmoid function - $\sigma$
$$
\sigma(z) = \frac{1}{1 + e^{-z}}
$$$\text{If z is large, then } e^{- \infty} \approx 0$
In that case, 
$$\sigma(z) \approx \frac{1}{1+0} = 1$$
Also, if Z is large negative number, then $e^{-(- \infty)} = e^\infty = \infty$ which makes the result $0$: 
$$\sigma(z) \approx \frac{1}{1+ \infty} = 0$$
---

So, we have established that we need to work with $\hat{y} = \sigma({w^{T_{x}} + b})$ where $\sigma(z) = \frac{1}{1 + e^{-z}}$

$\text{Given }({x_{1}, y_{1}), (x_{2}, y_{2}, \dots, (x_{3}, y_{3}))}$, we want $\hat{y}_{i} \approx y_{i}$ (predicted result $\hat{y}$ of $i^{th}$ instance as close as possible to actual result $y$ of the $i^{th}$ instance)  - and we want to learn the right values of w and b so that $\hat{y}$ predictions follow this requirement. 

>[!warning] [[Loss Function|Loss Function]] - We need to define a loss function that is convergent. 

We will use something similar to squared error function to define how we are doing with one training example, 
$L(\hat{y}, y) = (y \log{ \hat{y}} + (1-y) \log{(1-\hat{y})}$

Intuition: 
If y = 1, $L = -\log \hat{y}$
If y = 0, $L = -\log(1-\hat{y})$

For this, we want to have $y \in [0,1]$ as the loss function "pushes" the result towards 1 and 0 based on the actual expected value of y. 

[[Cost Function|Cost Function]] - for entire training sample. 
$$J(w,b) = \frac{1}{m} \sum_{i=1}^{m}{L(\hat{y}_{i}, y_{i})}$$
$$= -\frac{1}{m} \sum_{i=1}^{m} [y_{i} \log{\hat{y}_{i}} + (1-\hat{y}_{i} \log{(1-\hat{y}_{i})})]$$
We will try to minimize the cost. 

