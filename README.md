# Gaussian_Process_Regression

![image](https://github.com/user-attachments/assets/ed1ec577-7085-4695-857c-14b2bbacfd41)
## GPR Overview
A Gaussian Process models a function f(x) with a mean function m(x) and a covariance (kernel) function k(x, x'). Typically:
- m(x) = 0 (if no prior info),
- k(x, x') defines how similar x and x' are.

## Training Data
Given inputs X = {x1, x2, ..., xn} and outputs y = {y1, y2, ..., yn}, with noise ε ~ N(0, σ_n^2):
- y = f(X) + ε

## Prediction
For a new point x*, the prediction f* follows a Gaussian distribution with:
- Mean: μ*
- Variance: σ*^2

### Predictive Mean
μ* = K(x*, X) * [K(X, X) + σ_n^2 * I]^(-1) * y
- K(x*, X): covariance between x* and training points X,
- K(X, X): covariance matrix of training points,
- σ_n^2: noise variance,
- I: identity matrix.

### Predictive Variance
σ*^2 = k(x*, x*) - K(x*, X) * [K(X, X) + σ_n^2 * I]^(-1) * K(X, x*)
- k(x*, x*): covariance of x* with itself.

## Common Kernel
The RBF kernel is often used:
k(x, x') = σ_f^2 * exp(-||x - x'||^2 / (2 * ℓ^2))
- σ_f^2: signal variance,
- ℓ: length scale.
