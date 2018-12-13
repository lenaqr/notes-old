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

* A model-based RL approach that can learn from much fewer samples, but also performs well asymptotically by falling back to model-free RL.

[Deep Reinforcement Learning in a Handful of Trials using Probabilistic Dynamics Models](http://papers.nips.cc/paper/7725-deep-reinforcement-learning-in-a-handful-of-trials-using-probabilistic-dynamics-models) (Thu 16:20 Track 1)

* Another model-based RL approach. From Sergey Levine and students at UC Berkeley AI Lab.

## Tutorials

David Dunson gave a [tutorial on Scalable Bayesian Inference][sbi].

[sbi]: https://nips.cc/Conferences/2018/Schedule?showEvent=10984

He focused on MCMC, because in his opinion variational methods do a bad job of
quantifying uncertainty and you have no idea how accurate the approximation is.
This seems a bit unfair to me, because when I've used MCMC I also had no idea
how accurate the approximation was. He did have some slides that gestured at
theory behind his methods, so maybe there's something there? What do I know.

Anyway, I agree with the sentiment that if you go to the trouble of doing
Bayesian inference to get an uncertainty estimate, you should do a good job of
it. But he spent most of the time discussing a handful of methods from his
group, skipped over some of them to save time, and the ones he did present felt
like hacks since he breezed over the theory. Overall, I left the talk feeling
disappointed.

Susan Athey presented on [Counterfactual Inference][cfi].

[cfi]: https://nips.cc/Conferences/2018/Schedule?showEvent=10982

To be honest, I didn't pay that much attention during this tutorial and it
wasn't her fault. In broad strokes I would agree that a lot of important
problems are counterfactual inference problems. But outside of textbook
examples, I feel like I don't have any problems that I know how to formulate
as conterfactual inference problems.

It's a topic I definitely want to look into more later.

## Tuesday sessions

I didn't know beforehand that most of the talks at NeurIPS were 5-minute poster
spotlights. In the first session I planned to hop tracks to catch some specific
talks; I quickly realized that this was useless, since 5-minute talks have no
content. Browsing the posters themselves was comparatively way more useful.

I met Durk Kingma, who was presenting the Glow poster. I learned the following:

* Their work is based on a previous invertible architecture called Real NVP. The
  architecture is nearly the same but they've made some small refinements.
* It sounds like most of the performance gain relative to the previous paper
  comes from training a bigger and better model using more computers.
* I asked why this model generates good-quality images, compared to VAEs which
  (I thought) generate blurry images. Kingma said he thinks a VAE could generate
  similarly good images if a similar amount of work was put into it.
* However, VAEs still achieve better likelihood.
* More reading on invertible model architectures: [Analyzing Inverse Problems
with Invertible Neural Networks][ann]

[ann]: https://hci.iwr.uni-heidelberg.de/vislearn/inverse-problems-invertible-neural-networks/

I missed the talk on Neural ODEs, unfortunately. I've heard it was a high
quality paper, so I'll check it out.

## Wednesday sessions

Joelle Pineau gave an invited talk on reproducibility in reinforcement learning.
Two main takeaways:

* Reinforcment learning algorithms can perform differently due to different
  implementations, different hyperparameters, even different random seeds. We
  need to do more careful about fair comparisons to reach robust conclusions.
* Standard benchmark environments are easy to memorize. We need more diverse,
  realistic environments that test generalizability of results.
  
At posters, I had some good discussion with one of the authors of the IWVI
paper. I was a little concerned that it optimizes an upper bound on the KL
divergence, so it might waste effort minimizing the looseness of the bound
instead of the thing you care about. But the empirical results do look pretty
good.

I checked out the Edward2 poster. It sounds like the most exciting things about
it are that it supports stuff like distributing a large model across multiple
TPUs, and it's lower-level than alternatives like Pyro and therefore flexible
enough to support research into experimental model architectures. Having now
read the Edward2 paper and compared it to the [documentation of Pyro's internal
APIs][poutine], my impression is that these two actually seem extremely similar.
I'd like to try them both and compare sometime, when I get back into
probabilistic programming.

[poutine]: http://pyro.ai/examples/effect_handlers.html

I visited the Tangent poster and found out about a more recent Google
project in the same space, [jax][jax]. It uses program tracing for autodiff
combined with JIT-compiling code to GPUs and TPUs for high performance.

[jax]: https://github.com/google/jax

I didn't actually see the poster on "Backpropagation with Callbacks", but my
coworker pointed it out later. It's a way to implement automatic differentation
very simply and cleanly using functional programming. Might be worth studying,
although I'm not so interested in building an AD system from scratch that
doesn't come with a big library of array functions and GPU support and stuff.

## Thursday sessions

A few cool talks and posters today. 

In the morning I engaged with the SLANG poster. They use a low rank + diagonal
approximation to a covariance matrix (in this case, the covariance of a
variational posterior over model parameters). The low rank part is computed with
an eigendecomposition on each iteration and then the diagonal is corrected. I've
thought about how to compute a low rank approximation of a covariance matrix
before, but I hadn't thought about the fact that it's also computationally easy
to maintain the exact diagonal as a correction to the approximation.

In fact there's another natural gradient descent paper that uses this idea that
maintaining a diagonal correction is cheap: [Fast Approximate Natural Gradient
in a Kronecker-Factored Eigenbasis][ekfac]

[ekfac]: http://papers.nips.cc/paper/8164-fast-approximate-natural-gradient-descent-in-a-kronecker-factored-eigenbasis

In the afternoon I saw the two talks about model-based reinforcement learning
approaches, STEVE and PETS. Listening to the talks, they seemed extremely
similar to me: both emphasized quantifying uncertainty in the dynamics models,
and both emphasized how they could learn using few samples compared to
model-free methods. I probably could tell the difference if I were in the field
and could unpack what the jargon in the names meant, but instead I visited the
posters and found out:

* STEVE is based on Q learning. The model is used to roll out several time steps
  to obtain a more accurate estimate of the action-value function. It uses the
  uncertainty in the model to decide how far to roll out. If the model is too
  uncertain, it will fall back to one step which is the same as Q learning.
  
* PETS uses the dynamics model directly to plan its next sequence of actions by
  sampling trajectories. The model is the only thing that is learned, no policy
  or value function; however it does more work at inference time.

## Workshops

Frank Wood spoke about probabilistic programming. He's interested in
probabilistic models as *programs* with interesting dependency structure, and
[inference algorithms that take advantage of that structure][faith].

[faith]: http://papers.nips.cc/paper/7570-faithful-inversion-of-generative-models-for-effective-amortized-inference

One thing I found interesting is that he gave a plug for the [wake sleep
algorithm][wake] for learning an inference model, to be contrasted with the
variational Bayes methods that have been more popular recently. I haven't really
seen this before, but it reminded me of a [paper on neurally-guided procedural
generation][proc] I saw Noah Goodman talk about where they used perhaps a
similar technique.

[wake]: https://arxiv.org/abs/1805.10469
[proc]: https://papers.nips.cc/paper/6353-neurally-guided-procedural-models-amortized-inference-for-procedural-graphics-programs-using-neural-networks.pdf

There was another talk on model-based reinforcement learning using Bayesian
neural networks. One issue is that if you use the learned model as an input to a
planning algorithm that uses gradients, the planner will find adversarial
examples in the model. Oops!

One of my big takeaways from the Bayesian deep learning workshop is that
Bayesian models and other existing methods of uncertainty quantification seem to
do a bad job of predicting "out-of-distribution" inputs. They'll assign high
uncertainty in areas near decision boundaries, but they won't necessarily assign
high uncertainty for random inputs that are way outside the training
distribution.

A particular manifestation of this: [Do Deep Generative Models Know What They
Don't Know?][idk] This paper finds that a generative flow-based model trained on
the CIFAR-10 dataset assigns higher probability to examples from the SVHN
dataset than the ones from the training set. It seems these models are not
exactly doing what we think or would like that they are.

[idk]: http://bayesiandeeplearning.org/2018/papers/67.pdf

## Misc

In the above I've focused on content, rather than on my experience of attending
the conference.

I think that at some point I developed an overly rosy expectation of how
intellectually valuable it would be to attend a large academic conference like
NeurIPS. Attending talks was less enlightening than I imagined; meeting specific
scientists whose names I'd heard of was less exciting than I imagined. And I
don't know that it would be worth attending for the full week if I were to do it
again.

But adjusting for those expectations, I'm definitely glad I went.

My favorite part of the program was the poster sessions. I liked to hear people
talk about their work in a less scripted way, where they had more time to go
over details and maybe the background ideas and concepts that they build upon,
and it felt easier to ask questions and have some semblance of a conversation.

I'm not going to talk here about my conversations with people at our recruiting
booth or events, or with my former classmates and labmates and others I
recognized or met for the first time -- but those also felt valuable.

Most of all it was an excuse to immerse myself in machine learning and AI and
think about nothing else for a week. I definitely appreciated it for that alone.
My head is spinning with ideas now and I hope I get around to following up on
some of them.
