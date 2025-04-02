# Gaussian_Process_Regression

![image](https://github.com/user-attachments/assets/ed1ec577-7085-4695-857c-14b2bbacfd41)

Gaussian Process Regression (GPR) is a non-parametric Bayesian approach to regression that provides probabilistic predictions with uncertainty estimates. A Gaussian Process (GP) is a collection of random variables, any finite number of which have a joint Gaussian distribution. GPR uses this property to model a distribution over functions.

A GP is defined as:

\begin{equation}
f(x) \sim GP(m(x), k(x, x'))
\end{equation}

where:

 is the mean function, often taken as zero: .

 is the covariance function (kernel) that defines similarity between points.
