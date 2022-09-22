## 1.1 Model

Our first interaction with Stan as a user will be to specify a complete Bayesian model. This requires defining the observational space, y∈Y, the model configuration space, θ∈Θ, and then a joint probability density function over the product of these two spaces,
$$
\pi(y, \theta).
$$
**Because probability density functions can be awkward to work with in practice we will instead specify our model through the _log probability density function_**
$$
\log \pi(y, \theta).
$$
Let’s consider, for example, an observational space consisting of the product of N real-valued components,

$$
y = \left\{y_{1}, \ldots, y_{N} \right\},
$$
and the independent observational model

$$
\pi(y \mid \theta) = \prod_{n = 1}^{N} \text{normal} \, (y_{n} \mid \theta, 1).
$$
We then fill out the complete Bayesian model with a prior model on the lone parameter of our model configuration space,

$$
\pi(\theta) = \text{normal} \, (\theta \mid 0, 1).
$$

The joint probability density function of our complete Bayesian model is then given by
$$
\begin{align*}
\pi(y, \theta)
&= \pi(y \mid \theta) \, \pi(\theta)
\\
&=
\prod_{n = 1}^{N} \text{normal} \, (y_{n} \mid \theta, 1)
\cdot \text{normal} \, (\theta \mid 0, 1),
\end{align*}
$$

The log joint probability density function that will specify in the Stan Modeling Language is then

![[Pasted image 20220922094726.png]]


where now `normal_lpdf` refers to the natural logarithm of the normal probability density function.

## 1.2 Stan Program

The _Stan modeling language_ specifies each element of a Bayesian model through _programming blocks_. First the _data block_ defines the components of the observational space,

```
data {
  int N;
  real y[N];
}
```

Then the _parameters block_ defines a parameterization of the components of the model configuration space,

```
parameters {
  real theta;
}
```

Finally the _model block_ defines the target log probability density function by adding up each contributing log probability density function into a global `target` accumulator variable,

```
model {
  target += normal_lpdf(theta | 0, 1);
  for (n in 1:N)
    target += normal_lpdf(y[n] | theta, 1);
}
```

Altogether these blocks define a _Stan program_ that represents our complete Bayesian model,

```
data {
  int N;
  real y[N];
}

parameters {
  real theta;
}

model {
  target += normal_lpdf(theta | 0, 1);
  for (n in 1:N)
    target += normal_lpdf(y[n] | theta, 1);
}
```

## 1.3 Interface

Once we have specified our model we need to evaluate the components of the observational space on their observed values and compute the corresponding posterior expectation values. The conditioning and probabilistic computation is handled by the core libraries of Stan that convert a given Stan program into an _executable program_ capable of evaluating the log posterior density function _and_ its gradient function in order to run a high-performance implementation of Hamiltonian Monte Carlo. All of this machinery, however, is concealed behind an interface into which users input the observed data and from which they receive algorithm output and diagnostics.

![[Pasted image 20220922095302.png]]

..
We can now call the main `RStan` command **which conditions our joint model on the observed data and runs Hamiltonian Monte Carlo to estimate expect values.** In order to ensure reproducible behavior I make sure to set an explicit seed for Stan’s internal pseudo random number generator.

```
fit <- stan(file='stan_programs/intro.stan', data=input_data, seed=4938483)
```

The returned `stanfit` object contains information about our model and, most importantly, all of the output of Hamiltonian Monte Carlo.


Even with an algorithm as powerful as Hamiltonian Monte Carlo we have to be careful to check the available diagnostics for any indication of bias. Here I’m using a script that automates the checks in my personally recommended diagnostic workflow from the contents of the `stanfit` object.

```
util <- new.env()
source('stan_utility.R', local=util)

util$check_all_diagnostics(fit)
```
```
[1] "n_eff / iter looks reasonable for all parameters"
[1] "Rhat looks reasonable for all parameters"
[1] "0 of 4000 iterations ended with a divergence (0%)"
[1] "0 of 4000 iterations saturated the maximum tree depth of 10 (0%)"
[1] "E-FMI indicated no pathological behavior"
```

