## Abstract
**Weight Normalization:** A reparameterization of the weight vectors in a neural network that **decouples the length of those weight vectors from ther direction.**

By reparameterizing the weights in this way we improve the conditioning of the optimization problem and we speed up convergence of stochastic gradient descent.

# Introduction
Recent successes in deep learning have shown that neural networks trained by **first-order gradient based optimization** are capable of achieving amazing results.

However, it is also well known that the practical success of first-order gradient based optimization is highly dependent on the curvature of the objective that is optimized.
  - If the condition number of the Hessian matrix of the objective at the optimum is low, the problem is said to exhibit pathological curvature, and first-order gradient descent will have trouble making progress.

The amount of curvature, and thus the success of our optimization, is not invariant to reparameterization.
  -  There may be multiple equivalent ways of parameterizing the same model, some of which are much easier to optimize than others.
  -  Finding good ways of parameterizing neural networks is thus an important problem in deep learning.

While the architectures of neural networks differ widely across applications, they are typically mostly composed of conceptually simple computational building blocks sometimes called neurons.
  - **Neurons:** Each neuron computes a weighted sum over its inputs and adds a bias term, followed by the application of an elementwise nonlinear transformation. 


Several authors have recently developed methods to improve the conditioning of the cost gradient for general neural network architectures:
  1. One approach is to explicitly left multiply the cost gradient with an approximate inverse of the Fisher information matrix, thereby obtaining an approximately whitened natural gradient. 
  2. Alternatively, we can use standard first order gradient descent without preconditioning, but change the parameterization of our model to give gradients that are more like the whitened natural gradients of these methods. 

Following this second approach to approximate natural gradient optimization, we propose a simple but general method, called **weight normalization**, for improving the optimizability of the weights of neural network models. 
