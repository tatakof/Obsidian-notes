### Probabilistic scholarship

Bayesian inference takes a more inclusive perspective on probability theory, **allowing it to be used to model not only frequencies but also epistemological variation and weights over the model configuration space.** Consequently we are free to use probability theory to quantify inferences within an observational model. Neighborhoods of model configurations that are more consistent with the available information would be allocated more probability, and those less consistent would be allocated less.

One immediate benefit of this approach is that is provides a much richer means of quantifying information about our model relative to the binary quantification of frequentist inference. **A probability distribution encodes much more information than a step function!**

Moreover, we don’t have to choose a probability distribution over the model configuration space arbitrarily – there is a natural procedure for updating a _prior distribution_ that encodes our domain expertise about the model into a _posterior distribution_ that identifies those model configurations consistent with both our domain expertise _and_ the observed data. Inferences, decisions, and predictions all follow from natural probabilistic operations.


A probabilistic quantification of what we know about our model would take the form of a probability distribution over the model configuration space that depends on any observed data.

![[Pasted image 20220812100613.png]]

More specifically, once we allow probability distributions over the model configuration space  (i.e. the subset of data generating processes considered in a given analysis) then the observational model (i.e. the individual data generating processes considered in an analysis and that each define a possible mathematical narrative of how the data could be generated) becomes more than just a collection of data generating processes (i.e. probability distributions over the observation space) – it becomes a _conditional probability distribution_ over the product of the observational space (i.e. ?) and model configuration space  , Y×S, that we can specify with conditional probability density functions,

$$
\pi_{\mathcal{S}}(y ; \theta) \rightarrow \pi_{\mathcal{S}}(y \mid \theta).

$$

Once we introduce a prior distribution we can apply _Bayes’ Theorem_ to invert this conditional relationship and give a posterior distribution that encodes our information about the system we’re analyzing.



### The prior distribution
[[bayes_prior]]


### The likelihood function

[[bayes_likelihood]]

### The posterior distribution
[[bayes_posterior]]


### The complete bayesian model
Given a particular prior distribution and observational model, Bayesian updating is a straightforward procedure. Unfortunately the separation between the prior distribution and observational model is not always so clear in practice.

Consider, for example, a positivity constraint on one of the model configuration parameters corresponding to, say, the positivity of physical mass. Does this constraint belong in the observational model or should it be specified as a prior distribution that assigns zero probability to negative values? The resulting posterior distribution is the same either way.

Similarly, consider a model with unobserved latent structure between the model configuration parameters θ and ϕ, πS(θ∣ϕ), such as that arising in hierarchical models and hidden Markov models. We could assume that the parameters θ corresponding to hypothetically observable but missing data and define the observation model with the conditional probability density functions

$$
\pi_{\mathcal{S}}(y, \theta \mid \phi)
=
\pi_{\mathcal{S}}(y \mid \theta) \, \pi_{\mathcal{S}}(\theta \mid \phi),
$$
and a prior distribution with the probability density function


$$
\pi_{\mathcal{S}}(\phi).
$$

At the same time we could also define an observation model that consists of only the measured data,

$$
\pi_{\mathcal{S}}(y \mid \theta),
$$

and then specify a prior distribution with the joint probability density function

$$
\pi_{\mathcal{S}}(\theta, \phi)
=
\pi_{\mathcal{S}}(\theta \mid \phi) \, \pi_{\mathcal{S}}(\phi).
$$

Each specification is slightly different – **the former presumes that the components of the model specified by the θ parameters would vary from one observation to another, while the latter presumes that those components are static across all observations.** The corresponding posterior distributions for a _single_ observation, however, are exactly the same.

**Consequently in a Bayesian analysis it can be helpful to avoid discriminating between the observational model and the prior model entirely, instead focusing on the _complete Bayesian model_.** More formally, before we observe any particular data the prior distribution and observational model define a joint distribution over the observation space and the model configuration space, Y×S, specified by the probability density function,
$$
\pi_{\mathcal{S}}(y, \theta) 
= 
\pi_{\mathcal{S}}(y \mid \theta) \, \pi_{\mathcal{S}}(\theta).
$$

This joint distribution encompasses all of our modeling assumptions and specifies the complete Bayesian model.

The joint distribution also completely specifies the posterior distribution. Evaluating the joint probability density function at an explicit observation reduces it to the corresponding posterior density function, albeit unnormalized,

$$
\begin{align*}
\pi_{\mathcal{S}}(\tilde{y}, \theta)
&=
\pi_{\mathcal{S}}(\tilde{y} \mid \theta) \, \pi_{\mathcal{S}}(\theta)
\\
&\propto 
\frac{ \pi_{\mathcal{S}}(\tilde{y} \mid \theta) }
{ \pi_{\mathcal{S}}(\tilde{y}) } 
\, \pi_{\mathcal{S}}(\theta)
\\
&\propto
\pi_{\mathcal{S}}(\theta \mid \tilde{y}).
\end{align*}
$$

Note that the constant of proportionality can also be written explicitly as an integral of the joint probability density,

$$
\pi_{\mathcal{S}}(\tilde{y})
=
\int \mathrm{d} \theta \, 
\pi_{\mathcal{S}}(\tilde{y} \mid \theta) \, \pi_{\mathcal{S}}(\theta)
=
\int \mathrm{d} \theta \, 
\pi_{\mathcal{S}}(\tilde{y}, \theta),
$$

although in practice the unnormalized posterior almost always suffices.




### Calibration
[[bayes_calibration]]