The methodology most common to introductory statistics courses is the _frequentist_ approach **which introduces additional philosophical assumptions to constrain the possible quantifications of consistency.**

**Frequentist methods ultimately derive from attempts to make probability _objective_ by defining it as something which could be measured.** More formally, this approach assumes that probabilities are _defined_ as the long run frequencies of events that can be repeated infinitely often. For example the probability of rolling a given face on a die is defined as the ratio of rolls that yield that face over the total number of rolls, as the die rolling is repeated an infinite number of times. **Because all observers would hypothetically encounter the same limiting frequencies, these probabilities would be physical and hence independent of the observer.**


Unfortunately this definition quickly runs into technical difficulties [[10](https://betanalpha.github.io/assets/case_studies/modeling_and_inference.html#ref-DiaconisEtAl:2017)]. Firstly, we can never actually realize the infinite, perfect replications needed to define the limiting frequencies in practice. An infinite number of rolls would not only take infinitely long to perform, they would also take their toll on the integrity of the die and the arm of the poor soul entrusted with the Sisyphean task. Moreover, even if we ignore the infeasibility of the replications we cannot ignore the mathematical difficulties with defining limiting frequencies. **It turns out that even in simple cases these limits are not always so well-behaved.**


Consequently formal frequentist inference pulls something of a bait and switch – the frequency definition of probabilities is replaced with Kolmogorov’s axioms, but with the restriction that the resulting probability theory can be applied to _only_ events that can be repeated infinitely often, at least hypothetically. The hypothetical nature of this restriction has some interesting loopholes that one sometimes has to exploit to model populations and other systems of interest, but it does provide a mathematical foundation on which we can build inferences. In particular, if we presume that the circumstances of an observation can be exactly replicated then we can use probability theory to describe the distribution of possible observations and admit the observational models that we introduced above.

**The only way that we can define consistency under these assumptions, however, is through _binary quantifications_. Individual model configurations are either consistent with the observation or they’re not.** Any continuous, and mathematically self-consistent, quantification of consistency would be equivalent to the probability theory which is forbidden from consorting with the model configuration space.

An immediate weakness of binary configurations is that once a model configuration is deemed inconsistent it can no longer inform decisions. An overaggressive quantification can be lead astray by irrelevant features of an observation and end up discarding model configurations that well approximate the true data generating process, if not the true data generating process itself. To compensate for this frailty the frequentist approach treats inference as a _decision-making process_ and carefully calibrates those decisions to ensure that the binary quantifications are well-behaved _on average_.

Formally, consistency is assigned by _estimators_ that deterministically map observations into some binary quantifications of the model configuration space. If we treat the possible quantifications as actions, a, then an estimator defines a decision-making processes, a(y~), that we can calibrate with a model-based utility function, U(a,θ).

...

Because of the foundational assumptions of the frequentist perspective, however, we are limited here. For example we cannot average over the possible model configurations because as that would require applying probability theory to the model configuration space. Just about the only thing that we can do is report the _worst case expected utility_,
...

In this way we can calibrate the worst case behavior of the estimator and determine whether or not it meets our needs, at least under the assumptions that the true data generating process is contained within the observational model (m'STRONG ASSUMPTION').

In the end frequentist inference does not define a unique inferential procedure. Instead if formalizes inferential procedures as estimators and defines a unique procedure for calibrating those estimators. In order to develop a frequentist analysis we need to specify not just our observational model but also an estimator and its associated utility function, and then carry out the worst case expected utility analysis.


...
...
...


### Frequentist Inference in Practice

As we saw above, the worst case calibration used by frequentist methods can be very conservative. An estimator might be well-behaved for most reasonable model configurations but have its worst case behavior determined by the boundaries of the model configuration space populated by extreme, but not impossible, model configurations. That said, if we are fortunate enough to engineer an estimator with an acceptable worst case expected utility then we can have confidence that its behavior will be extremely robust, at least within the context of the observational model. The practical challenge is whether or not such an estimator even exists and we can find it.

Even if such an estimator does exist, however, performing the proper frequentist calibration needed to determine the worst case expected utility isn’t always feasible. Despite the simplicity of the observational model in the examples shown above, for example, the calculations were not for the faint of heart. Even with the advantageous properties of the complementary models, estimators, and utility functions we had to know exactly what manipulations would lead to fruitful analytic results. Upon perturbing any of those inputs the convenience dissolves away and we typically have to consider numerical approximations.

Simulation, and Monte Carlo estimation of the expected utilities, offers a general strategy for approximating the calibration, but it can be extremely expensive in practice. A simulation for a single model configuration can be expensive on its own, and a frequentist calibration needs to simulate along a sufficiently fine grid of model configurations to quantify the full behavior of the expected utilities. This is complicated by the fact that we typically have to expand the grid all the way to the boundaries of the model configuration space where the worst case expected utility often hides. Still, simulation methods can be useful for low-dimensional observational models where relatively diffuse crude can be sufficient. As we increase the dimensionality of the model, however, we require exponentially finer grids, and exponentially increasing costs, that quickly overwhelm the available computational resources.

An unfortunate consequence of these challenges is that these systems with analytic results are often forced into applications where they have limited usefulness. The requisite observational model, for example, may be a poor approximation to the system being analyzed, or the requisite estimator may be irrelevant to the overall inferential goals of the analysis. In order to facilitate ignoring these complications, frequentist methods are often presented as black boxes for consuming data and automatically producing insights without any consideration of the implicit assumptions. The growing popularity of statistical software which can hide these assumptions in code often exacerbates the problem.

All of this said, there is one circumstance where relatively robust calibrations are available in closed form for a wide class of observational models. Under certain conditions, aggregating sufficiently-many independent observations results in model configurations that are reasonably well-approximated with Gaussian probability density functions. In this _asymptotic_ regime we can then apply calculations similar to those introduced above to calibrate specific point estimators and set estimators. I discuss asymptotic results, and their limitations, more in [Section Four](https://betanalpha.github.io/assets/case_studies/modeling_and_inference.html#sec:asymptotics).

