### 3.1.3 The Posterior Distribution

One we have a prior distribution and a likelihood function we can immediately construct a posterior distribution using Bayes’ Theorem. Within a parameterization of the model configuration space, Bayes’ Theorem defines the posterior density function as

$$
\begin{align*}
\pi_{\mathcal{S}}(\theta \mid \tilde{y}) 
&=
\frac{ \pi_{\mathcal{S}}(\tilde{y} \mid \theta) }
{ \int \mathrm{d} \theta \, 
\pi_{\mathcal{S}}(\tilde{y} \mid \theta) \, \pi_{\mathcal{S}}(\theta) } 
\cdot \pi_{\mathcal{S}}(\theta)
\\
&\propto
\pi_{\mathcal{S}}(\tilde{y} \mid \theta) \cdot \pi_{\mathcal{S}}(\theta).
\end{align*}
$$

The name Bayesian inference derives from this application of Bayes’ Theorem, which can lead to confusion in practice because Bayes’ Theorem a general result from probability theory and not unique to this application. In other words using Bayes’ Theorem does not define Bayesian inference. **Using probability distributions to quantify information about the model configuration space defines Bayesian inference.**

**Bayes’ Theorem can be thought of as switching from one conditional probability density function, that specifying the observational model, to another, that specifying the posterior distribution**. Bayes’ Theorem can also be thought of a procedure for _updating_ the prior distribution into a posterior distribution.

![[Pasted image 20220812105327.png]]


**This latter perspective makes it more clear that this particular application of Bayes’ Theorem implements a _learning_ process. What we know after the observation, as encoded in the posterior distribution, is just the combination of what we knew before the observation, as encoded in the prior distribution, and what we learned from the observation, as encoded in the likelihood function**. Bayes’ Theorem ensures that all of this information is conserved and makes its way to the posterior distribution.

The posterior density function, and hence the posterior distribution itself, concentrates on those model configurations that are consistent with _both_ our domain expertise, as encoded in the prior density function, and the observation, as encoded in the likelihood function. This manifests in three basic updating behaviors:

**_Contraction_ occurs when the likelihood function is more informative than, but also consistent with, the prior distribution.**
![[Pasted image 20220812105635.png]]

**_Containment_ occurs when the prior distribution is more informative than, but also consistent with, the likelihood function.**

![[Pasted image 20220812105733.png]]

**_Compromise_ occurs when there is tension between the information encoded in the likelihood function and the prior.**

![[Pasted image 20220812105834.png]]


... 

Depending on the observed data and the choice of m and s (known parameters of the model), the updating process can exhibit any of the three behaviors discussed above.

