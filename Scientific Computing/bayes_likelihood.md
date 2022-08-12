If we specify the observational model with a family of probability density functions over the observational space, πS(y∣θ), then the evaluation of those probability density functions at a specific observation, y~, defines a _likelihood function_,
$$
\begin{alignat*}{6}
l_{\tilde{y}} :\; &\Theta& &\rightarrow& \; &\mathbb{R}^{+}&
\\
&\theta& &\mapsto& &\pi_{\mathcal{S}}(\tilde{y} \mid \theta)&.
\end{alignat*}
$$

**The likelihood function maps each model configuration to a numerical quantification that increases for model configurations that are more consistent with the specific observation and decreases for those model configurations that are less consistent. In other words, the likelihood function quantifies the relative consistency of each model configuration with the observed data.**

**Formally these likelihood evaluations provides only _relative_ information – the absolute likelihood value depends on how we parameterize the observation space and hence doesn’t have any well-posed meaning. Indeed from the Bayesian perspective it’s not the likelihood function that quantifies consistency with an observation but rather the _likelihood ratio_.** Those not interested in the technical details should skip the rest of this section.

Given a prior distribution and an observational model we can define a marginal probability distribution over the observation space,

$$

\pi_{\mathcal{S}}(y)
=
\int \mathrm{d} \theta \, 
\pi_{\mathcal{S}}(\tilde{y} \mid \theta) \, \pi_{\mathcal{S}}(\theta).

$$

The likelihood ratio is then defined as the Radon-Nikodym derivative of the distributions in the observational model with respect to this marginal probability distribution,

$$
\mathcal{L}(\tilde{y}; \theta) 
=
\frac{ \mathrm{d} \pi_{\mathcal{S} \mid \tilde{y}} }
{ \mathrm{d} \pi_{\mathcal{S}} } (\theta)
=
\frac{ \pi_{\mathcal{S}}(\tilde{y} \mid \theta) }
{ \pi_{\mathcal{S} (\tilde{y}) }.
}

$$

**The likelihood ratio defines a numerical quantification of data consistency that, unlike the likelihood function, is independent of how we parameterize the observational space.**

**That said, the only difference between a likelihood function corresponding to a given parameterization of the observational space and the likelihood ratio is a constant that depends only on the observed data and not the model configurations. An arbitrary likelihood function and the likelihood ratio give the same relative quantifications of consistency. Because in typical practice we need only relative consistency to form well posed inferences, the difference between a likelihood function and the likelihood ratio is usually irrelevant.**

