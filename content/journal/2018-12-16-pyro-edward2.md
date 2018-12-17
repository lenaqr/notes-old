---
title: Pyro and Edward2 comparison by example
---

To get a flavor of the probabilistic programming frameworks Pyro and Edward2, I
decided to implement some examples in each of them.

I've started by running through a small example in the Pyro tutorial docs and
then porting it to Edward2. Notebooks: [Pyro][pyro] [Edward2][edward2]

[pyro]: https://github.com/luanthe/notebooks/blob/master/2018-12-16%20pyro.ipynb
[edward2]: https://github.com/luanthe/notebooks/blob/master/2018-12-16%20edward.ipynb

My first impressions:

Pyro has a much more organized set of tutorials and examples that explain how to
use it. Edward2 -- and Tensorflow Probability in general of which it is a part
-- lacks anything comparable. There is a set of lengthier standalone examples
showcasing various things it can do, but I end up having to cross reference
several of them just to learn what I need to put together a simple example.
Hopefully this will get better with time.

Also, while Pyro does SVI out of the box, Edward2 doesn't seem to have a built
in variational inference op at all; I copied an example that explicitly wrote
out the stochastic ELBO objective in terms of the model and variational models'
log joint functions. This would make sense if Edward2 is in some sense
complementary to existing frameworks, especially Edward 1. You could do vanilla
VI in Edward, so Edward2 is designed for everything else.

Next I'd like to take one of the standalone examples in Edward2 and rewrite it
in Pyro.

[probtorch]: https://github.com/probtorch/probtorch
