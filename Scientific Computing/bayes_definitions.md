Or betancourts glossary?


#### Observational process

 "It is any methodology that measures, collects, curates or manipulates observations sensitive to the latent phenomenon. This includes, for example, not only dedicated experiments explicitly designed to interrogate the phenomenon of interest but also retrospective analyses of incidental experiments or previously conducted experiments designed for other purposes."


Note that we distinguish *possible* outcomes of an observational process from *explicitly realized* observations. Betancourt distinguishes them as: $y$ denotes an arbitrary point in the observation space while $\tilde{y}$ denotes a particular point. 

#### Observation space. 
the variation of possible outcomes of an observation process??
with variability sources being epistemological, ontological or others?

#### Data generating process
Probability distributions over the observation space. 

#### True data generating process
The probability distribution that exactly captures the observational process in a given application. 


#### Observational process vs Observation space
???????


#### Observational model 
This small world defines an *observational MODEL* consisting of individual data generating processes that each define a possible mathematical narrative of how the data could be generated. m' so the observational MODEL consists of individual probability distributions over the observation space that each define a possible mathematical narrative of how the data could be generated'.  I think this is 
$$
\pi_{\mathcal{S}}(\tilde{y} \mid \theta)$$

#### Data generating process
Probability distributions over the observation space. 
Mathematical narrative of how the data could be generated. 


#### True data generating process
The probability distribution that exactly captures the observational process in a given application. 

#### Model configuration space, $\mathcal{S}$
The subset of data generating processes considered in a given analysis. 
Model configuration space and Observational model can be used interchangeably. 


#### Model configuration
An individual data generating process considered in a given analysis. 

#### Observational model
its the same as the model configuration space (interchangeable). 
It consists of individual data generating process that each define a possible mathematical narrative of how the data could be generated. m' so the observational MODEL consists of individual probability distributions over the observation space that each define a possible mathematical narrative of how the data could be generated'. 

#### Parameterization of an observational model
Is the one-to-one mapping between the model configuration space and the numerical space $\Theta$, such as the real numbers. In other words, a parameterization is the assignment of a unique value, or *parameter* $\theta \in \Theta$, to each model configuration, $s \in \mathcal{S}$. Keep in mind that the parameterizations themselves are not unique; in general there will be many equivalent ways of LABELING model configurations. 
In practice it helps to assign distinct, numerical LABELS to each data generating processes within an observational model?????? are we labelling or assigning values to the parameters of the data generating process????


#### Generative model in machine learning: 
 
