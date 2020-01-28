Title: Continuous-time discrete-space MCMC

I came across this preprint which I found fascinating:

- Sam Power, Jacob Vorstrup Goldman (2019) [Accelerated Sampling on Discrete Spaces with Non-Reversible Markov Processes][arxiv]

[arxiv]: https://arxiv.org/abs/1912.04681

The main new idea to me is that of MCMC sampling using a continuous-time Markov process, rather than a discrete-time Markov chain. [Hamiltonian Monte Carlo][hmc] and other successful sampling algorithms already use continuous-time dynamics in continuous spaces, and this paper explores analogues of this for sampling discrete spaces.

[hmc]: https://arxiv.org/abs/1701.02434

Working in continuous time makes the algorithm design clean in some ways: rather than rejecting state transitions to get the correct stationary distribution, one can choose how much time advances before the next transition. This effectively determines how much weight the current state gets in the final sample. I think this is similar to the difference between [rejection sampling and importance sampling][jordan]. The authors also import useful ideas from continuous samplers, like adding momentum variables, to design more efficient samplers.

[jordan]: https://people.eecs.berkeley.edu/~jordan/courses/260-spring10/lectures/lecture17.pdf

The authors focus on spaces with a kind of algebraic structure, which plays the role of the vector structure of continuous space. I'm curious where else these ideas can be applied.
