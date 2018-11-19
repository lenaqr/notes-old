----
title: Entropy Is Relative
slug: entropy-is-relative
date: 2018-02-27
----

The entropy of a random quantity $X$ is the "amount of uncertainty" or "information content" in $X$. It is defined as:

$$ H(X) = -E[ \log P(X) ] $$

It's the number of bits you need to specify the value of $X$ if you know its distribution, or equivalently, the number of random bits you need to generate $X$.

This makes sense for discrete-valued $X$, like coin flips and letters in English text. But what about continuous distributions? What is the entropy of a normal distribution?

This post is to try to make sense of this.

## Infinity?

If you think about it, the entropy of a continuous distribution ought to be infinite. After all, a draw from a normal distribution is a real number which has an infinite number of digits to describe.

But this isn't very useful. Somehow a normal distribution with variance 1 seems less uncertain than a normal distribution with variance 2, and we'd like to capture that.

## Differential entropy

A first idea is to just reuse the same definition, but with probability density instead of mass:

$$ h(X) = -E[ \log p(X) ] $$

But this is kind of fishy. Probability density can be greater than 1, so $h(X)$ can go negative. Also, the density has units of $1/dx$, but we're taking the log of it? It turns out that we've actually defined the [differential entropy][diff], which sort of looks like entropy but doesn't have all the nice properties.

[diff]: https://en.wikipedia.org/wiki/Differential_entropy

## Relative entropy

Better is the idea of relative entropy (also [KL divergence][kl]). If we have a reference distribution with density $q$, then the relative entropy with respect to $q$ is [^nonstandard]

[kl]: https://en.wikipedia.org/wiki/Kullback%E2%80%93Leibler_divergence

$$ H_q(X) = -E[ \log \frac{p(X)}{q(X)} ] $$

[^nonstandard]: This definition is non-standard; relative entropy is usually defined as the negative of the above and spelled $D(p \Vert q)$ or $KL(p \Vert q)$. I defined it this way to make it more similar to the definition of entropy.

The thing in the log is a ratio of densities, so at least the units check out. And if you let $q$ be a general measure rather than a distribution, it subsumes both discrete entropy and differential entropy as special cases (when $q$ is the counting measure or the Lebesgue measure, respectively).

But what does it mean? It's sometimes described as "the difference between the number of bits to encode $X$ using a code optimized for $q$ and a code optimized for $p$," but that never made as much sense to me as regular entropy.

## The connection

To that end, I found it helpful to think back to regular entropy, interpreting it as the number of random bits you need to sample from the distribution of $X$.

How many bits do you need to sample from a continuous distribution? In some sense the answer is still infinity, but no one was going to use infinity digits of the answer anyway. Instead we can ask how many bits are needed to generate $X$ up to $n$ digits of precision.

For now let's imagine $X$ takes on values from $[0, 1)$, so we can easily represent it as a sequence of binary digits. Then the first $n$ digits is just a binary string, so it has a well defined entropy.

In general this will depend on $n$. But if $X$ has a continuous density, after some point all the remaining digits will be effectively uniform, so each additional digit will require an additional random bit. In the limit of large $n$, the number of bits we need will approach $h(X) + n$.

Restating this a bit, we can say that the differential entropy is the number of bits you need to determine $X$ to within an interval of length $2^{-n}$, minus $n$ which is the number of bits you would need to specify that interval naively. Cool.

But notice that we're implicitly using Lebesgue measure here when we talk about interval length and digits of precision. So we can generalize this to relative entropy with respect to any reference measure $q$: it's the number of bits you need to determine the result to within a set of measure $2^{-n}$, as measured by $q$.

And now we see that we get regular entropy back when $q$ is the counting measure! If we determine $X$ to within a set of counting measure 1, then we've determined $X$.

## Maximum entropy is relative

The maximum entropy distribution is the uniform distribution, because it represents the least state of knowledge about $X$, the state of maximum ignorance. Or is it?

It turns out that the distribution which maximizes relative entropy with respect to $q$ is the one where $p(x)$ is proportional to $q(x)$.[^proportional] So the uniform distribution is max entropy only because we're using a uniform reference measure.

[jensen]: https://en.wikipedia.org/wiki/Jensen%27s_inequality#Information_theory

[^proportional]: More technically, $p$ has a uniform density with respect to the measure $q$.

This also solves a puzzle of how max entropy works with change of variables. Example: Suppose you have a coin that lands heads with probability $p$, and you want a prior on $p$. You have no idea, so you assign it the uniform distribution over $[0, 1]$, because it's the maximum entropy distribution. But what if you instead wanted a prior on $\theta = \log p$ instead? You don't know anything about $\theta$ either, so you ought to assign a maximum entropy uniform distribution over $(-\infty, 0]$. But that isn't the same as making $p$ uniform, so what gives?

The answer is that you have to fix a reference measure, which can be either uniform in linear space or log space but not both. Maximum entropy can't help you decide.

Even in the discrete case, there's a version of this reference measure problem when it's not clear how to define the set of possible values. The uniform categorical distribution depends on what the categories are, and categories are made by people.

## A word on thermodynamic entropy

Thermodynamic entropy sure doesn't seem relative. It's measured in units like joules per kelvin and it seems to have real physical consequences, like the fact that you can't un-fry an egg. But thermodynamical entropy is supposed to be related to information entropy; can we fit it into the above picture?

As far as I can tell, everything in statistical mechanics depends on the assumption (axiom?) that all microstates of an [isolated system in equilibrium][mce] are equally probable. That's a reference measure!

[mce]: https://ocw.mit.edu/courses/physics/8-044-statistical-physics-i-spring-2013/readings-notes-slides/MIT8_044S13_mcrocanoncl.pdf

So I think you could say the second law of thermodynamics is really about the *relative* entropy of the universe, with respect to its ultimate stationary distribution.
