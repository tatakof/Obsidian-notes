#### 3.2 The Posterior Predictive Distribution
The other possibility is to **average** the data generating processes (m' or the likelihood???) in the observational model with respect to the posterior distribution. This convolution yields the _posterior predictive distribution_ which is specified by the probability density function.

$$
\pi_{S}(y \mid \tilde{y}) = \int \mathrm{d} \theta \, 
\pi_{\mathcal{S}}(\theta \mid \tilde{y}) \,
\pi_{\mathcal{S}}(y \mid \theta).
$$

Because the posterior predictive distribution uses the observational model twice, once to inform the posterior and again for the predictions, it requires an explicit decomposition of the complete Bayesian model into a prior model and an observational model.

The posterior predictive distribution is influenced by the model configurations consistent with not just the relevant domain expertise but also the particular data we’ve observed. This makes it ideal for informing predictions about future interactions with the latent system.

Comparisons between the posterior predictive distribution and the observed data also provide a measure of how well our model approximates the latent system. Although we can’t explicitly form these comparisons in practice, _estimates_ of these comparisons form the basis of all predictive model validation procedures, including information criteria and cross validation


As with the prior predictive density function, the posterior predictive density function is rarely available in closed form. If we have already generated posterior samples, say through a Markov chain Monte Carlo fit, then we can generate posterior predictive samples, y~′, through ancestral sampling,
$$
\begin{align*}
\tilde{\theta} &\sim \pi_{\mathcal{S}}(\theta \mid \tilde{y})
\\
\tilde{y}' &\sim \pi_{\mathcal{S}}(y \mid \tilde{\theta} ).
\end{align*}
$$



















