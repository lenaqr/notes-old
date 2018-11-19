----
title: Regularizers Are Not Priors
slug: not-priors
date: 2018-02-22
----

In statistics and machine learning there is an idea called _regularization_, which is when you penalize complex models in favor of simpler models rather than just finding the one model that best fits the observed data. The reason to do this is that simpler models are more likely to generalize; overly complex models can "overfit", picking up on false patterns in the training sample that don't hold in the larger population.

![](/images/PRML_Figure1.4d.png){: width=50% }
Overfitting: the red curve is a 9th-order polynomial fit to the 9 data points in blue, which were generated according to the green curve. From Bishop's [Pattern Recognition and Machine Learning][prml].
{: .figure }

[prml]: https://www.microsoft.com/en-us/research/people/cmbishop/#!prml-book

If you squint, adding regularization is sort of like having a Bayesian prior over possible models, where simpler models have more prior probability than complex models. And indeed, people often talk about it that way, for instance in scikit-learn's documentation of [Lasso](lasso) and [ElasticNet](elasticnet).

But a real Bayesian prior is different! In some important ways. This confused me when I was first learning about Bayesian methods, so this post is to explain the difference.

## Running example: regularized least-squares regression

Suppose we have some data consisting of pairs $(x_i, y_i)$ and we would like to fit a model $y = f(x; \theta)$.[^fxtheta]

[^fxtheta]: Here, I mean that $f$ is some family of models parameterized by $\theta$. For example, $f$ could be the family of 9th-order polynomials, and $\theta$ the coefficients of the polynomial.

In ordinary least squares, the objective is to find the $\theta$ that minimizes the sum of squared errors:

$$ \hat \theta_{OLS} = \arg \min_\theta \sum_i (y_i - f(x_i; \theta))^2 $$

However, this problem may produce an overfit solution or even be underdetermined.

Regularized least squares is when you add an extra term that depends on $\theta$ in order to constrain the solution and make the problem more well behaved. One common form of this is L2 regularization or ridge regression, which adds a penalty term on the L2 norm of $\theta$:

$$ \hat \theta_{RLS} = \arg \min_\theta \left( \sum_i (y_i - f(x_i; \theta))^2 + \Vert\theta\Vert^2 \right) $$

This can make sense if $\theta$ is a vector of coefficients; it can discourage large coefficients that happen to cancel out near the observed data points, such as in the intro figure.

## The connection to probability

So far we haven't said anything about probability. However, it turns out we can cast our modeling in a probabilistic light by interpreting the loss as a negative log likelihood.

In particular, let's now imagine our model is probabilistic, so that $y$ follows a distribution that depends on $x$. If we let[^gaussian]

$$p(y \mid x; \theta) \propto e^{-(y - f(x; \theta))^2}$$

[^gaussian]: You may know this as the density of a [Gaussian distribution][gaussian] centered around $y = f(x; \theta)$.

[gaussian]: https://en.wikipedia.org/wiki/Normal_distribution

then the least squares objective from before boils down to

$$\hat\theta_{ML} = \arg \max_\theta p(y \mid x; \theta)$$

This is called maximum likelihood. Pretty intuitive: find the $\theta$ which assigns the highest probability to the data.

In this framework, we can incorporate the regularization term by imagining we have a prior on $\theta$,

$$p(\theta) \propto e^{- \Vert\theta\Vert^2}$$

And now we're maximizing $p(y \mid x; \theta) p(\theta)$. This is called [maximum a posteriori estimation](https://en.wikipedia.org/wiki/Maximum_a_posteriori_estimation) or MAP for short.

$$\hat\theta_{MAP} = \arg \max_\theta p(y \mid x; \theta) p(\theta)$$

This is what people mean when they say, for example, that L2 regularization corresponds to a Gaussian prior on the coefficients.

So are we Bayes now?

## It's not the same

The biggest way in which this is different from fully Bayesian updating is that it produces a point estimate, a single value $\hat\theta$.

In Bayesian inference, the result of updating on new data *is* the posterior distribution of $\theta$. The posterior represents your belief state after seeing the data; different points in that distribution are different possible models consistent with the data; a wider distribution means more uncertainty about the model. The posterior becomes your new prior going forward, and additional data can further inform your belief about the correct model. At no point does your belief state collapse to a single value of $\theta$.

