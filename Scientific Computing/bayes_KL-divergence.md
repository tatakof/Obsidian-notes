 add stuff from that video on the KL divergence. 


## Betancourt stuff

#### 1.4.2.1 Assessing Predictive Distributions
The mathematical structure of probability distributions limits the ways in which we can construct self-consistent numerical comparisons. Information theory works out the precise consequences of these limitations; here I will present a summary of the results.

Without endowing an ambient space with any particular structure -- like a metric or coordinate functions -- the only self-consistent way to compare two measures μ
and ν over that space is with an _f__-divergence_ [[6](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#ref-CsiszarEtAl:2004)],

$$
D_{f} \! \left( \mu \mid\mid \nu \right)
= \mathbb{E}_{\nu} \left[
f \! \left( \frac{ \mathrm{d} \mu }{ \mathrm{d} \nu } \right) \right],
$$
where f:R→R is any convex function satisfying f(1)=0. An f-divergence vanishes only when the two measures are equal and monotonically increases as the two measures deviate from each other, approaching infinity when μ is not absolutely-continuous with respect to ν.

Most choices of f, however, yield divergences that are not compatible with any product structure on the ambient space. More specifically consider a product space X=X1×X2 with the two _independent measures_, μ=μ1×μ2 and ν=ν1×ν2. Even though the measures are independent over the two components, a general f-divergence between these two product measures will _not_ decompose into a sum of f-divergences between the component measures μ1 and ν1 and f-divergences between the component measures between μ2 and ν2. In other words comparisons of the first components are not independent of the second components. For example if X1 were the configuration space of some system on Earth and X2

were the configuration space of some system on Mars then we wouldn't be able to compare two measures on Earth without first being able to quantify what's happening on Mars, even though the measures are all unrelated!

In order for these comparisons to be consistent with the marginalization of irrelevant components we need f to convert _products_ of Radon-Nikodym derivatives into _sums_ of Radon-Nikodym derivatives. Up to scaling the only function with this property is the natural logarithm. The _Kullback-Leibler divergence_ is given by the choice f(x)=xlog(x),

$$
\begin{align*}
\mathrm{KL} \! \left( \mu \mid\mid \nu \right)
&\equiv
\mathbb{E}_{\nu} \left[
\frac{ \mathrm{d} \nu }{ \mathrm{d} \mu } \cdot
\log \frac{ \mathrm{d} \mu }{ \mathrm{d} \nu } \right]
\\
&=
\mathbb{E}_{\mu} \left[
\log \frac{ \mathrm{d} \mu }{ \mathrm{d} \nu } \right]
\\
&=
- \mathbb{E}_{\mu} \left[
\log \frac{ \mathrm{d} \nu }{ \mathrm{d} \mu } \right],
\end{align*}
$$

or, equivalently, by the choice f(x)=−log(x),
$$
\begin{align*}
\mathrm{KL} \! \left( \nu \mid\mid \mu \right)
&\equiv
\mathbb{E}_{\nu} \left[
- \log \frac{ \mathrm{d} \mu }{ \mathrm{d} \nu } \right]
\\
&=
- \mathbb{E}_{\nu} \left[ \log \frac{ \mathrm{d} \mu }{ \mathrm{d} \nu } \right]
\\
&=
\mathrm{KL} \! \left( \mu \mid\mid \nu \right).
\end{align*}
$$

**Because the Kullback-Leibler divergence is not symmetric in its two arguments we have two possible ways that we can compare a predictive distribution, πpred, and the true data generating process, π†. Using the predictive distribution as the base measure,**

$$
\mathrm{KL} \! \left( \pi^{\text{pred}} \mid\mid \pi^{\dagger} \right),
$$
**focuses the comparison only where the predictive distribution concentrates, and consequently does not penalize predictive distributions that completely ignore neighborhoods allocated reasonable probability by π†. In the extreme limit this divergence does not even penalize predictive distributions that are not absolutely continuous with respect to the true data generating process!**

In order to truly assess a predictive distribution we need to instead base the divergence on the true data generating process itself,

$$
\mathrm{KL} \! \left( \pi^{\dagger} \mid\mid \pi^{\text{pred}} \right)
=
- \mathbb{E}_{\pi^{\dagger}}
\left[ \log \frac{ \mathrm{d} \pi^{\text{pred}} }{ \mathrm{d} \pi^{\dagger} } \right],
$$

or in terms of probability density functions,

$$
\mathrm{KL} \! \left( \pi^{\dagger} \mid\mid \pi^{\text{pred}} \right)
=
- \int_{Y} \mathrm{d} y \, \pi^{\dagger}(y)
\log \frac{ \pi^{\text{pred}}(y) }{ \pi^{\dagger}(y) }.
$$
**Because this particular Kullback-Leibler divergence is motivated by just a few, natural properties it ends up being the foundation for many predictive validation methods, even those that were originally motivated from other perspectives. That said, the Kullback-Leibler divergence, and hence all of the methods derived from it, is not without its limitations.**

**The most foundational problem with the Kullback-Leibler divergence is that it depends on the _entirety_ of the two distributions being compared, often in mysterious ways. For example the divergence has a complex relationship, if any at all, to the differences in expectation values with respect to the two distributions. In fact two distributions specified by normal probability density functions can have arbitrarily small Kullback-Leibler divergence even when the location parameters are moved infinitely far apart! The comprehensive nature of the Kullback-Leibler divergence means that we cannot in general discriminate between relevant and irrelevant features. Indeed in practice the divergence is often dominated by details inconsequential to a given analysis.**

**Moreover the output values of the Kullback-Leibler divergence themselves have no _absolute_ meaning. While zero implies perfect agreement between the two distributions being compared there is no natural threshold below which we can declare our model "good enough". The awkward relationship between the Kullback-Leibler divergence and more interpretable distribution properties defined by expectation values usually makes it impossible to construct a useful threshold either theoretically or empirically.**

**Ultimately the only meaning of Kullback-Leibler divergences are _relative_ to other Kullback-Leibler divergences. This does allow us, however, to _order_ multiple models by their divergence from the true data generating process to the respective predictive distributions.**

#### 1.4.2.2 Relative Predictive Performance Scores
