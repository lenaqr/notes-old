---
title: Pyro and Edward2 comparison by example
---

To get a flavor of the probabilistic programming frameworks Pyro and Edward2, I
decided to implement some examples in each of them.

I've started with a small example cribbed from the Pyro docs. Notebooks:
[Pyro][pyro] [Edward2][edward2]

[pyro]: https://github.com/luanthe/notebooks/blob/master/2018-12-16%20pyro.ipynb
[edward2]: https://github.com/luanthe/notebooks/blob/master/2018-12-16%20edward.ipynb

My first impressions:

Pyro has a much more organized set of tutorials and examples that explain each
of its features. Edward2 -- and Tensorflow Probability in general of which it is
a part -- lacks anything comparable. There is a set of lengthier standalone
examples showcasing various things you can do, but it's hard to get a complete
picture from them. Hopefully this will get better with time.

Also, while Pyro does SVI out of the box, Edward2 doesn't seem to have a built
in variational inference op at all; you have to spell out the ELBO objective.
This would make sense if Edward2 is in some sense complementary to existing
frameworks, especially Edward 1. You could do vanilla VI in Edward, so Edward2
is for everything else.

Next I'd like to take one of the standalone examples in Edward2 and rewrite it
in Pyro.

Update: I obviously never got back to this, but [someone else did something
similar][colcarroll] with many frameworks. It's more aimed toward the common use
patterns of each API, whereas I would've liked to do examples digging into some
lower level details, but that's a task for another day.

[colcarroll]: https://colcarroll.github.io/ppl-api/
