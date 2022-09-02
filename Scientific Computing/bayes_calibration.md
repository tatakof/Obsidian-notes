## 3.3 Bayesian Calibration
Ideally the true data generating process, or at least the best approximation to it within our observational model, would fall into a neighborhood of high posterior probability. That accuracy would ensure that whatever conclusions we draw from our model, in particular the decisions informed by those inferences, would be faithful to the real latent system being analyzed.

In general, however, there are no such guarantee in Bayesian inference. The posterior distribution naively follows the information encoded in the model and the observation. Without a carefully designed model the posterior distribution is vulnerable to being led astray by irrelevant quirks in a given observation, ending up far away from the desired model configurations.
Bayesian inference provides a procedure for constructing inferences but it offers no general guarantees on the overall behavior of those inferences. If we want to ensure robust inferences then we at least need to attempt some _calibration_ in order to determine how we expect our model to perform.

Following [Section 1.3.3](https://betanalpha.github.io/assets/case_studies/modeling_and_inference.html#sec:model_based_calibration) we might consider inferential outcomes of our model that take the form of a decision-making process, a(y). For example, we could consider a(y) as a particular property of the posterior distribution, or the outcome of Bayesian decision making process. In that case a utility function U(a(y),θ) provides a calibration for a specific observation and model configuration. We can then use the data generating process corresponding to a given model configuration to extend that calibration across possible observations, but so far we’ve had limited ways of extending the calibration across the unspecified model configuration. For example, in the frequentist setting we were limited to calibrations based on worst case expected utility.

In a Bayesian analysis we can use the joint distribution corresponding to the complete Bayesian model to account for both the unknown observation _and_ the unknown model configuration. We can push the joint distribution through the utility function to construct an entire probability distribution of potential outcomes, πS(U),

![[Pasted image 20220818113444.png]]
and then define calibrations such as expected utilities,
$$
\overline{U}_{\mathcal{S}} = \int \mathrm{d} y \, \mathrm{d} \theta \,
\pi_{\mathcal{S}} (y, \theta) \,
U(a(y), \theta).
$$

In practice we can implement this calibration by sampling from the joint distribution and then evaluating the utility function,

$$
\begin{align*}
\tilde{\theta} &\sim \pi_{\mathcal{S}}(\theta)
\\
\tilde{y} &\sim \pi_{\mathcal{S}}(y \mid \tilde{\theta} )
\\
\tilde{U} &= U(a(\tilde{y}), \tilde{\theta}).
\end{align*}
$$

m' so sampling from the joint is the same as sampling from the prior and then the likelihood cuz the joint equals the conditional and the marginal?'

Put in words, we can calibrate a Bayesian analysis by repeatedly simulating model configurations from the prior distribution, observations from the corresponding data generating process, running our analysis to completion, and then scrutinizing the resulting likelihood functions, posterior distributions, and decision outcomes in the context of the simulated ground truth.

The conclusions we draw from these calibrations will always be limited by the quality of the complete Bayesian model. If we are not confident that our observational model reasonably approximates the true data generating process, or that our prior model encodes sufficient domain expertise to regularize any misbehaving likelihood functions, then of what use are these calibrations? In practice these calibrations serve as a way of _bootstrapping_ model development. Starting with an initial crude model we can use these calibrations to identify the limitations of that model and inform improvements such as more sophisticated observational models, more precise domain expertise, or even more robust methods for computing expectations. This information is critical to [a _principled Bayesian workflow_ for model development](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html).

At the same time, the complete Bayesian model used for constructing the calibration simulations doesn’t have to be the same model used to construct our inferences. We can, for example, use a more sophisticated, and possibly more expensive, model to calibrate a more approximate model that we aim to employ in a given application. Indeed this use of multiple models is not uncommon in scientific practice.

Bayesian calibration is surprisingly general, and it spans a wide range of useful analyses. Here I introduce just a few of the techniques that fall under this general approach.

### 3.3.1 Calibrating Predictions
One immediate application is the study of the simulated data itself, which we can equivalently think of as samples from the prior predictive distribution. Tension between the behavior of this simulated data and our expectations indicates that our prior model needs to integrate more domain expertise.

This _prior predictive check_ has a long history in Bayesian inference, going all the way back to Good’s “device of imaginary results” [[12](https://betanalpha.github.io/assets/case_studies/modeling_and_inference.html#ref-Good:1950)]. A natural extension is to study not just the simulated data but also the behavior of the resulting likelihood functions, inspecting for poor identification that might require more domain expertise.


### 3.3.2 Calibration Posterior Behaviors
Studying the properties of potential posterior distributions resulting from these calibration simulations allows us to identify common pathologies, such as overfitting and poor identifiability, that limit the utility of any resulting inferences. In addition to evaluating specific decision making processes we can also study the more general properties that can identify suspicious behavior.

For example, if θ~ is the true model configuration then we can quantify how closely the posterior distribution is to the true model configuration with the _z-score_ for each parameter,

$$
z = \frac{ \mathbb{m}_{\mathrm{post}} - \tilde{\theta} }
{ \sqrt{ \mathbb{V}_{\mathrm{post}} } },
$$
were mpost is the marginal posterior mean and Vpost is the marginal posterior variance. Smaller z-scores indicate that the posterior distribution concentrates around the true model configuration while larger values indicate concentration away from the true model configuration.

At the same time the _contraction_ of a given parameter,
$$
c = 1 - \frac{ \mathbb{V}_{\mathrm{post}} }
{ \mathbb{V}_{\mathrm{prior}} }
$$
provides one possible quantification for how much the posterior is influenced by the information encoded in the observed likelihood function. Contraction near zero indicates that the simulated data provided little information beyond the domain expertise encoded in the prior distribution, while contraction near one indicates a likelihood function that strongly informs that parameter.

Conveniently, these two posterior expectations are sensitive to an array of pathological behavior that can compromises our inferences. The ideal behavior concentrates towards strong contraction and small z-scores, indicating a posterior distribution that strongly concentrates around the true model configuration. A posterior distribution with strong contraction and a large z-score, however, indicates a model that overfits to irrelevant structure of the simulated data and is unable to accurately recover the true model configuration. Similarly a posterior distribution with weak contraction and a small z-score indicates a model that is poorly informed by the simulated data. Finally a posterior distribution with weak contraction and a large z-score indicates a fit where the likelihood function and prior distribution disagree with each other.

![[Pasted image 20220818131934.png]]

Consider, for example, this output from simulations using a simple regression model. Each point records the z-score and contraction of the posterior distribution derived from one of the simulations from the complete Bayesian model.


![[Pasted image 20220818131952.png]]

We see that most of the resulting posterior distributions are reasonably well-behaved with small z-scores and moderate contraction. Occasionally, however, the posterior distribution chases some irrelevant structure in the data resulting in strong contraction and much larger z-scores. This indicates that are model isn’t quite as robust as we might hope, and it has the nasty habit of being its most confident exactly when it’s the most wrong.

### 3.3.3 Calibrating Posterior Computation
We can even use Bayesian calibration to quantify how faithfully our computational tools represent the models that they’re fitting.

As we fit each posterior distribution for each simulated observation we can evaluate the computational performance. At a very high level we can see if it even successfully ran to completion, if it never finished within a reasonable time frame, or if it encountered a software failure due to bugs, exhausted memory resources, and the like. Going further we can evaluate any self-diagnostics in completed fits, such as the potential scare reduction factor for general Markov chain Monte Carlo algorithms or divergences and energy fractions of missing information in Hamiltonian Monte Carlo. If our tool proves robust to all of the potential posterior distribution behaviors across the simulated observations then we have some assurance that it should perform well enough for any real observations, at least if our model is sufficiently accurate.

What can we do, however, if our computational tool isn’t self-diagnostic? Fortunately Bayesian inference provides a subtle consistency property that allows us to check _any_ method capable of generating posterior samples.

Regardless of our particular model, averaging the posterior distributions fit from observations simulated from the prior predictive distribution will _always_ recover the prior distribution,

$$
\pi_{\mathcal{S}}(\theta') 
= 
\int \mathrm{d} y \, \mathrm{d} \theta \,
\pi_{\mathcal{S}} (\theta' \mid y) \, \pi_{\mathcal{S}} (y, \theta).
$$

In particular this implies that the ensemble of posterior samples, θ~′,

$$
\begin{align*}
\tilde{\theta} &\sim \pi_{\mathcal{S}}(\theta)
\\
\tilde{y} &\sim \pi_{\mathcal{S}}(y \mid \tilde{\theta})
\\
\tilde{\theta}' &\sim \pi(\theta \mid \tilde{y}),
\end{align*}
$$

will follow the same distribution as as the incident samples from the prior distribution, θ~. Any deviation between the two samples indicates that either our simulations are incorrect, our fit is using an inconsistent model from the simulations, or that our computational tool is generating biased samples.

_Simulated-based calibration_ [[13](https://betanalpha.github.io/assets/case_studies/modeling_and_inference.html#ref-TaltsEtAl:2018)] compares the ensemble posterior sample and the prior sample using _ranks_. For each simulated observation we generate R samples from the corresponding posterior distribution,

$$
\begin{align*}
\tilde{\theta} &\sim \pi_{\mathcal{S}}(\theta)
\\
\tilde{y} &\sim \pi_{\mathcal{S}}(y \mid \tilde{\theta})
\\
(\tilde{\theta}'_{1}, \ldots, \tilde{\theta}'_{R}) 
&\sim \pi(\theta \mid \tilde{y}),
\end{align*}
$$

and compute the rank of the prior sample within the posterior samples, i.e. the number of posterior samples larger than the prior sample,

$$
\rho = \sharp \left\{ \tilde{\theta} < \tilde{\theta}'_{r} \right\}.
$$
If the ensemble posterior sample and the prior sample are equivalent then these ranks will be uniformly distributed. The uniformity of the ranks itself is straightforward to analyze visually by histogramming the ranks for each parameter in the model configuration space.

![[Pasted image 20220819094304.png]]

Here the grey band demonstrates the expected variation of ranks distributed according to an exact uniform distribution. Deviation outside of these bands, especially systematic deviation of many bins at once, indicates computational problems. See [[13](https://betanalpha.github.io/assets/case_studies/modeling_and_inference.html#ref-TaltsEtAl:2018)] for further discussion of common systematic deviations and their interpretations.