**Without any indications of problems we can move on to using the samples output by Hamiltonian Monte Carlo to construct Markov chain Monte Carlo estimators.** A summary of default estimators and related quantities, including the means and quantiles of the component marginal distributions, is given by the `print` function.



For more bespoke estimators we can access the samples contained in the `stanfit` object directly using the `extract` function.

```
params <- extract(fit)
```

By default Stan runs four parallel Markov chains each with 1000 iterations in their main sampling phase. This corresponds to 4000 total samples with which we can work.

Using these samples we can, for example, **construct histograms to visualize the marginal posterior distributions for each component of the model configuration space**, in this case just the one `theta`.

# 2 The Stan Ecosystem
Mindful of the basic functionality of Stan we can now develop a much more comprehensive understanding of the Stan ecosystem and each of its components. The Stan ecosystem can roughly be decomposed into a _language library_, a _math library_, an _algorithm library_, and a set of interfaces.

The user experience begins with the specification of a Stan program that defines the target probability distribution.
![[Pasted image 20220922100446.png]]
Within Stan the language library parses a given Stan program into a high-performance `C++` program with the math library defining the `C++` functionality.

![[Pasted image 20220922100652.png]]

The resulting `C++` model representation is then compiled into an executable program that implements a suite of computational algorithms defined in the algorithm library.

![[Pasted image 20220922100715.png]]

...


## 2.1 The Stan Language Library

...

## 2.2 The Stan Math Library

**Critically the Stan Math Library also implements _automatic differentiation_ for all of its functions. Automatic differentiation is a technique for efficiently evaluating the exact values of the gradient of a `C++` function at a given set of inputs. This means that every Stan program defines both a target log probability density function _and_ the corresponding gradient function without any additional effort from the user. This then allows the use of extremely effective gradient-based algorithms like Hamiltonian Monte Carlo without the user having to pour through pages upon pages of analytic derivative calculations.**

**The cost of automatic differentiation is only a small overhead relative to the cost of the evaluating the `C++` function itself, but that overhead can be important in performance-limited circumstances. A key feature of advanced Stan use is identifying programming patterns with excessive overhead and replacing them with code that leads to more efficient automatic differentiation.**

## 2.3 The Stan Algorithm Library
...

**The flexibility of the Stan Modeling Language is critical for the specifying the sophisticated models that live on the frontiers of applied statistics, but that breadth also stresses even the most advanced algorithms. Ultimately the user is responsible for verifying that a given algorithm has yielded estimation sufficiently accurate for their application, using whatever diagnostics are provided. Extensive theoretical and empirical work have verified that the dynamic Hamiltonian Monte Carlo algorithm in Stan is robust to a diversity of Stan programs with diagnostics that clearly identify failures. Modal estimation using the optimizer and variational estimation using ADVI have proven to be much more fragile, with failures manifesting in subtle ways that are often hard to diagnose.**

We will be working with dynamic Hamiltonian Monte Carlo exclusively in this case study and beyond.

## 2.4 The Stan Interfaces
...
`CmdStan` is the most lightweight interface closest to the core `C++` functionality. `CmdStan` consists of a series of makefiles that allow a Stan program to be compiled into a executable program within a command line environment. Algorithm output is streamed to text files which can be analyzed both during and after the running of an executable. Because `CmdStan` is so lightweight it adds little overhead to the core algorithms and consequently is especially useful in performance-limited applications. The proximity to the core libraries also means that `CmdStan` typically exposes new language and algorithm features first.

The most popular interfaces are `RStan` and `PyStan`. These interfaces are integrated directly into the `R` and `Python` environments. Algorithm output is stored in memory instead of an external file making it easier to analyze after the fact but also preventing it from being analyzed while the algorithms are running. The tight integration between these interfaces and their target environments makes for a smooth user experience, but it does introduce some computational overhead. Moreover this approach is much more challenging for software development. **This difficulty, for example, has recently manifested in long delays for updates to the `RStan` and `PyStan` interfaces relative to the core library and `CmdStan`.**

Finally there is a large collection of interfaces that expose `CmdStan` through other computing environments, such as `Julia`, `Mathematica`, `Matlab`, and more. Recently `CmdStanR` and `CmdStanPy` have been introduced to expose `CmdStan` in `R` and `Python` directly, complementing the more integrated functionality of `RStan` and `PyStan`.