Let's say after having observed all the $(x_i, y_i)$ we want to make a prediction at a new point $x^*$.

The usual thing to do, whether you're using a regularizer or not, would be to use the $\hat\theta$ from your learning algorithm to predict $y^* = f(x^*; \hat\theta)$.

The fully Bayesian thing to do would be to integrate over your posterior distribution $p(\theta \mid D)$, obtaining a *predictive distribution* on $y^*$:

$$p(y^* \mid x^*, D) = \int p(y^* \mid x^*, \theta) p(\theta \mid D) d\theta$$

This takes into account your uncertainty about $\theta$, and "pushes it forward" into uncertainty about $y^*$.

Obviously in many cases this is a less tractable thing to do; but it does get at something that the point estimate doesn't, and sometimes it may be worth trying to do something more like the Bayesian approach.

Machine learning researchers have been trying to do this! Here are some blog posts about applying Bayesian techniques to deep models.

* Alex Kendall: [Deep Learning Is Not Good Enough, We Need Bayesian Deep Learning for Safe AI](https://alexgkendall.com/computer_vision/bayesian_deep_learning_for_safe_ai/) (2017)
* Yarin Gal: [What My Deep Model Doesn't Know](http://mlg.eng.cam.ac.uk/yarin/blog_3d801aa532c1ce.html) (2015)

## More things about Bayes and non-Bayes

* MAP estimation, the thing where you find the maximum of the posterior and go with it, is not well defined under change of variables. If you have a model parametrized by $\theta$, and you decide, say, to set $u = 1/\theta$ and work with that instead, the posterior max $\hat u_{MAP}$ need not be equal to $1/\hat\theta_{MAP}$.

    In contrast, Bayes doesn't care what variables you choose, as long as you take care to transform your prior density function appropriately for the change of variables.[^variables]

[^variables]: Max likelihood also doesn't care, since there's no prior at all. Also, if $\theta$ is discrete, then MAP is well defined again: it's the one value of $\theta$ with the most probability mass. It's still only as meaningful as a plurality winner though.

* If you actually look at Bayes' rule, there's one piece we didn't about: the normalization constant.

    $$ p(D) = \int p(D \mid \theta) p(\theta) d\theta $$

    This factor is safe to ignore when optimizing over $\theta$. But it has a nice interpretation: it's the probability of seeing the data $D$, averaged over the prior $p(\theta)$. This is sometimes called the model evidence, and you can think of it as measuring how good your prior was in light of seeing the data. You can even use it to compare different priors.[^bmc]

[^bmc]: For more on this kind of stuff, I recommend David MacKay's textbook [Inference Theory, Inference, and Learning Algorithms](http://www.inference.org.uk/itila/book.html), in particular chapter 3 ("More about Inference") and chapter 28 ("Model Comparison and Occam's Razor").

* Probability distributions have to sum up to one. This relates to the previous point. Sometimes this doesn't matter but sometimes it forces you to not assign more probability mass than you have. Compared to inventing a loss function out of thin air, sticking to a probabilistic framework feels to me like almost a form of type checking that rules out some things that obviously make no sense.

I hope I've managed to convey that Bayesian modeling really does bring more to the table and it's not just the same as an additional term on your loss function. I often find the Bayesian answers intuitively pleasing; I'm not saying it's the appropriate tool for every problem, but it's certainly worth learning more about.

---

Edit (April 2018): Here's a [post from raginrayguns on tumblr][raginrayguns] that makes a similar point.

> tl;dr: Regularization is not the point of the prior. Even when we’re not regularizing, the prior is an indispensable part of useful machinery for producing “hedged” estimates, which are good in all plausible worlds.

[raginrayguns]: http://raginrayguns.tumblr.com/post/163079571377/bayes-a-kinda-sorta-masterpost

The post makes a case for why you might want to do the Bayesian thing, which I didn't really say anything about here. It has an example of an estimation problem where using Bayesian reasoning produces a better estimator (according to a specified loss function, which happens to be mean squared error) than maximum likelihood, even with a flat prior.
