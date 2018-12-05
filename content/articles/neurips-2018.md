----
title: NeurIPS 2018 stuff
slug: neurips-2018
date: 2018-12-04
----

## Pre-notes

Looking through the schedule, here are some things that I thought looked
interesting. It's definitely not a comprehensive list, nor related to what a
typical ML researcher might consider notable, also I don't really know what I'm
talking about so take my editorial descriptions with a grain of salt.

[Glow: Generative Flow with Invertible 1x1 Convolutions](https://nips.cc/Conferences/2018/Schedule?showEvent=11968) (Tue 10:45 poster)

* A generative model, comparable to VAEs and GANs. Gains some computational advantages by using invertible layers. [OpenAI blog post](https://blog.openai.com/glow/)

[Neural ODEs](https://nips.cc/Conferences/2018/Schedule?showEvent=12596) (Tue 15:50 Track 2)

* Replace a discrete stack of layers with continuous dynamics. David Duvenaud and students

[Bayesian Nonparametric Spectral Estimation](https://nips.cc/Conferences/2018/Schedule?showEvent=11960) (Tue 16:55 Track 1)

* Fourier analysis through the lens of Gaussian processes.

[Sequential Attend, Infer, Repeat](https://nips.cc/Conferences/2018/Schedule?showEvent=12639) (Wed 10:25 Track 2)

* Generative model for scene understanding, based on VAEs?

[Importance Weighting and Variational Inference](https://nips.cc/Conferences/2018/Schedule?showEvent=11441) (Wed 10:45 poster)

* On some recent importance-weighted VAE work and repurposing it for probabilistic inference only.

[PCA of high dimensional random walks](https://nips.cc/Conferences/2018/Schedule?showEvent=11975) (Wed 10:45 poster)

* PCA has been proposed as a way to visualize deep net training trajectories. What if you apply it to a random walk?

[Simple, Distributed, and Accelerated Probabilistic Programming](http://papers.nips.cc/paper/7987-simple-distributed-and-accelerated-probabilistic-programming) (Wed 10:45 poster)

* On Edward2, a new probabilistic programming package that works with Tensorflow. My former colleague Alexey Radul's name is on it. Google (Brain)

[Autoconj: Recognizing and Exploiting Conjugacy Without a DSL](https://nips.cc/Conferences/2018/Schedule?showEvent=12013) (Thu 10:45 poster)

* Automatically optimize parts of a probabilistic program embedded in Python. Also from Google AI/Brain

[Tangent: Automatic differentation using source-code transformation for dynamically typed array programming](https://nips.cc/Conferences/2018/Schedule?showEvent=11606) (Wed 10:45 poster)

[Backpropagation with Callbacks](http://papers.nips.cc/paper/8221-backpropagation-with-callbacks-foundations-for-efficient-and-expressive-differentiable-programming) (Wed 17:00 poster)

[Automatic Differentiation in ML: Where we are and where we should be going](https://nips.cc/Conferences/2018/Schedule?showEvent=11836) (Thu 10:40 Track 1)

* A bunch of work on automatic differentiation. One of them does source code transformation on Python!

[Human-in-the-Loop Interpretability Prior](https://nips.cc/Conferences/2018/Schedule?showEvent=12706) (Thu 10:25 Track 1)

* What makes an model interpretable? Ask ML researchers.

[SLANG: Fast Structured Covariance Approximation for Bayesian Deep Learning with Natural Gradient](http://papers.nips.cc/paper/7862-slang-fast-structured-covariance-approximations-for-bayesian-deep-learning-with-natural-gradient) (Thu 10:45 poster)

[BRUNO: A Deep Recurrent Model for Exchangeable Data](http://papers.nips.cc/paper/7949-bruno-a-deep-recurrent-model-for-exchangeable-data) (Thu 10:45 poster)

* Bayesian deep learning models.

[Hyperbolic Neural Networks](http://papers.nips.cc/paper/7780-hyperbolic-neural-networks.pdf) (Thu 15:30 Track 2)

* A theory for neural networks that work in hyperbolic geometry, which is "bigger" than Euclidean space even in many dimensions.

[Sample-Efficient Reinforcement Learning with Stochastic Ensemble Value Expansion](https://nips.cc/Conferences/2018/Schedule?showEvent=12742) (Thu 15:50 Track 1)

* A model-based RL approach that can learn from much fewer samples, but also performs well asymptotically by falling back to something like model-free RL.

[Deep Reinforcement Learning in a Handful of Trials using Probabilistic Dynamics Models](http://papers.nips.cc/paper/7725-deep-reinforcement-learning-in-a-handful-of-trials-using-probabilistic-dynamics-models) (Thu 16:20 Track 1)

* Another model-based RL approach. From Sergey Levine and students at UC Berkeley AI Lab.
