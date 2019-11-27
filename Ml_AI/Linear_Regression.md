# Linear Regression

#### Line Equation

$$
y = mx + b
$$

An output $y$ can be represented by the sum of a starting point $b$ plus a change $m$ for every step in $x$

#### Key Assumption

A linear correlation exists such that a response can be assumed to be proportional to some change in $x$ 

#### Goal

Derive the equation $y = mx + b$ by choosing a $m$ and a $b$ such that the Mean Squared Error is minimized

Consider the graphical representation of error. A pink point represents a real observation and the blue line represents the prediction using $y = mx + b$. The red line represents the offset.

![Least Squares Error](https://cdn-media-1.freecodecamp.org/images/MNskFmGPKuQfMLdmpkT-X7-8w2cJXulP3683)

We can represent the mean squared error as:
$$
MSE = \frac {\sum_{i=0}^N{(y_i - (mx_i+b))^2}} {N}
$$
Where $N$ is the number of observations (pink dots) and $y_i$ is an observation $i$ for an input $x_i$

We want to minimize MSE and can do so by taking 2 derivatives, one derivative as a function of $m$ and another as a function of b
$$
MSE'=
\begin{vmatrix}
	\frac{\partial f}{\partial m}\\
	\frac{\partial f}{\partial b}
\end{vmatrix} =
\begin{vmatrix}
	\frac{1}{N}\sum_{i=0}^N-2x_i(y_i-(mx_i+b))\\
	\frac{1}{N}\sum_{i=0}^N-2(y_i-(mx_i+b))
\end{vmatrix}
$$

#### Computational approach to minimizing via Gradient Descent

$$
\begin{vmatrix}
	m \\
	b
\end{vmatrix} :=
\begin{vmatrix}
	m - \frac{2\alpha}{N}\sum_{i=0}^Nx_i(y_i-(mx_i+b))\\
	b - \frac{2\alpha}{N}\sum_{i=0}^N(y_i-(mx_i+b))
\end{vmatrix}
$$

reassign $m$ and $b$ to the difference between the previous value for $m$ and $b$ and the average error calculated using the previous $m$ and $b$ in the equation $y = mx + b$ times a learning rate $\alpha$. Then using the new $m$ and $b$ calculate $MSE$ to see if it is within an acceptable error range

```python
# X_observed from some data
# Y_observed from some data
# n from some data
m = 0 # guess
b = 0 # guess
alpha = 0.001 # guess
acceptable_error = 0.001 # arbitrary
error = 1 # arbitrary
while True:
  Y_pred = m * X_observed + b
  D_m = ((-2 * alpha)/n) * sum(X_observed * (Y_observed - Y_pred))
  D_b = ((-2 * alpha)/n) * sum(Y_observed - Y_pred)
  m = m - D_m
  b = b - D_b
  error = (1/n) * sum((Y_observed - Y_pred)**2)
  if( error < acceptable_error ):
    break
```

