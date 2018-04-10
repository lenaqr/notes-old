----
title: Three Ways to Look at a Matrix
slug: matrix-three-ways
date: 2018-04-08
----

A matrix can be used to represent at least three different things:

1. A linear map, which takes vectors to vectors
2. A bilinear form, which takes pairs of vectors to scalars
3. An element of the tensor product of two vector spaces

The first one of these is the most familiar, if you learned linear algebra the way I did. A matrix $M$ represents a linear map which acts according to multiplying a vector by that matrix, $T(v) = Mv$.

For a while I thought this was the only way to think about matrices, and while it is the right way a lot of the time, sometimes people do use matrices in some other way and it's confusing to try to interpret them as linear maps. And sometimes it's helpful to view the same matrix in multiple ways. So I'd like to say a little about other ways to look at a matrix.

## Bilinear forms

A bilinear form is a function that takes two vectors and produces a scalar, and is linear in each argument separately. Some familiar examples are the dot product and the cross product.

If you have a $m$ by $n$ matrix $M$, you can define a bilinear form $T: \mathbb{R}^m \times \mathbb{R}^n \to \mathbb{R}$ by:

$$T(u, v) = u^T M v$$

You can think of this as a sort of product of $u$ and $v$, where the $(i,j)$ entry of $M$ is the weight to put on $u_i$ times $v_j$. (Exercise: show this by expanding the matrix-vector products.)

The dot product is what you get if $M = I$. The cross product in three dimensions is given by the matrix

$$\begin{pmatrix}
0 & 1 & -1 \\
-1 & 0 & 1 \\
1 & -1 & 0 \\
\end{pmatrix}$$

A bilinear form can be used to define a quadratic function from vectors to scalars (a [quadratic form][quadratic form]) by letting $u$ and $v$ be the same vector. For example, the probability density of a normal distribution in multiple dimensions looks like

$$p(x) \propto \exp( -(x - \mu)^T \Sigma^{-1} (x - \mu) )$$

[quadratic form]: https://en.wikipedia.org/wiki/Quadratic_form

where $\mu$ is the mean and $\Sigma$ is the covariance. The thing in the exponent is a "product" of $x - \mu$ with itself. So the log density peaks at $x = \mu$, and it falls off quadratically in each direction with some curvature determined by $\Sigma$.[^psd]

[^psd]: Technically this also depends on the fact that covariance matrices are positive definite, which is basically a condition that the "product" of any vector with itself is not negative.

If you have a $M$ which represents a linear map $\mathbb{R}^m \to \mathbb{R}^n$, you can "cast" it into a bilinear form: $u^T M v = u \cdot Mv$. That is, first apply the linear map to $v$ to get another vector $M v$, and then take the dot product of that with $u$.

In fact, any bilinear form can be viewed this way, and that's what you do when you insist that the matrix $M$ represents a linear map.

## Tensor products

The tensor product $u \oplus v$ represents the pair of vectors $u$ and $v$, if you think of them as the pair of arguments to a bilinear map. The tensor product space is what you get if you also allow linear combinations of these. Fuller explanation: Jeremy Kun's post [How to Conquer Tensorphobia][tensorphobia]

[tensorphobia]: https://jeremykun.com/2014/01/17/how-to-conquer-tensorphobia/)

As a matrix, you can represent $u \oplus v$ as the outer product $uv^T$. It's easy to check that $uv^T$ is linear in each of $u$ and $v$ separately.

If you have $uv^T$, you can determine the result of $u^T M v$ for any $M$. This is the "trace trick":

$$ u^T M v = \mathop{\rm tr}(u^T M v) = \mathop{\rm tr}(M vu^T) = \mathop{\rm tr}(M (uv^T)^T) $$

So $uv^T$ is a way to summarize $(u, v)$ that plays nicely with bilinear stuff and lets you take linear combinations of pairs $(u, v)$.

The example I have in mind here is covariance matrices. If $x$ is a random vector with zero mean, its covariance matrix is $E[xx^T]$. This matrix lets you compute the expectation of any quadratic function of $x$, that is, anything that looks like $E[x^T M x]$.[^covar-basis-independent]

[^covar-basis-independent]: I like this because it shows that the covariance matrix represents an object that is coordinate-independent; it doesn't just tell you the covariance between $x_i$ and $x_j$, which you can get by reading off the entries, but also the covariance between linear functions of $x$ that are not coordinate-aligned.

