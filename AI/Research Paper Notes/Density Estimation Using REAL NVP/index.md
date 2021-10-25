# Density Estimation Using REAL NVP
1. [Model Definition](./Model%20Definition/index.md)
2. [Experiments](./Experiments/index.md)

## References
* [Paper](https://arxiv.org/pdf/1605.08803.pdf)

## Abstract
Unsupervised learning of probabilistic models is a central yet challenging problem
in machine learning. 
  -  Designing models with tractable learning, sampling, inference and evaluation is crucial.

## Introduction
wever, metrics that measure the
diversity in the generated samples are currently intractable 
Data of interest are generally high-dimensional and highly structured, the challenge in this domain is building models that are powerful enough to capture its complexity yet still trainable.

We address this challenge by introducing **real-valued non-volume preserving (real NVP) transformations**.

The architecture presented in this paper enables exact and efficient reconstruction of input images from the hierarchical features extracted by this model.

## Related work
**Probabilistic Undirected Graphs**
  - Restricted Boltzmann Machines
  - Deep Boltzmann Machines
  - Because of the intractability of the associated marginal distribution over latent variables, their training, evaluation, and sampling procedures necessitate the use of approximations:
    - Mean Field inference 
    - Markov Chain Monte Carlo

**Autoregressive models**
  - This class of algorithms tractably models the joint distribution by decomposing it into a product of conditionals using the probability chain rule according to a fixed ordering over dimensions, simplifying log-likelihood evaluation and sampling.
  -  The sequential nature of this model limits its computational efficiency.
  -  Additionally, there is no natural latent representation associated with autoregressive models.

**Generative Adversarial Networks (GANs)**
  - Can train any differentiable generative network by avoiding the maximum likelihood principle altogether.
  -  Instead, the generative network is associated with a discriminator network whose task is to distinguish between samples and real data.
  -  Successfully trained GAN models can consistently generate sharp and realistically looking samples.
  - However, metrics that measure the diversity in the generated samples are currently intractable 
  - Additionally, instability in their training process requires careful hyperparameter tuning to avoid diverging behavior.