In machine learning a generative model is typically defined as a probabilistic model of all quantities that vary from observation to observation; in other words a model over the entire observational space, Y [[1](https://betanalpha.github.io/assets/case_studies/generative_modeling.html#ref-Bishop:2006)]. For example given an observational space parameterized by two variables y=(y1,y2) the conditional model π(y1|y2;θ) would not be generative because it lacks a probabilistic model for y2. Such incomplete model specifications, often denoted _discriminative_ models, commonly arise in regression modeling where the observational space Y×X separates into variates, y∈Y, and covariates, x∈X, and only the conditional relationship π(y|x;θ) is modeled.


#### Narratively generative:
In applied statistical settings "generative" more commonly refers not to how a model is implemented but rather how the model is _interpreted_. Here generative describes models that follow the progressive structure of some assumed data generating process; in other words they model not just the outcome of a measurement but also the internal composition of that measurement. I will refer to this notion of generative as _narratively generative_.


#### _Narratively generative structure_ of a model:
In statistics and computer science causality typically refers not to all possible influences but rather to only those influences that are explicitly modeled. In any practical model we ignore an infinity of physical interactions that we assume are too weak to meaningful affect a given data generating process.


#### KL Divergence

##### Delta estimators
Unfortunately in practice we don't have all that many observations. Typically we are so starved for information that we need to aggregate most, if not all of our data into a single monolithic observation to inform sufficiently precise inferences. Consequently the most common estimators, also known as _delta estimators_, use just N=1 which results large estimation error. (from [[bayes_workflow]])

##### Holdout estimators
_Holdout estimators_ partition a single observation into two groups, one for fitting the model and one for constructing delta estimators of relative predictive performance scores. Although this avoids the bias due to reusing the same observation twice, it introduces its own bias. The problem is that inferences based on subset of the data will not, in general, be characteristic of inferences based on the entirety of the data, especially in complex models. Moreover, the log predictive density evaluated at a subset of the data will not, in general, have any relationship to the log predictive density evaluated over the full data. In other words holdout estimators implicitly estimate the predictive performance in the context of a _a smaller observation_, and we don't know how to correct that to the predictive performance of the full observation except in very simple circumstances.

##### Jackknife estimators (cross validation)
_Jackknife estimators_ average holdout estimators over many different partitions in order to reduce the variance of the delta estimators. While this averaging can be effective it does not eliminate the bias inherent to holdout estimators. Moreover the averaging requires fitting a model multiple times which can quickly exhaust any available computational resources. Jackknife estimators of any predictive performance scores, not just the particular relative predictive performance score we have been considering, are collectively known as _cross validation_ in the machine learning and statistics literature.



#### Prior predictive check

#### Prior pushforward check


#### Posterior predictive check

#### Posterior retrodiction checks
One substantial limitation of this classic residual check is that there isn't a scale that separates significant and insignificant deviations. In the context of the curve fitting model that scale is set by the assumed normal fluctuations of the observational model; deviations much smaller than σ are unresolvable from the noise while deviations much larger than σ are inconsistent with the assumed noise. **In other words these larger deviations indicate either an improbably extreme deviation or some deficiency in either the normal observational model or the shape of the best fit line.**

We can incorporate these scales into residual checks by deriving an entire predictive distribution from our best fit model,

$$
\pi_{\text{pred}}(y \mid \tilde{y})
=
\text{normal}(y \mid f(\hat{\theta}(\tilde{y}), x), \hat{\sigma}(\tilde{y})),
$$
and overlaying that against the observed data. Because the predictive distribution in this context isn't being used for making predictions of new observations but rather _retrodictions_ of an existing observation, I will refer to this comparison as a _retrodictive check_.



#### Simulation based calibration

#### Residual analysis
Classical residual analysis arises in _curve fitting models_ where observed data fluctuates around one of a family of possible curves f(x;θ) parameterized by the parameters θ,
$$
\pi(y \mid x, \theta) = \text{normal}(y \mid f(x; \theta), \sigma).
$$

Given a "best fit" configuration, θ^(y~), we can overlay the curve f(x;θ^(y~)) and the observed data y~ to investigate possible disagreements. While we can't expect that every datum will be close to the best fit curve, especially when we observe many data each with their own opportunity to fluctuate, the model presumes that these fluctuations will be _uncorrelated_. In other words any deficiency of the curve fitting model will manifest as _systematic_ deviations that persist across many values of x is the residual plot. (from [[bayes_workflow]])

### Ancestral sampling



### Fitting a model
With an algorithm locked and loaded we can proceed to _fit_, or estimate expectation values with respect to, the posterior distributions induced from each of our simulated observations,

$$
\pi_{\mathcal{S}}(\theta \mid \tilde{y}).
$$

### STAN


### JAGS

### CmdStan
`CmdStan` is the most lightweight interface closest to the core `C++` functionality. `CmdStan` consists of a series of makefiles that allow a Stan program to be compiled into a executable program within a command line environment. Algorithm output is streamed to text files which can be analyzed both during and after the running of an executable. Because `CmdStan` is so lightweight it adds little overhead to the core algorithms and consequently is especially useful in performance-limited applications. The proximity to the core libraries also means that `CmdStan` typically exposes new language and algorithm features first.

### Automatic differentiation
Critically the Stan Math Library also implements _automatic differentiation_ for all of its functions. Automatic differentiation is a technique for efficiently evaluating the exact values of the gradient of a `C++` function at a given set of inputs. This means that every Stan program defines both a target log probability density function _and_ the corresponding gradient function without any additional effort from the user. This then allows the use of extremely effective gradient-based algorithms like Hamiltonian Monte Carlo without the user having to pour through pages upon pages of analytic derivative calculations.


#### Probabilistic programming language
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













### Product distributions


### Product spaces

### Probability distributions over product spaces. 

### Conditional decomposition


### Unnormalized probability density function
they differ from the target probability density function only by a constant
$$
\bar{\pi}(x) \propto \pi(x).
$$

### Density function
**A probability density function does, however, provide sufficient information for many probabilistic computational algorithms, in particular Markov chain Monte Carlo. Given a probabilistic program that evaluates the target probability density function these algorithms can generate estimates of expectation values. In fact most of these algorithms need only _unnormalized_ probability density functions that differ from the target probability density function by only a constant,**

$$
\bar{\pi}(x) \propto \pi(x).
$$
**Consequently an even more general target for a probabilistic programming language is an unnormalized probability density function, which I will refer to from here on is as _density function_.**


