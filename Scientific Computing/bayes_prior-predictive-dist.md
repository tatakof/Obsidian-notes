#### 3.2.3.1 The Prior Predictive Distribution
One possibility is to average the data generating processes in the observational model with respect to the prior distribution. This convolution yields the _prior predictive distribution_ which is specified by the probability density function.
$$
\pi_{S}(y) = \int \mathrm{d} \theta \, 
\pi_{\mathcal{S}}(\theta) \,
\pi_{\mathcal{S}}(y \mid \theta).
$$
Note that the integrand is the probability density function that specifies the complete Bayesian model. This implies that we can equivalently derive this predictive distribution as a marginal of the complete Bayesian joint distribution,

$$
\pi_{S}(y) = \int \mathrm{d} \theta \, 
\pi_{\mathcal{S}}(y, \theta).
$$
The prior predictive distribution is most strongly influenced by those model configurations most consistent with the domain expertise encoded in the prior distribution (m'cuz theres no data'). **In other words the prior predictive distribution quantifies our best understanding of the scope of reasonable observations using only the domain expertise that we’ve introduced**. This allows us to make predictions _before_ we’ve made any observations, which is useful when we want to study how our inferences and subsequent decision making processes might play out before we probe the latent system.


In practice we typically cannot construct the prior predictive density function in closed form, but we have a few ways of generating samples from the predictive distribution. One approach is to employ ancestral sampling: first we exactly sample a model configuration from the prior distribution,

$$
\tilde{\theta} \sim \pi_{\mathcal{S}}(\theta),
$$
and then we simulate an observation from the corresponding data generating process,

$$
\tilde{y} \sim \pi_{\mathcal{S}}(y \mid \tilde{\theta} ).
$$
If we cannot exactly sample from both the prior distribution and the data generating processes in the observational model, or if we specified only the complete Bayesian model and don’t have distinct prior and observational models, then we cannot implement ancestral sampling. In that case we can run Markov chain Monte Carlo on the joint distribution to generate correlated samples from the joint distribution and then project out the sampled model configurations,

$$
\left\{ \tilde{\theta}, \tilde{y} \right\}
\rightarrow 
\left\{ \tilde{y} \right\}.
$$

Once we have prior predictive samples we can estimate prior predictive expectation values, pushforward distributions, or even further convolutions.