There is a way to think of $uv^T$ as a linear map (or to think of a linear map as a linear combination of $uv^T$s). Jeremy Kun has a post explaining this too: [Tensorphobia and the Outer Product](https://jeremykun.com/2016/03/28/tensorphobia-outer-product/)

## Some things you can do with matrices and what they mean

Matrix multiplication:

* If $A$ and $B$ are matrices representing linear maps, then $AB$ represents the linear map of $A$ composed with the linear map of $B$.

* If $A$ represents a linear map and $B$ represents a bilinear form, $A^T B A$ represents the bilinear form you get by applying $A$ to the each argument before applying $B$. $A^T B$ is if you apply $A$ to the first argument only, and $B A$ if you apply $A$ to the second argument only.

* If $A$ and $B$ represent linear maps, $A^T B$ represents the bilinear form you get by applying $A$ to the first argument and $B$ to the second argument, then taking a dot product.

Transpose:

* If $A$ is a linear map from $U$ to $V$, $A^T$ is a linear map from $V^*$ to $U^*$, where $V^*$ is the dual vector space of $V$. This is a bit complicated and deserves its own post, which I won't write because others probably have already elsewhere.

* If $A$ is a bilinear form, $A^T$ is the bilinear form you get by switching the arguments. If $A$ is symmetric, its bilinear form is symmetric in its arguments.

* If $A$ is a linear combination of outer products, $A^T$ is what you get if you did the outer products in the other order ($vu^T$ instead of $uv^T$).

Eigenvectors:

* An eigenvector $v$ of $A$, with eigenvalue $\lambda$, is a vector satisfying $Av = \lambda v$. That is, the linear map of $A$ acts on the vector $v$ by scaling it by $\lambda$.

* If $A$ is a bilinear form, a right eigenvector $v$ of $A$ is a vector that has the property that for all $u$, $u^T A v = u^T \lambda v = \lambda (u \cdot v)$. A left eigenvector is the same thing but for the left argument. This property sounds like just a roundabout way to say $Av = \lambda v$ but it makes nice things happen if you have an orthonormal basis of eigenvectors.

Diagonal:

* A linear map whose matrix is a diagonal matrix is one that acts on each coordinate independently.

* A bilinear form whose matrix is diagonal is one that acts on each coordinate of the two vectors independently; it has no "cross terms".

All of this except for diagonality is coordinate free, so it works the same if you change to a different basis. Some of it depends on the dot product, so it only makes sense if it makes sense to take a dot product. I think it's worth noticing when you do something that depends on your choice of coordinates, or your choice of units (which affects the dot product), because it determines whether you can make these choices arbitrarily or if they matter.[^pca]

[^pca]: An example that comes to mind is [PCA][pca]. PCA cares about the Euclidean distances between the points, so it only makes sense when it would make to take dot products. In particular this means that if you scale some of your variables, the result of PCA will be different!

[pca]: https://en.wikipedia.org/wiki/Principal_component_analysis

## Bonus: quantum states and observables

(Disclaimer: I'm not a physicist and I don't really know what I'm talking about)

In quantum mechanics, an observable is represented by a linear operator $A$ that acts on the quantum state $\psi$. The idea is that you write $\psi$ as a linear combination of eigenstates of $A$, and in each eigenstate the value of $A$ is given by the corresponding eigenvalue, and when you observe $A$ the state collapses to one of the eigenstates.

It always seemed a bit weird to me that the result of the linear operator $A$ doesn't have a physical meaning and is hardly ever talked about, as if the operator exists only to be a bag of eigenstates.

However, the expectation value of $A$ in the state $\psi$ is $\langle \psi | A | \psi \rangle$ (which is basically $\psi^T A \psi$ in physicists' notation). So, maybe another way to think of a quantum observable is as a bilinear form, which when applied to a quantum state gives its expected value?

Also, the density matrix corresponding to $\psi$ is $| \psi \rangle \langle \psi |$, which is just the outer product of $\psi$ with itself. As we've seen, this is enough information to determine the expected value of any observable $A$. And it makes sense that you can take linear combinations of these to get mixed states, and the expected values of observables factor through to their expected values in the pure states.

But this story only accounts for expected values, and a quantum state is supposed to determine all the probabilities of each result. So it seems like eigenstates still have to have special meaning physically. I'm still confused about this.
