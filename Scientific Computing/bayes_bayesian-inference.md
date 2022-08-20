### Questions
- The key step in _implementing_ a Bayesian analysis is _evaluating_ the posterior expectation values for whatever functions are deemed relevant to the analysis. (m' what does he mean here with functions????????'')



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

This joint distribution encompasses all of our modeling assumptions and specifies the complete Bayesian model. (m' i believe this is from where we make a prior predictive check')

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

One benefit of this joint perspective is that it facilitates model development. Once we separate the model configuration space into phenomenological, environmental, and probe parameters, for example, the full model can be decomposed into a sequence of conditional distributions that follows the generative structure of the true data generating process

$$
\begin{align*}
\pi_{\mathcal{S}}(y, \theta) 
=& \;\;\;
\pi_{\mathcal{S}}(y, \theta_{\text{phenom}}, \theta_{\text{envir}}, \theta_{\text{probe}}) 
\\
=& \;\;\;
\pi_{\mathcal{S}}(y \mid \theta_{\text{phenom}}, \theta_{\text{envir}}, \theta_{\text{probe}}) 
\\
& \cdot \pi_{\mathcal{S}}(\theta_{\text{probe}} \mid \theta_{\text{phenom}}, \theta_{\text{envir}}) 
\\
& \cdot \pi_{\mathcal{S}}(\theta_{\text{envir}} \mid \theta_{\text{phenom}}) 
\\
& \cdot \pi_{\mathcal{S}}(\theta_{\text{phenom}}).
\end{align*}
$$


Using this generative decomposition as scaffolding to construct the complete Bayesian model not only facilitates the development of coherent yet sophisticated models but also allows different parts of the model to be isolated and modeled separately. This can be hugely beneficial when the development is being done by a large team or collaboration and not any one individual.

Another benefit of the complete Bayesian model is that is it illuminates the _interaction_ of the prior distribution and the likelihood functions for possible observed data. As discussed in [Section 3.1.1](sec:prior), this interaction is crucial for determining the amount of domain expertise that we need to encode in the prior distribution, and hence critical for principled model building.


For example, if the likelihood functions derived from reasonable observations typically concentrate in a small neighborhood of the model configuration space then they will dominate the shape of the posterior density function and we get contractive behavior,

![[Pasted image 20220817111330.png]]

In this case the information encoded in the posterior distribution is governed almost entirely by what we learn from the observation. Even vague priors are sufficient for useful inferences and we don’t have to spend much time interrogating our own domain expertise.

The possible likelihood functions, however, aren’t always so well-behaved. In particular, our probe might not be sufficiently sensitive to the phenomena of interest at the scales approximated by the observational model. In that case the observational model is said to be _weakly-identified_ and the likelihood functions tend to disperse over expansive regions of the model configuration space for most, if not all, observations. 

In circumstances like these the form of the posterior distribution is strongly influenced by the form of the prior distribution; a careless prior distribution will allow the weak identification of the observational model to propagate to the posterior distribution.

In order to compensate for the possibility of diffuse likelihood functions we need the prior distribution to incorporate at least a soupçon of domain expertise. At the very least we want the prior distribution to suppress extreme, although not entirely impossible, model configurations to ensure containment behavior in the Bayesian updating.


![[Pasted image 20220817111603.png]]

Specifying prior distributions that are robust to possible pathologies in the likelihood functions derived from the observational model is key to robust analyses. This specification is itself greatly facilitated by not modeling the prior distribution and observational model independently but rather together through the development of a complete Bayesian model.

## 3.2 Employing Our Education
Bayes’ Theorem ensures that any information learned by our model is encoded in the posterior distribution. Consequently any inferential query we might pose must be answered with only valid manipulations of the posterior distribution. In probability theory, however, all valid manipulations take the form of the evaluation of expectation values or the construction of pushforward distributions. This seemingly limited set of inferential outputs provides a rich diversity of applications.

### 3.2.1 Making Inferences

Most inferences take the form of posterior _expectation values_ of certain functions. In other words, the question we ask is encoded in a real-valued function over the model configuration space, g:Θ→R, and the corresponding answer is given by the corresponding posterior expectation value,
$$
\mathbb{E} [ g(\theta) ]
=
\int \mathrm{d} \theta \, \pi_{\mathcal{S}}(\theta \mid \tilde{y}) \,
g(\theta).
$$

For example we might ask _where_ in the model configuration space our posterior concentrates. We can answer this with posterior means or even posterior medians, which are derived from the difference of expectation values. Similarly the _breadth_ of this concentration can be quantified by posterior standard deviations or perhaps posterior tail quantiles. More sophisticated questions are answered with expectation values of more sophisticated functions.

The key step in _implementing_ a Bayesian analysis is _evaluating_ the posterior expectation values for whatever functions are deemed relevant to the analysis. (m' what does he mean here with functions????????'')



If the posterior density can be worked out analytically then certain expectation values are given exactly.

Even with a closed-form posterior density function, however, the expectation value of more sophisticated functions will not always be available analytically. Moreover, closed-form posterior density function rely on very simple models and hence are unrealistic in all but the simplest applications. In practice we instead rely on probabilistic computational methods to _approximate_ various posterior expectation values. Markov chain Monte Carlo, for example, is a paramount technique which can consume the joint density function that specifies the complete Bayesian model and return estimates of posterior expectations along with quantifications of the estimator errors.


The term “fit” is often used to colloquially denote statistical computation, derived from a time when statistical computation reduced to finding a single model configuration that best fit the observed data. These days statistical computation is much more complex and careless use of the term promotes confusion. Obtaining a normalized posterior density function, for example, _cannot_ be the entirety of a Bayesian fit because it is useful for evaluating at best only some expectation values. A proper Bayesian fit is instead the computation, or more realistically estimation, of _all_ expectation values relevant to a given application. Equivalently one might define a Bayesian fit as the generation of intermediate objects, such as posterior samples, that can be used after the fact to estimate any expectation value.

### 3.2.2 Making Decisions

The posterior distribution also provides a formal means for the robust decision making that originally motivated our foray into statistical inference.

As we saw in [Section 1.3.3](https://betanalpha.github.io/assets/case_studies/modeling_and_inference.html#sec:model_based_calibration) a model-based utility function

$$
\begin{alignat*}{6}
U:\; &A \times \Theta& &\rightarrow& \; &\mathbb{R}^{+}&
\\
&(a, \theta)& &\mapsto& &U(a, \theta)&.
\end{alignat*}
$$

isn’t immediately applicable for informing decisions because of the dependence on the unknown model configuration. In a Bayesian analysis, however, the posterior distribution quantifies the relevance of each possible model configuration. Consequently we can compute _expected utilities_ as posterior expectation values,

$$
\overline{U}(a, \tilde{y}) = 
\mathbb{E}_{ \pi_{\mathcal{S}}(\theta \mid \tilde{y}) } [ U(a, \theta) ]
=
\int \mathrm{d} \theta \, \pi_{\mathcal{S}}(\theta \mid \tilde{y}) \,
U(a, \theta).
$$
Note the implicit dependence on the observation due to its influence on the posterior distribution.

The optimal decision _in the context of the available information_ is then given by taking the action that maximizes these expected utilities. This defines the _Bayesian decision making process_
$$
a^{*}(\tilde{y}) = \underset{a \in A}{\text{argmax}} U(a, \tilde{y}).
$$
Mathematically Bayesian decision theory is straightforward and a natural consequence of using probability theory to quantify information. At the same time it can be a conceptual paradigm shift for many because of its explicit consideration of the _uncertainty_ inherent in our inferences. Indeed many common fallacies arise from ignoring inferential uncertainty, or presuming models that poorly approximate the true data generating process. Going through the steps of developing a Bayesian model and computing expected utilities is a powerful way of avoiding common mistakes and facilitating more robust decisions.

For example, let’s say that our goal is to report a point summary of the posterior distribution, θ^, and we want that summary to minimize the squared difference to the best model configuration. In that case the utility function would take the form

$$
U(\hat{\theta}, \theta)
=
- (\hat{\theta} - \theta)^{2}.
$$
and the expected utility would become
$$
\begin{align*}
\overline{U}(\hat{\theta}, \tilde{y}) 
&= 
\int \mathrm{d} \theta \, \pi_{\mathcal{S}}(\theta \mid \tilde{y}) \,
U(\hat{\theta}, \theta)
\\
&= -
\int \mathrm{d} \theta \, \pi_{\mathcal{S}}(\theta \mid \tilde{y}) \,
(\bar{\theta} - \theta)^{2}
\\
&=
- (\hat{\theta} - \mathbb{m}(\tilde{y}))^{2}
- \mathbb{V}{\tilde{y}},
\end{align*}
$$
where m(y~) is the posterior mean and V(y~) is the posterior standard deviation. This expected utility is maximized when we report the posterior mean, which defines the optimal point summary,
$$
\hat{\theta}^{*} = \mathbb{m}(\tilde{y}).
$$

A more elaborate circumstance might consider how to optimally dose a new medication. Strong doses might be more effective, but they also suffer from increased, possibly even lethal, side effects. Weaker doses are safer but may not be sufficiently effective at treating a disease. The overall utility of a given dosing will then depend on how the medication interacts with the physiology of a patient, or typically the expected population of patients that might receive this treatment. With a sufficiently sophisticated model we can infer these interactions, compute the expected utility of each action, and then make our decision about how best to dose the treatment.

Bayesian decision theory is a powerful framework but it strives only to make an optimal decision in the context of the available information. There is no guarantee that the resulting decision-making process will perform well across the range of observations distributed according to the true data generating process. For that we need to go one step further and _calibrate_ our decision-making process over some incidence of reasonable observations.





### 3.2.3 Making Predictions

**If the latent observational process is stationary then predictions for future observations are no different from post hoc predictions of the observed data. In particular, predictions are straightforward to make given a particular model configuration; the predictive distribution is simply the corresponding data generating process.**

In Bayesian inference we could isolate a single model configuration with a carefully designed expectation value, such as the posterior mean for each parameter. That isolation, however, would prevent us from utilizing all of the information available to our model. Instead we can construct predictions sensitive to _all_ of the possible model configurations by convolving a probability distribution over the model configuration space with each of the possible data generating processes. Those configurations allocated more probability will then more strongly influence the resulting predictive distribution relative to those allocated less probability.


Because we have two natural probability distributions over the model configuration space available in Bayesian inference, the prior distribution and posterior distribution, we have two natural predictive distributions.


#### 3.2.3.1 The Prior Predictive Distribution
[[bayes_prior-predictive-dist]]


#### 3.2.3.2 The Posterior Predictive Distribution

[[bayes_posterior-predictive-dist]]




## 3.3 Bayesian Calibration
[[bayes_calibration]]





# 4 Comparing Asymptotic Apples to Preasymptotic Oranges
[[bayes_asymptotics]]




# 5 Conclusion

Bayesian inference is a versatile methodology for fusing information from observations and domain expertise into coherent inferences and decision-making processes. The probabilistic foundations of the methodology ensure that the mechanisms for evaluating, analyzing, and criticizing inferences are all implemented by natural operations in probability theory.

Conceptually this makes Bayesian computation particularly well-suited to automation once a complete Bayesian model has been specified. In practice automated computation can’t quite be realized, but with the careful utilization of modern tools we can get impressively close. At the same time, carefully designed probabilistic programming languages provide the means for practitioners to specify the broad extent of models that arise in applications.

Together probabilistic programming and state-of-the-art Bayesian computational methods provide a platform for implementing Bayesian inference in practice. In particular, their combination is the basis for Stan [[14](https://betanalpha.github.io/assets/case_studies/modeling_and_inference.html#ref-Stan:2018)].
















