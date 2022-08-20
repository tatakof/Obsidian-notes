So far our discussion of frequentist and Bayesian inference has neglected a ubiquitous, and often abused, concept that completely changes the discussion of how we implement inference in practice: _asymptotics_. In this final section let’s use what we’ve learned so far as a foundation on which we can properly introduce asymptotics and discuss its practical limitations.

Consider an observation comprised of many identical and independently generated components, y={y1,…,yN} with the total observation space defined as the product of each component observation space $\times_{n = 1}^{N} Y$

As the number of these components, N

, grows our observation should assimilate more information. Eventually only those model configurations that closely approximate the true data generating process should have any chance of being inferred as consistent with the observation. In other words, the likelihood function should concentrate around the true data generating process, at least if it’s contained within the observational model.

At the same time, when we consider an observation with an increasing number of components the idiosyncratic properties of any particular component observation should average out. How the likelihood function concentrates around the true data generating process should largely be irrelevant of the particular details of any given observation.

These intuitions are formalized in the theory of _asymptotics_. Here we assume that the likelihood function for any observation is smooth and then consider the _maximum likelihood estimator_,

$$
\theta_{\text{ML}}(y) =  
\underset{\theta \in \Theta}{\text{argmax}}
\pi_{\mathcal{S}}(y ; \theta).
$$
If the observational model contains the true data generating process, π†(y)=π(y;θ†) for some true parameters θ†, then under some technical conditions the distribution of maximum likelihood estimates converges towards θ† as the number of component observations increases. In particular, for sufficiently large N the maximum likelihood estimator approximately follows a distribution specified by a Gaussian probability density function,

$$
J(\theta_{\text{ML}}(y)) \cdot (\theta_{\text{ML}}(y) - \theta^{*}) \sim 
\mathcal{N}(0, 1),
$$

where J is the _Fisher information matrix_ which evaluates the expectation value of the Hessian of the log likelihood function,
$$
J_{ij}(\theta) = \int \mathrm{d} y \, 
\pi_{\mathcal{S}}(y ; \theta)
\frac{ \partial^{2} }{ \partial \theta_{i} \partial \theta_{j} } 
\log \pi_{\mathcal{S}}(y ; \theta).
$$
A common temptation is to write this result as
$$
\theta_{\text{ML}}(y) 
\sim 
\mathcal{N}(\theta^{*}, J(\theta_{\text{ML}}(y))),
$$
but this is technically incorrect as the pushforward distribution for the estimator cannot depend on the estimator itself! The slightly awkward form used above gathers the maximum likelihood estimator dependencies together to avoid this problem.

Once this asymptotic behavior takes hold, any expected utility that depends only on the maximum likelihood estimator or the Fisher information becomes a Gaussian integral which will be straightforward to approximate, if not outright derive in closed-form, for many utility functions. Moreover, because the distribution for the maximum likelihood estimator depends on only the true model configuration, we don’t have to worry about figuring out a worst case expected utility. All of the expected utilities will be the same!

Consequently in this asymptotic limit we can construct point estimators and confidence sets with known calibrations regardless of the specifics of the observational model. To implement them in practice all we have to do is compute a straightforward maximization of the likelihood function. If we’re being good we’d also verify that the observation has enough independent components for the asymptotic limit to be a reasonable approximation for _all_ possible true model configurations.

Under mild conditions this behavior also carries over to Bayesian inference. Provided that the prior is smooth and doesn’t assign zero probability to any neighborhood of the model configuration space then the _Bernstein-von Mises Theorem_ shows that the posterior distribution manifests the same concentration around the true data generating process that the maximum likelihood estimator does. In this case most posterior expectation values become much easier to approximate, if not evaluate exactly.

This asymptotic limit is a paradise relative to the fragile world that I’ve carefully introduced above. The problem is that verifying for what N a given observational model is well approximated by asymptotic behavior is no trivial task. Simpler models will converge to the asymptotic limit faster and hence be well approximated with smaller N, while more complex models will typically require larger N. Working out the exact details of this convergence for each model configuration in the observational model, however, requires serious mathematical and computational tools.

Perhaps more importantly, the assumption that the observational model contains the true data generating process can obstruct the applicability of the asymptotic limit altogether. Recall that observational models are themselves often crude approximations to the true data generating process. For small N the observation will be only weakly informative and we won’t be able to resolve the system well enough to notice the approximation. As N increases, however, our observations become informative enough that we can resolve the limitations of the observational model. In other words, as we try to escape to the asymptotic limit the assumption that the observational model contains the true data generating process become harder and harder to justify.

Consider, for example, an observational model where we ignore any heterogeneity in the processes that generate each component observation. In this case our model might need only a few parameters homogenous to all the components. For sufficiently many components in the observation the asymptotic limit will well approximate this homogenous observational model. In that limit, however, our inferences for the homogenous parameters become precise enough that we start to resolve the heterogeneity that we ignored. Even though the homogenous observational model converges to the asymptotic limit, it _diverges_ from the true data generating process and the limit becomes largely irrelevant.

When the observational model is an approximation, the ultimate utility of the asymptotic limit depends on the existence of an intermediate N for which the observational model converges close enough to the asymptotic limit without diverging too far from the true data generating process. Demonstrating that such an N exists in a particular application, and then identifying it if it does, is an extremely challenging task.

Still, frequentist asymptotics have become the norm in many applied fields because of the ease of their implementation, along with the ease with which the underlying assumptions can be ignored. Indeed frequentist inference has become so tightly bound to the asymptotic limit in much of the academic literature it becomes the basis for unfounded comparisons to Bayesian methods.

A common refrain is that frequentist methods are much less computationally demanding than Bayesian methods. This comparison, however, is not between the general application of the two methodologies but rather between the application of frequentist methods in the asymptotic limit and the general application of Bayesian methods _without_ the luxury of that limit. A single optimization through the model configuration space is undoubtable less computationally demanding than the survey of the model configuration space needed to accurately approximate posterior expectation values, but this isn’t a proper comparison.

The asymptotic limit drastically simplifies the structure of the observational model, reducing the burden of _both_ frequentist and Bayesian computation. In the asymptotic limit we no longer need to rely on general Bayesian tools for computing posterior expectations and can instead utilize approximate algorithms that exploit the asymptotic structure. If the limit well approximates the observational model in a given application then any fair comparison has to allow both methodologies to take advantage of it. In that case the computational burden of both approaches becomes nearly equivalent.

On the other hand, if the asymptotic limit poorly approximates the observational model then we have to rely the general frequentist and Bayesian methodologies. Here we can no longer rely on the asymptotic calibration of maximum likelihood estimators and instead have to engineer a bespoke estimator and go through the costly calibration process in its entirety. In comparison, building and calibrating a Bayesian model is often much less computationally demanding.