# 3 Probabilistic Programming

Earlier I defined Stan as a probabilistic programming language without actually defining what a probabilistic programming language is. Unfortunately as probabilistic programming has become more popular over the past decade so too have the diversity of its interpretations. These different interpretations can make it challenging to understand the properties of a particular language while also complicating comparisons between different languages.

The one unifying aspect of probabilistic programming is the use of computer programs to represent probability distributions and their transformations under various operations. Ambiguities arise, however, when specifying exactly which probability distributions and probabilistic operations are within the scope of a given probabilistic programming language.

Ideally a probabilistic programming language would be able to specify _every_ possible probability distribution over _every_ possible ambient space, along with _every_ possible probabilistic operation from expectations to pushforwards and conditionings.
![[Pasted image 20220922110354.png]]

Unfortunately the space of all possible probability distributions is littered with distributions whose probabilities cannot be computed, even in principle. At the very least any practical language has to be restricted to the space of _computable_ probability distributions.

![[Pasted image 20220922110408.png]]

Within the space of computable probability distributions most languages focus on product distributions.

![[Pasted image 20220922110440.png]]

The space of product distributions can be further broken down by whether or not the component spaces are continous, discrete, or a mixture of the two.

![[Pasted image 20220922110508.png]]
Even with a restriction to product spaces a critical limitation of probabilistic programming is which operations we can _faithfully_ implement in practice. The design of a probabilistic programming language has to carefully balance the extent of the language with the reality of the probabilistic computation.

## 3.1 All In

Many probabilistic programming languages originating in theoretical computer science are concerned with the challenge of effectively specifying probability distributions and their operations, but not so much the accurate implementation of those operations. While there are many important research questions confronted by these languages, their theoretical focus has to be taken into account when they are brought into the proximity of practical applications.

The extent of these languages can be massive, spanning nearly every computable probability distribution and probabilistic operation. These languages are of limited use in practice, however, because most of the programs one can write in them can’t be evaluated accurately, at least not without infinite computation. A probabilistic algorithm can always be applied to evaluate these programs, but if the output of those algorithms doesn’t implement the probability theory with small, quantifiable error then we have no idea how faithful that output will be.

**We often take for granted that a computer will be able to accurately implement the operations encoded in our programs. That cavalier attitude is _usually_ safe, but when the implementations become less trustworthy programming becomes much, much harder.** Just ask anyone who has struggled with the difference between the exact arithmetic of the real numbers and how addition and multiplication are actually implemented in floating point arithmetic.

A key design feature of more practically minded probabilistic programming languages is the restriction of distributions and operations to those within the scope of accurate computation. Given the state-of-the-art in probabilistic computational algorithms, this essentially limits the scope of useful probabilistic programming languages to the computation of conditional expectation values. That said, some people are more optimistic and one should recognize that this isn’t a universal opinion.

## 3.2 Graphic Design

**There are many possible designs for specifying conditional probability distributions, each based on different representations of probability distributions.**

**For example probability distributions over product spaces can be represented with directed graphical models.** Consequently we can use graphical models as the basis for a probabilistic programming language. The use of _univariate_ directed graphical models was pioneered by the BUGS project [@LunnEtAll:2009], the first probabilistic programming language popular in applied statistics.

**One benefit of univariate directed graphical modeling languages is that the detailed conditional structure in each program encodes a tremendous amount of information about the target distribution that can then be exploited by not only users but also other computer programs. This facilitates automated _static analysis_ of a given program that can identify ways to implement or even optimize probabilistic computation of the implied probability distribution. BUGS utilized this structure to automatically compute the _Markov blanket_ around each parameter and define conditional updates needed to implement Gibbs samplers.**

This structure, however, comes at a cost. Because only a relatively small subset of probability distributions can be represented by univariate directed graphical models, any probabilistic programming language designed around this structure will have a fundamentally limited expressibility.


![[Pasted image 20220922111313.png]]
This limitation may not be significant for the simple models one encounters when first learning probabilistic modeling, but it becomes increasingly problematic as one matures into more sophisticated modeling techniques, especially those employing components spaces with multidimensional constraints.

