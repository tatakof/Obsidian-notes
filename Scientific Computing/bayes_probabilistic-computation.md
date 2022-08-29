A probability distribution is a frustratingly abstract object. In order to explicitly specify a probability distribution in full we would have to specify the probability assigned to each element of the ambient σ-algebra, which is beyond impractical for even simple spaces. In practice we instead define probability distributions _implicitly_ through their computational consequences. More formally we define them _algorithmically_ through methods that return expectation values.

More poetically we can think of a probability distribution as an oracle. While we cannot perceive the oracle directly, we can ask it questions. Those questions take the form of real-valued, integrable functions, and the answers we receive from our probabilistic oracle take the form of expectation values of those functions with respect to the probability distribution.

Some simple distributions are structured such that certain expectation values are known analytically. For example the distributions specified by probability density functions within the Gaussian family are parameterized in terms of their means and standard deviations. These distributions also admit closed-form cumulative distribution functions which can be used to compute probabilities and quantiles.

The more sophisticated probability distributions that arise in applied analyses, however, do not enjoy these analytic results, even for the expectation values of simple functions. Instead we have rely on numerical algorithms which only _estimate_ the exact expectation values returned by a given probability distribution. In other words we don’t hear our oracle so clearly, receiving our answers only over noisy transmission lines that corrupt its delicate answers. The challenge of practical probabilistic computation is the construction of algorithms with well-behaved and well-quantified errors that allow us to understand when we can trust the corrupted answers that we receive.

In this case study I introduce the basics of probabilistic computation, with a focus on the challenges that arise as we attempt to scale to problems in more than a few dimenions. I discuss a variety of popular probabilistic computational algorithms in the context of these challenges and set the stage for a more thorough discussion of Markov chain Monte Carlo and Hamiltonian Monte Carlo that will follow in future case studies.

# 1 Representation with Computational Taxation


The basic algorithmic approaches to probabilistic computation are motivated by how we represent a target probability distribution, π, defined over an ambient space, Q. I am intentionally using Q to denote the ambient space, and q to denote points in that space, instead of something more familiar, to emphasize the abstract nature of this discussion. Computation is the same regardless of the interpretation of π and Q



Here we will consider two of the most popular representations – probability density function representations and sampling representations.


## 1.1 I Just Find Densities Terribly Exhausting

In most applications probability distributions are specified through a probability density function representation within a given parameterization, and the computations that follow.

For example probability distributions over discrete spaces can be specified with a probability mass function, π(q), and expectation values can be computed with summation over the entire space,

$$
\mathbb{E}_{\pi}[f] = \sum_{q \in Q} \pi(q) \, f(q).
$$
(m' wtf is that f(q)?????????)

Beyond ambient spaces with only a finite number of points, these sums quickly exhaust our finite computational resources. In practice all we can do is limit whatever resources are available to a subset of points in order to _approximate_ these expectation values.


When specifying probability distributions over continuous spaces we can appeal to probability density functions, π(q), that give expectation values through the standard integral from calculus,

$$
\mathbb{E}_{\pi}[f] = \int_{Q} \mathrm{d} q \, \pi(q) \, f(q).
$$


For most probability density functions we won’t be able to work out these integrals analytically. Without infinite computational resources we won’t be able exhaustively survey the entire ambient space to compute a numerical value, either.


...

The ultimate lesson here is that any attempt to exhaustively quantify a space, whether a discrete space or a discretized continuous space, in order to estimate expectation values is largely limited to one or two-dimensional problems. In order to scale to the higher-dimensional problems that arise in practice we need to be smarter with our precious, finite computational resources. We need to identify exactly _where_ in the ambient space we should be focusing that computation to achieve as small an error as possible



Unfortunately the answer to that question is obfuscated by the counterintuitive behaviors of high-dimensional spaces. In order to build up any conceptual understanding we first need to learn how our intuition fails.

## 1.2 The House Always Wins


























