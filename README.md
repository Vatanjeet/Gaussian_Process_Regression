# Gaussian_Process_Regression

![image](https://github.com/user-attachments/assets/ed1ec577-7085-4695-857c-14b2bbacfd41)

\documentclass{article}
\usepackage{amsmath, amssymb, amsthm, graphicx}
\usepackage{hyperref}
\usepackage{geometry}
\geometry{a4paper, margin=1in}

\title{Gaussian Process Regression (GPR)}
\author{}
\date{}

\begin{document}

\maketitle

\section{Introduction}
Gaussian Process Regression (GPR) is a non-parametric Bayesian approach to regression that provides probabilistic predictions with uncertainty estimates. A Gaussian Process (GP) is a collection of random variables, any finite number of which have a joint Gaussian distribution. GPR uses this property to model a distribution over functions.

A GP is defined as:

\begin{equation}
f(x) \sim GP(m(x), k(x, x'))
\end{equation}

where:

 is the mean function, often taken as zero: .

 is the covariance function (kernel) that defines similarity between points.

\section{Prior Distribution}
Before observing any data, we assume a prior distribution over function values:

\begin{equation}
\mathbf{f} \sim \mathcal{N}(\mathbf{0}, \mathbf{K})
\end{equation}

where  is the kernel matrix with entries .

\section{Likelihood Function}
Given a dataset , we assume:

\begin{equation}
y_i = f(x_i) + \epsilon, \quad \epsilon \sim \mathcal{N}(0, \sigma_n^2)
\end{equation}

where  is Gaussian noise. The likelihood function is:

\begin{equation}
p(\mathbf{y} | \mathbf{X}, \mathbf{f}) = \mathcal{N}(\mathbf{f}, \sigma_n^2 \mathbf{I})
\end{equation}

\section{Posterior Distribution}
For a test input , the joint prior distribution of training outputs  and the test output  is:

\begin{equation}
\begin{bmatrix} \mathbf{y} \ f_* \end{bmatrix} \sim \mathcal{N} \left( \mathbf{0}, \begin{bmatrix} \mathbf{K} + \sigma_n^2 \mathbf{I} & \mathbf{k}* \ \mathbf{k}*^\top & k_{**} \end{bmatrix} \right)
\end{equation}

where:

 is the covariance between training inputs and the test point.

 is the self-covariance of the test point.

Using properties of multivariate Gaussians, the posterior mean and variance of  are:

\begin{equation}
\mathbb{E}[f_] = \mathbf{k}_^\top (\mathbf{K} + \sigma_n^2 \mathbf{I})^{-1} \mathbf{y}
\end{equation}

\begin{equation}
\text{Var}[f_] = k_{**} - \mathbf{k}_^\top (\mathbf{K} + \sigma_n^2 \mathbf{I})^{-1} \mathbf{k}_*
\end{equation}

Thus, the predictive distribution is:

\begin{equation}
p(f_* | x_, \mathcal{D}) = \mathcal{N}(\mathbb{E}[f_], \text{Var}[f_*])
\end{equation}

\section{Kernel Functions}
The kernel function  defines the similarity between points. Some common choices:

\subsection{Radial Basis Function (RBF) Kernel}
\begin{equation}
k(x, x') = \sigma_f^2 \exp \left(-\frac{|x - x'|^2}{2\ell^2} \right)
\end{equation}

\subsection{Matern Kernel}
\begin{equation}
k(x, x') = \sigma_f^2 \frac{2^{1-\nu}}{\Gamma(\nu)} \left(\frac{\sqrt{2\nu} |x - x'|}{\ell} \right)^\nu K_\nu \left(\frac{\sqrt{2\nu} |x - x'|}{\ell} \right)
\end{equation}

\subsection{Periodic Kernel}
\begin{equation}
k(x, x') = \sigma_f^2 \exp \left(-\frac{2 \sin^2(\pi |x - x'| / p)}{\ell^2} \right)
\end{equation}
