## Procedure
The algorithm learn distributions on unbounded space.

But, in general, the data of interest have bounded magnitude. 
  - For examples, the pixel values of an image typically lie in [0, 256] after application of the recommended **jittering procedure**.

In order to reduce the impact of boundary effects, we instead model the density of logit (alpha + (1-alpha)*(x/256)), where alpha is picked here as 0.05.

We use the **multi-scale architecture** and use **deep convolutional residual networks** in the coupling layers with **rectifier nonlinearity** and **skip-connections**.

To compute:
  1. **Scaling functions s:** We use a hyperbolic tangent function multiplied by a learned scale.
  2. **Translation function t:** Affine output.

We set the prior p_Z to be an isotropic unit norm Gaussian.

## Results
The number of bits per dimension, while not improving over the Pixel RNN baseline, is competitive with other generative methods.

Maximum likelihood is a principle that values diversity over sample quality in a limited capacity setting.

## Discussion and conclusion
In this paper, we have defined a **class of invertible functions** with **tractable Jacobian determinant**, **enabling exact and tractable log-likelihood evaluation**, **inference**, and **sampling**.

Future Improvement: Exploiting the latest advances in **dilated convolutions** and **residual networks architectures**.

The definition of powerful and trainable invertible functions can also benefit domain other than generative unsupervised learning.

