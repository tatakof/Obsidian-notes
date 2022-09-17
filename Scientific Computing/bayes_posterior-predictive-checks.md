statistical rethinking 2nd edition

"Posterior predictive checks combine uncertainty about parameters, as described by the posterior distribution, with uncertainty about outcomes, as described by the assumed likelihood function.  These checks are useful for verifying that your software worked correctly. They are also useful for prospecting for ways in which your models are inadequate"


------------------------------------
https://stats.stackexchange.com/questions/115157/what-are-posterior-predictive-checks-and-what-makes-them-useful
Posterior predictive checks are, in simple words, "simulating replicated data under the fitted model and then comparing these to the observed data" ([Gelman and Hill, 2007, p. 158](http://www.stat.columbia.edu/~gelman/arm/)). So, you use posterior predictive to "look for systematic discrepancies between real and simulated data" ([Gelman et al. 2004, p. 169](http://www.stat.columbia.edu/~gelman/book/)).




Posterior predictive checks are helpful in assessing if your model gives you "valid" predictions about the reality - do they fit the observed data or not. It is a helpful phase of model building and checking. It does not give you a definite answer on if your model is "ok" or if it is "better" then other model, however, it can help you to check if your model makes sens.

This is nicely described in **LaplacesDemon** vignette [_Bayesian Inference_](https://cran.r-project.org/web/packages/LaplacesDemon/vignettes/BayesianInference.pdf):

"Comparing the predictive distribution $yrep$ to the observed data $y$ is generally termed a "posterior predictive check". This type of check includes the uncertainty associated with the estimated parameters of the model, unlike frequentist statistics.

Posterior predictive checks (via the predictive distribution) involve a double-use of the data, which violates the likelihood principle. However, arguments have been made in favor of posterior predictive checks, provided that usage is limited to measures of discrepancy to study model adequacy, not for model comparison and inference (Meng 1994).

Gelman recommends at the most basic level to compare $yrep$ to $y$, looking for any systematic differences, which could indicate potential failings of the model (Gelman et al. 2004, p. 159). It is often first recommended to compare graphical plots, such as the distribution of $y$ and $yrep$.""


----------------------------------------------

## Betancourt (he calls them posterior retrodictive checks)

### 1.4.3 Posterior Retrodiction Checks

Although relative predictive performance scores don't ultimately provide a useful tool for model criticism, their derivation does highlight some of the properties we need in a such a tool.

Firstly, we cannot compare a predictive distribution to the true data generating process without, well, already knowing the true data generating process. If we did know the true data generating process then modeling would be completely gratuitous! **In a practical analysis where we don't already know the truth we have to rely on the only manifestation of the true data generating process available: the observed data itself. Consequently any practical model criticism will be limited to comparing a predictive distribution to an observation.**

Secondly, it's difficult to construct a useful quantitative comparison without knowing exactly what deviant behavior we want the comparison to probe. In practice it's often more useful to exploit visual, qualitative comparisons that can exhibit many deviant behaviors at the same time. By focusing on _exploring_ potential limitations instead of explicitly _testing_ for them we can build more flexible methods better equipped for the elaborate model failures that we'll often encounter in practice.

In other words we really want methods to visually compare a predictive distribution to the observed data that can effective display many possible deviant behaviors all at the same time. Fortunately such methods are already ubiquitous in _residual analysis_.

Classical residual analysis arises in _curve fitting models_ where observed data fluctuates around one of a family of possible curves f(x;θ) parameterized by the parameters θ,
$$
\pi(y \mid x, \theta) = \text{normal}(y \mid f(x; \theta), \sigma).
$$
Given a "best fit" configuration, θ^(y~), we can overlay the curve f(x;θ^(y~)) and the observed data y~ to investigate possible disagreements. While we can't expect that every datum will be close to the best fit curve, especially when we observe many data each with their own opportunity to fluctuate, **the model presumes that these fluctuations will be _uncorrelated_**. **In other words any deficiency of the curve fitting model will manifest as _systematic_ deviations that persist across many values of x is the residual plot.**

For example consider the following residual plot. The scatter of the observed data around the best fit curve seems reasonably uncorrelated. **This doesn't mean that the best fit curve is correct, just that we can't resolve any deviant behavior.**

![[Pasted image 20220916104837.png]]

On the other hand this other residual plot exhibits strong systematic deviations. The data at central values of x are all lower than the best fit line while the data at the peripheral values of x are all higher.

![[Pasted image 20220916104929.png]]


  

One substantial limitation of this classic residual check is that there isn't a scale that separates significant and insignificant deviations. In the context of the curve fitting model that scale is set by the assumed normal fluctuations of the observational model; deviations much smaller than σ are unresolvable from the noise while deviations much larger than σ are inconsistent with the assumed noise. **In other words these larger deviations indicate either an improbably extreme deviation or some deficiency in either the normal observational model or the shape of the best fit line.**

We can incorporate these scales into residual checks by deriving an entire predictive distribution from our best fit model,

$$
\pi_{\text{pred}}(y \mid \tilde{y})
=
\text{normal}(y \mid f(\hat{\theta}(\tilde{y}), x), \hat{\sigma}(\tilde{y})),
$$
and overlaying that against the observed data. Because the predictive distribution in this context isn't being used for making predictions of new observations but rather _retrodictions_ of an existing observation, I will refer to this comparison as a _retrodictive check_.

By using the entire predictive distribution we can now be fairly confident that there are no deviations in the first example above, at least none beyond what is already expected from the assumed observational model

![[Pasted image 20220917101248.png]]

Likewise the predictive distribution establishes the extremity of the deviation seen in the second example. We can now use the shape of the deviation to suggest improvements to the best fit predictive distribution, for example a better choice of curve or perhaps a more flexible family of curves entirely.

![[Pasted image 20220917101525.png]]

Predictive distributions quantify how well we can resolve features in the data, and hence the manifestations of any deficiencies of the assumed model.

Once we embrace this retrodictive aspect residual analysis naturally generalizes to Bayesian inference. The _posterior predictive distribution_

$$
\pi_{\mathcal{S}}(y \mid \tilde{y})
=
\int \mathrm{d} \theta \,
\pi_{\mathcal{S}}(\theta \mid \tilde{y}) \, \pi_{\mathcal{S}}(y \mid \theta),
$$
**reduces the entire Bayesian model to a single predictive distribution by averaging all of the data generating process in the observational model over the inferred posterior distribution, quantifying all of the predictions consistent with both our domain expertise and the observation, y~. By using the posterior predictive distribution to make retrodictions we incorporate all of our inferential uncertainty, not just a best fit point estimate, and define meaningful scales for disagreements with the observed data regardless of the structure of the model.**

The only obstruction to generalizing retrodictive residual analysis to Bayesian inference is working out how to visually compare the posterior predictive distribution to observed data, especially when the observational space is high-dimensional.

**While we can't easily visualize the entire predictive distribution at once, we can construct a collection of powerful visualizations by projecting to subspaces of the observational space that isolating particular consequences of our retrodictions that highlight potential limitations. Fortunately we've already considered how to isolate the features of the observation space relevant to our scientific questions when we were motivating summary statistics we for prior predictive checks! In other words we can reuse those summary statistics to construct _posterior retrodictive checks_ that visually compare the pushforwards of the posterior predictive distribution,** $\pi_{t(Y) \mid Y}(t \mid \tilde{y})$, to the observed summary statistic, $t(\tilde{y})$.

If the observed summary statistic, here shown in black, falls within the bulk of the pushforward distribution, here shown in dark red, then there are no indications that our model is doing an inadequate job of modeling the particular behaviors captured by the summary statistic.

![[Pasted image 20220917111055.png]]

When the observed summary statistic falls in the tails of the pushforward distribution, however, the situation is not so clear.

![[Pasted image 20220917111114.png]]

**As in the curve fitting context we can't discriminate between our observation being a rare but not impossible fluctuation and our model being insufficiently sophisticated to capture the structure of the true data generating process that manifests in the given summary statistic.** All we can do is fall back to our domain expertise and hypothesize about the nature of any systematic deviations and the possible model improvements--improvements spanning all of the phenomenological, environmental, and experimental effects that could manifest in the true data generating process--that could account for those deviations. **Most of the time the tension between the posterior predictive distribution and the observed data seen in a retrodictive check is due to not modeling a loose cable in our detector. Sometimes it's because of the breakdown of Newtonian mechanics into special relativity.**

In practice we typically can't construct explicit posterior predictive density functions, let alone various pushforward density functions. We can, however, readily approximate pushforwards of the posterior predictive distribution with samples. Specifically we can generate posterior predictive samples

$$
\tilde{y}' \sim \pi_{\mathcal{S}}(y \mid \tilde{y})
$$
by sequentially sampling from the posterior and then the corresponding data generating process,
$$
\begin{align*}
\tilde{\theta} \sim \pi_{\mathcal{S}}(\theta \mid \tilde{y})
\\
\tilde{y}' \sim \pi_{\mathcal{S}}(y \mid \tilde{\theta})
\end{align*}
$$
and then generate pushforward samples by applying the corresponding summary statistic,
$$
t(\tilde{y}') \sim \pi_{t(Y) \mid Y}(t \mid \tilde{y}).
$$

**(m'this i dont get)**

This allows us to, for example, construct visual posterior retrodictive checks pushforward with histograms.

![[Pasted image 20220917111753.png]]

Often systematic deviations are easier to see with multidimensional summary statistics. For example we might want to analyze how retrodictive agreement varies with some auxiliary variable, x, as in the curve fitting example. In this case we might construct quantile ribbons for sequential bins of x and plot them all at the same time.

![[Pasted image 20220917112358.png]]

  

Residual analysis is ubiquitous in the applied sciences. For a review of more formal residual analysis techniques in the frequentist setting see [[8](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#ref-BoxEtAl:2005)]. Posterior retrodictive analysis was considered by [[1](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#ref-Good:1983)] but posterior retrodictive checks, also known as posterior predictive checks, became practical only when simulation tools became widely available in applied statistics [[9](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#ref-Rubin:1984)].


### 1.4.4 Limitations of Posterior Retrodiction Checks
Posterior retrodictive checking is an extremely powerful technique for investigating the adequacy of a model in the context of a given observation, but that context introduces some important limitations.

**By using the same observation to both inform and evaluate the posterior predictive distribution, posterior retrodictive checks assess only the self-consistency of the model at that particular observation. In particular they do not assess how well the assumed Bayesian model might perform with other observations, and hence they provide only a very narrow view on the compatibility of the model and the entire true data generating process.**

If we are worried that the qualitative predictive performance in the context of a given observation is not characteristic of other possible observations then we can always generalize posterior retrodictive checks to proper _posterior predictive checks_ against other observations. In other words we can use one observation y~1 to inform the posterior distribution, and hence the posterior predictive distribution, and a second, independent observation y~2 to evaluate. A posterior predictive distribution consistent with both observations exhibits no problems, while one consistent with the first but not the second indicates that the predictive performance may be sensitive to the structure of the first observation.

![[Pasted image 20220917115244.png]]

This might, for example, but due to an overly flexible model overfitting to y~1. At the same time it could also be a consequence of y~1 manifesting misfit less clearly than y~2, or even y~2 being an unlikely tail event. Identifying which requires followup investigations.

**Even if the posterior predictive distribution is compatible with all possible observations, however, that only implies that we have adequately modeled the true data generating process _for a given experiment_. That does not necessarily imply that any of the components of our model will generalize to other experiments.**

**A particular data generating process encompasses only the phenomena and surrounding environment that interact with a given experimental probe, and predictive evaluations identify deficiencies in only that context and only up to the resolution of that probe.** **A phenomenological model that is adequate for one experiment, for example, may be inadequate for another experiment that is sensitive to different latent phenomena or different behaviors in the surrounding environment. At the same time a model that is adequate for one measurement may be insufficient for repeated measurements that that allow us to better resolve the entire data generating process. Or repeated measurements might just provide more opportunity for the expected expected experimental design to be violated, introducing more structure that has to be modeled.**

All we can do in practice is investigate deficiencies of our model in the very narrow context of a given experiment. How that model, and inferences within the scope of that model, generalize beyond that narrow context is a scientific question and not a statistical one. [[8](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#ref-BoxEtAl:2005)] analogized an experiment as a narrow window through which we can view of the latent phenomenology and its surrounding environment. In reality this view is further limited by the resolution of our model -- in other words we're looking through a dirty window that admits only a fuzzy view. That obscured view fundamentally limits not only how well we can learn about the latent system but also well we can assess the adequacy of a model of that system.