## 3.3 Propensities for Densities

**Another useful representation that probabilistic programming can exploit are probability density functions in a given parameterization of the ambient space. Languages where probabilistic programs specify a parameterization and probability density function are extremely expressive, capable of capturing all probability distributions within the scope of univariate directed graphical languages and much more. The only limitation to the expressiveness of these languages is a restriction to finite-dimensional ambient spaces.**

**At the same time probability density functions provide only a monolithic representation of a probability distribution that doesn’t necessarily reveal any of its internal structure.** This limits the potential for static analysis and some automated operations. For example if we specify a probability distribution over a product space with a joint probability density function then we won’t always be able to automatically construct an explicit conditional decomposition, and hence be unable to apply any algorithms that require such a decomposition.

**A probability density function does, however, provide sufficient information for many probabilistic computational algorithms, in particular Markov chain Monte Carlo. Given a probabilistic program that evaluates the target probability density function these algorithms can generate estimates of expectation values. In fact most of these algorithms need only _unnormalized_ probability density functions that differ from the target probability density function by only a constant,**

$$
\bar{\pi}(x) \propto \pi(x).
$$
**Consequently an even more general target for a probabilistic programming language is an unnormalized probability density function, which I will refer to from here on is as _density function_.**

**Requiring only a density function has the added benefit of enabling probabilistic operations like conditioning. As shown in my product distribution case study, we can generate an unnormalized _conditional_ probability density function by evaluating a joint probability density function at the conditioning variables. Consequently when supported by algorithms that require only density functions a probabilistic programming language can automatically implement conditioning and the estimation of conditional expectation values.**

This is particularly useful for inferential applications as it allows for the evaluation of posterior expectation values once a density function for the complete Bayesian model, and values for the observed data, are provided.

**The expressiveness of probability density functions does come at the expense of some ambiguity. Because many probability density functions will correspond to the same probability distribution, many probabilistic programs in such a language will encode equivalent information. Each of those programs, however, might interact with a given computational algorithm _differently_, introducing the need to find a program that works best with a given algorithm.**


## 3.4 Savile Row
Another important design choice in a probabilistic programming language is whether or not to _embed_ it within another ambient, non-probabilistic programming language, like `R` or `Python`. Embedded languages can take advantage of the existing infrastructure and programmer familiarity of the ambient programming language, making them less intimidating for users. On the other hand embedded languages have to work around the structure of the ambient language which often requires compromising on the probabilistic aspects of the design.

In particular embedded languages may have to exclude popular aspects of the ambient language that are not consistent with the probabilistic programming paradigm, potentially confusing new programmers who don’t have the intuition for which features persist into the embedded language and which do not. Moreover embedded languages will be entirely inaccessible for programmers not familiar with the ambient language in the first place.

Bespoke, or _domain specific_, probabilistic programming languages are designed from the ground up with probability theory in mind. This singular focus allows domain specific languages to be _self-contained_, exposing all of the desired probabilistic objects and operations without any irrelevant language features. Domain specific languages are also independent of any existing language or environment, allowing them to be used in a wide variety of existing analyses. The cost of these features, however, is an increased burden on new users who have to learn _yet another programming language_ in order to implement their inferences.

## 3.5 The Ascent of Stan

A common feature of state-of-the-art algorithms, like Hamiltonian Monte Carlo, is their utilization of differential information about a target distribution to maximize the possibility of accurate computation while also increasing the sensitivity of algorithm-specific diagnostics. The Stan Modeling Language is a domain specific probabilistic programming language designed to complement these algorithms by specifying not just any density function but _differentiable_ density functions defined over continuous product spaces.

![[Pasted image 20220922111451.png]]

Continuous product spaces are vast span the majority of statistical applications, but this restriction does limit the scope of the language. What can’t be captured, however, are largely probability distributions that we cannot faithfully compute anyways.

A _Stan program_ defines a product space consisting of unbound continuous components and bound continuous and discrete components, and an unnormalized probability density function over that product space. When evaluated at the bound variables this density function defines an a continuous, unnormalized conditional density function over the unbound variables suitable for algorithms like Hamiltonian Monte Carlo.

