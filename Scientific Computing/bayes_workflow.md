


# Definitions:
- statistics: In classical statistics, functions of the observational space are know as statistics. 
- model calibration: determining what outcomes a model might return, rather than any process of modifying a model to achieve a particular outcome. 
- Posterior Z-score: The posterior z-score quantifies how accurately the posterior recovers the true model configuration along this coordinate. Smaller values indicate a posterior that more strongly concentrates around the true value while larger values indicate a posterior that concentrates elsewhere. Note that the posterior z-score captures neither the bias nor the precision of the posterior distribution but rather a combination of the two.
- Posterior contraction of a given parameter: Posterior contraction quantifies how much the likelihood function from a given observation informs the given function. Posterior contraction near zero indicates that the data provide little information beyond the domain expertise encoded in the prior model, while posterior contraction near one indicates observations that are much more informative relative to the prior model.  
- M Categories: classification for the relationship between an observational model and the true data generating process.
	- M-Closed: The ideal, and largely unattainable, circumstance where our model contains the true data generating process. 
	- M-Open: The more practical circumstance where our model doesn't contain the true data generating process. 
	- M-good enough: where the model is sufficient for our particular analysis. 


Principled model development strives for an observational process that captures the relevant structure of the phenomenon, environment, and probe that give rise to the true data generating process. We always have to be careful, to recognize the limitations of the even the most carefully designed observational model in any given analysis.


# Towards A Principled Bayesian Workflow

#### Michael Betancourt

Given a probabilistic model and a realized observation, Bayesian inference is straightforward to implement. At least _conceptually_. **Inferences, and any decisions based upon them, follow immediately in the form of expectations with respect to the induced posterior distribution**. _Building_ a probabilistic model that is useful in a given application, however, is a far more open-ended challenge. Unfortunately the process of model building is often ignored in introductory texts, leaving practitioners to piece together their own model building workflows from potentially incomplete or even inconsistent heuristics.

A principled workflow considers whether or not modeling assumptions are appropriate and sufficient for answering relevant questions in _your_ particular applied context. Because everyone asks different questions in different contexts, such a workflow cannot be reduced to a deterministic algorithm. All we can do is assemble a coherent set of techniques to help us evaluate our own assumptions and guide our unique path through model space.

We will begin with a discussion of what behaviors we want in a probabilistic model, and how we can condense information to guide our evaluation of those behaviors...


Together an observational model, πS(y∣θ), and a prior model, πS(θ), define the complete Bayesian model specified through the joint probability density function

$$
\pi_{\mathcal{S}}(y, \theta) =
\pi_{\mathcal{S}}(y \mid \theta) \, \pi_{\mathcal{S}}(\theta).
$$


**Theoretically we implement Bayesian inference by conditioning the complete Bayesian model on an observation y~ and computing expectation values with respect to the induced posterior distribution.** The utility of these inferences, however, is completely dependent on the assumed Bayesian model. A model inconsistent with the actual data generating process will be of little use in practice, and may even be dangerous in critical applications.


What, however, exactly characterizes a probabilistic model that is consistent enough with a given application? Ideally the model would be compatible with our domain expertise, capturing our knowledge of the experimental design and latent phenomena, or at least enough to domain expertise to enable answers to the inferential questions of interest. It would also help if the model didn't choke our available computational tools so that we could accurately estimate posterior expectation values and faithfully implement the desired inferences in practice. Finally it would be great if our model were rich enough to capture the structure of the true data generating process relevant to our inferential questions.

In other words we can evaluate a model by answering four questions.

#### Question One: Domain Expertise Consistency

_Is our model consistent with our domain expertise?_

#### Question Two: Computational Faithfulness

_Will our computational tools be sufficient to accurately fit our posteriors?_

#### Question Three: Inferential Adequacy

_Will our inferences provide enough information to answer our questions?_

#### Question Four: Model Adequacy

_Is our model rich enough to capture the relevant structure of the true data generating process?_


Even in simple applications, however, these questions can be challenging to answer. We need to carefully examine a candidate model in the context of these four questions and concentrate enough pertinent information to identify any limitations of the model and suggest specific improvements.

## 1.1 Domain Expertise Consistency


**Models built upon assumptions that conflict with our domain expertise will give rise to inferences and predictions that also conflict with our domain expertise. While we don't need our model to capture _every_ last detail of our knowledge, at the very least our models should not be in outright conflict with that knowledge. In order to judge the compatibility of our modeling assumptions and our domain expertise, however, we need to actually acknowledge our implicit domain expertise about the latent phenomena, encapsulating environments, and experimental probes in a given application.**

Unfortunately _eliciting_ our domain expertise, translating our implicit knowledge into something more explicit, is far from straightforward. For example our implicit knowledge often takes the form not of absolute statements but rather relative comparisons that are harder to quantify. Moreover this elicitation takes time and effort which means that our quantifications will _evolve_ with the work we put into the process. The process is even more expensive when domain expertise is spread across a group of individuals.

Ultimately we will never be able to precisely and completely elicit our collective domain expertise in practice. What we can do, however, is elicit a _self-consistent approximation_ to that domain expertise that is sufficient for a given analysis.

From this perspective eliciting domain expertise, and contrasting our model assumptions with that knowledge, is an _iterative_ process. We begin with an initial model and investigate the _consequences_ of that model within relevant contexts. In each context we elicit domain expertise that we have not yet considered and check whether our model consequences are consistent with that knowledge or instead _surprise_ us and suggest improvements towards a more self-consistent model. By focusing on the consequences relevant to a given application we can then refine our complete Bayesian model until we have achieved sufficient consistency.


**Formalizing this process we arrive at visual _prior pushforward checks_ and _prior predictive checks_ which are readily implemented with modern sampling methods, providing powerful instruments for our model building workflow.**

### 1.1.1 Quantifying Consequences

In order to formalize the process for evaluating the consistency between our modeling assumptions and our domain expertise we need to define exactly how we isolate particular consequences of those assumptions, elicit domain expertise in that context, and then compare the elicitation to the consequences.


#### 1.1.1.1 Abridge Too Far

**In any nontrivial analysis where the model configuration space and observational space are relatively high dimensional, the complete Bayesian model and its consequences will be far too big to reason about as a whole. Instead we need to isolate lower-dimensional subspaces that isolate particular consequences and facilitate the consistency analysis.**

**Mathematically this means defining a _summary function_ that projects the entire product space into some interpretable, lower-dimensional space, U, that is relevant to the analysis,**

$$
\begin{alignat*}{6}
t :\; &Y \times \Theta& &\rightarrow& \; &U \subset Y \times \Theta&
\\
&(y, \theta)& &\mapsto& &t(y, \theta)&,
\end{alignat*}
$$

**and then analyzing the corresponding pushforward distribution, πt(Y×Θ)(t). For example when the parameterization of Y×Θ is interpretable the coordinate functions are often useful summary functions.**

When the summary space is the one-dimensional real line, U=R, we can visualize the pushforward distribution with the pushforward probability density function.


![[Pasted image 20220829091205.png]]

Often it's useful to consider a collection of one-dimensional summary functions that might, for example, capture the consequence of our modeling assumptions within ordered categories.

![[Pasted image 20220829091456.png]]

When these discrete categories are approximating a continuous set of summary functions the visualization often benefits from interpolating between neighboring pushforward distributions to fill in the gaps.

When these discrete categories are approximating a continuous set of summary functions the visualization often benefits from interpolating between neighboring pushforward distributions to fill in the gaps.


#### 1.1.1.2 Pain Threshold

In order to judge the behavior of a pushforward probability distribution we need to elicit domain expertise within the narrow context of each summary function we consider. Even if the summary space is one-dimensional this can be challenging as our domain expertise is rarely so well-defined that it can be immediately encoded in anything as precise as a probability distribution.

Domain expertise is often much easier to elicit in terms of relative _comparisons_ of the summary function values, for example which of two values is more reasonable than the other. This may not be enough to define a probability distribution but it is enough to define approximate _thresholds_ that separate "reasonable" values of the summary function and "extreme" values. Importantly extreme values above the thresholds are unreasonable but not impossible; in other words these thresholds quantify when we transition from being ambivalent with the output values to being uneasy with them.

If we've parameterized our model such that zero specifies a reasonable value then we can also talk about the thresholds partitioning the summary space into the reasonable values of the summary function we more associate with zero and the extreme values that we more associate with infinity. From this perspective the thresholds define where we start to "round up" to infinity.

Typically we won't be able to reduce our domain expertise into thresholds with precise values, and in practice it's easier to consider them as identifying only the order of magnitude where values start to become unsavory. Another way to reason about the order of magnitude is to reason about the _units_ deemed appropriate to the problem. A summary function typically presented in units of grams is unlikely to exceed values that surpass kilograms, otherwise kilograms would have been the more conventional unit in the first place!

To demonstrate the elicitation of approximate thresholds let's consider a model of how quickly a drug propagates through a patient's blood stream. Even if we are not well-versed in physiology we are not completely ignorant; for example we can be fairly confident that the unknown propagation speed will be less than the speed of sound in water, as a drug dose traveling that fast would have...unfortunate physical consequences on the integrity of blood vessels. The speed of sound in water is around 1 kilometer per second, and that order of magnitude provides a threshold capturing our very basic domain expertise. Of course the more domain expertise we have about physiology the closer to zero we can push this threshold.

Similarly if we're modeling carbon concentration in the air then we can be sure that our thresholds should at least be bounded by concentrations more characteristic of solid concrete than gaseous, breathable air. If we're modeling the migration of birds then we should probably define thresholds on flying speed well below the speed of light.

This focus on thresholds has a few key advantages when trying to elicit domain expertise in practice.

Because we only need to identify where extreme values begin, we, or the experts with whom we are working, can focus on only rejecting bad values instead of having to take the responsibility of accepting good values. In other words we can take advantage of our natural appetite to criticize by moving the threshold down to less extreme values until we start to become hesitant in our pessimism.

Secondly thresholds are easier to manage when trying to reconcile conflicting domain expertise from multiple sources. While those sources might disagree about the fine details within the thresholds, they are much more likely to agree about the extremes. Moreover we can always take a conservative approach and set the thresholds as the largest of those elicited, defining extreme values consistent with all of the domain expertise considered.

#### 1.1.1.3 Tall Tails

Thresholds informed by our approximate domain expertise separate the output of a summary function into reasonable and extreme values. In order to compare this manifestation of our domain expertise to the consequences of our model we need our pushforward probability distributions to make a similar partition.

Unimodal probability density functions are often separated into a _bulk_ or _head_, a central neighborhood in which most of the probability is concentrated, surrounded by one or more _tails_, containing the meager probability that remains.


![[Pasted image 20220912103544.png]]

If the summary space is unbounded then the tails will typically stretch out towards infinity in both directions. When the summary space is bounded, however, a probability density function might feature a bulk adjacent to the boundary with a tail on the other side, or a bulk surrounded by tails stretching to the boundaries on either side.

![[Pasted image 20220912103827.png]]

![[Pasted image 20220912103814.png]]

Qualitatively the bulk and the tails of a probability density function define their own separation of the summary space into "reasonable" and "extreme" values. If we've parameterized the summary space well then the bulk will contain zero, and we can also talk about the boundary between the bulk and the tails as partitioning the summary space into the reasonable values of the summary function closer to zero and the extreme values closer to infinity.

The bulk and the tails of a probability density function are qualitative features with no precise definition. In order to make the definition more explicit we can define tails as the bounding neighborhoods that contain a specific amount of probability, but we have to remember that any choice is approximate. For convenience I usually define a tails as a bounding regions containing 1% of the total probability, but when making any quantitative comparisons I also consider the 0.1% and 5% regions to avoid any sensitivity to this particular choice.

![[Pasted image 20220912105212.png]]

#### 1.1.1.4 Wag the Dog
Now that we have distilled both our domain expertise to thresholds and our model consequences to tails in each summary space we can go about comparing them. Because both are approximate, and best considered as orders of magnitude, we should require that those orders of magnitude are consistent with each other.

I personally prefer to summarize these comparisons visually by plotting the domain expertise informed thresholds over the pushforward probability density functions for each summary function.

![[Pasted image 20220912105420.png]]
![[Pasted image 20220912105427.png]]

![[Pasted image 20220912105435.png]]

The advantage of this visualization is that we can see what qualitative features of the pushforward probability density function have to change to ensure compatibility within the context of each summary function, and hence motivate changes to the complete Bayesian model.

We can provide a more quantitative measure by computing the pushforward probability outside of the domain-expertise informed thresholds to see if they are consistent with what we would expect from tails. Because these thresholds, and the definition of a tail, are only vaguely defined we have to be careful not to expect too much from these tail probabilities. I typically consider anything between 0.1% to 5% to be valid.

![[Pasted image 20220912105542.png]]

#### 1.1.1.5 Implementing Prior Checks

Unfortunately the implementation of these model checks in practice is frustrated by our inability to analytically construct explicit pushforward density functions outside of very simple circumstances. In most cases we can construct visual checks, however, by pushing forward exact samples from the complete Bayesian model.

Conveniently we can often construct a sample from the complete Bayesian model, (y~,θ~)

, sequentially, first generating a sample from the prior distribution,

$$
\tilde{\theta} \sim \pi_{\mathcal{S}}(\theta)
$$

before simulating an observation from the corresponding data generating process,

$$
\tilde{y} \sim \pi_{\mathcal{S}}(y \mid \tilde{\theta}).
$$


We can then construct a sample from any summary pushforward distribution by evaluating the summary function at this sample,

$$
\tilde{t} = t(\tilde{y}, \tilde{\theta}).
$$

Using these pushforward samples we can then construct visualizations such as histograms, empirical cumulative distribution functions, and the like that allows us to immediately implement the consistency checks.

![[Pasted image 20220912105920.png]]


When using a sequence of summary functions I prefer to use _quantile ribbons_ to compactly visualize each pushforward distribution next to each other. For example here I use nested 10%-90%, 20%-80%, 30%-70%, and 40%-60% intervals, along with the median, which are readily estimated from ensembles of hundreds of samples.


![[Pasted image 20220912110016.png]]

### 1.1.2 Prior Pushforward Checks
In many applications, especially in science, the observational model is understood much better than the prior model. Consequently we often need to prioritize checking the consequences of the prior model, especially in the context of the observational model.

A _prior pushforward check_ considers summary functions that depend only on the model configuration space,
$$
\begin{alignat*}{6}
t :\; &\Theta& &\rightarrow& \; &U \subset \Theta&
\\
&\theta& &\mapsto& &t(\theta)&,
\end{alignat*}
$$
and the corresponding pushforward of the prior model, $\pi_{t(\Theta)}(t)$

If the model configuration space is a product space then the coordinate functions are natural candidates for summary functions. Indeed if our prior model is defined by an independent probability density function,

$$
\pi_{\mathcal{S}}(\theta)
=
\pi_{\mathcal{S}}(\theta_{1}, \ldots, \theta_{N})
=
\prod_{n = 1}^{N} \pi_{\mathcal{S}}(\theta_{n}),
$$

then we can use thresholds informed by our domain expertise to motivate the component prior density functions in the first place. We will use this strategy extensively in [Section 4](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:demonstration).

Principled component prior density functions are critical to a good prior model, but they are not sufficient. In general the observational model will be mediated by intermediate functions of the model configuration space, and good component priors do not guarantee that the pushfoward of the entire prior model onto these intermediate functions are well-defined. If our complete Bayesian model is built from a conditional decomposition with a directed graphical representation then the internal pushforward nodes all identify functions that we will want to investigate for the given application.

For example consider a data generating process that manifests in binary observations, Y={0,1}N, and an observational model specified by the Bernoulli family of probability mass functions where the probability parameters are defined by some function of the model parameters,

$$
\pi_{S}(y \mid \theta)
= \pi_{S}(y_{1}, \ldots, y_{N} | \theta)
= \prod_{n = 1}^{N} \text{Bernoulli}(y_{n} \mid p(\theta)).
$$

In this case the complete Bayesian model admits a directed graphical model representation.
![[Pasted image 20220912111145.png]]

In order to understand the full consequences of our prior model _in the context of this observational model_ we would need to take the probability function p(θ) as a summary function and investigate the corresponding pushforward of the prior model. A prior distribution that is too diffuse, for example, might induce a pushforward distributions that concentrate too strongly at extremely small or large probabilities.

![[Pasted image 20220912111337.png]]

These horns are extremely metal but also indicate that this concentration is likely to overwhelm the contribution of likelihood functions and pull any posterior distribution to the boundaries as well, at least unless we have a wealth of data. If this behavior is at odds with our domain expertise, say knowledge that favors a more uniform distribution over probabilities, then we would have to refine our prior model until the prior pushforward check is better behaved.

![[Pasted image 20220912111434.png]]

### 1.1.3 Prior Predictive Checks

To fully probe the consequences of our prior model, however, we need to investigate its effects on the observational space itself. A _prior predictive check_ considers summary functions that depend only on the observational space,

$$
\begin{alignat*}{6}
\hat{t} :\; &Y& &\rightarrow& \; &U \subset Y&
\\
&y& &\mapsto& &\hat{t}(y)&,
\end{alignat*}
$$
and the corresponding pushforward of the prior model, $\pi_{\hat{t}(Y)}(t)$. In classical statistics functions of the observational space are also know as _statistics_, so to avoid any confusion with prior pushforward checks I will refer to these summary functions as _summary statistics_.

Pushing the complete Bayesian model, πS(y,θ), forward along a summary statistic is equivalent to pushing the prior predictive distribution,

$$
\begin{align*}
\pi_{\mathcal{S}}(y)
&= \int \mathrm{d} \theta \, \pi_{\mathcal{S}}(y, \theta)
\\
&= \int \mathrm{d} \theta \,
\pi_{\mathcal{S}}(y \mid \theta) \, \pi_{\mathcal{S}}(\theta),
\end{align*}
$$

along that statistic. **Consequently we can also interpret prior predictive checks as investigating the structure of the prior predictive distribution and looking for an excess of extreme predictions.**

**Constructing an interpretable yet informative summary statistic is very much an art where we can fully employ our creativity to define useful real-valued summaries or even structured multidimensional summaries like a histograms or empirical cumulative distribution functions.** The orthodox frequentist literature also provides a surprising wealth of inspiration as classic estimators define summary statistics with very clear interpretations. For example empirical means and medians are sensitive to the centrality of the prior predictive distribution along specific components of the observational space, with the empirical standard deviation and quartiles sensitive to the breadth of the distributions. We can be more creative, however, when the observational space is more structured. Empirical correlograms, for example, can summarize the structure of time series data while analysis of variance statistics can summarize heterogeneity between groups.

Because summary statistics are defined with respect to only the observational space the thresholds we need to complete the prior predictive checks need to be informed only by knowledge of the observational space itself. Consequently it can be easier to elicit these thresholds than the thresholds for prior pushforward checks, which require understanding the structure of the complete Bayesian model. This is especially true when working with domain experts more familiar with the experiment than with models of the latent phenomena.

**Importantly prior predictive checks are a technique for comparing our model assumptions to our domain expertise, and to _only_ our domain expertise. Allowing comparisons between the prior predictive distribution and any _observed_ data to influence the development of the prior model is a form of _empirical Bayes_ that uses the data twice, once to directly inform the prior model and again to construct the posterior distribution. This over-influence of the observed data is prone to _overfitting_ where we develop a model that is exceptionally good at retrodicting the particular data we observed at the cost of poor predicitons of the rest of the true data generating process.**

One of the nice features of implementing prior pushforward checks and prior predictive checks with samples is that these implementations use progressive information about the complete Bayesian model, allowing us to share computation between the checks. For example, once we've generated a sample from the complete Bayesian model,

$$
\tilde{\theta} \sim \pi_{\mathcal{S}}(\theta),
\\
\ \tilde{y} \sim \pi_{\mathcal{S}}(y \mid \tilde{\theta}),
$$

**we can use the sampled model configuration for prior pushforward checks and the simulated observation for prior predictive checks without any additional cost. This is even more apparent when the full Bayesian model admits a nice conditional decomposition that allows us to use ancestral sampling, with each conditional sample corresponding to an intermediate pushforward distribution that we can analyze for consistency.**


## 1.2 Computational Faithfulness
A model is only as useful as our ability to wield it. A Bayesian model is only as good as our ability to compute expectation values with respect to the posterior distributions it generates or, more practically, estimate expectation values with quantifiable error.

Given a particular observation, and hence posterior distribution, we can use methods with self-diagnostics, such as Hamiltonian Monte Carlo, to identify inaccurate computation and provide some confidence that we can actually realize faithful inferences.

Before we've made an observation, however, we don't know what shape the likelihood function will take and hence the structure of the posterior density function that our algorithms must manage. Some potential observations, for example, might lead to likelihood functions that strongly concentrate within compact neighborhoods and yield well-behaved posterior density functions, but some might lead to more degenerate likelihood functions that induce more problematic posterior density functions.

![[Pasted image 20220913122330.png]]

**All we can do to assess the faithfulness of our computational methods before we've made an observation is to apply them to posterior density functions arising from a variety of possible data, ideally spanning the worst behaviors we might actually see in practice. What, however, defines the scope of observations that might be realized in an experiment? Within the context of our model it's exactly the prior predictive distribution.**

If we've already addressed the first question and believe that our model is consistent with our domain expertise then we can simulate observations from the prior predictive distribution,

$$
\tilde{\theta} \sim \pi_{\mathcal{S}}(\theta),
\ 
\tilde{y} \sim \pi_{\mathcal{S}}(y \mid \tilde{\theta}),
$$
fit the resulting posterior distributions with our chosen computational method,
$$
\pi_{\mathcal{S}}(\theta \mid \tilde{y}),
$$
and then examine the ensemble behavior of those fits using whatever diagnostics are available. If we've already performed prior checks then the prior predictive samples will already have been generated -- all we have to do is fit the corresponding posteriors.

These assessments, however, are only as good as the self-diagnostic methods available. **Fortunately Bayesian inference implies a subtle consistency property that allows us to carefully assess the accuracy of _any_ algorithm capable of generating posterior samples.**

**An arbitrary Bayesian model guarantees nothing about the behavior of any single posterior distribution, even if the data are simulated from the prior predictive distribution. The _average_ posterior distribution over prior predictive draws, however, will always recover the prior distribution,**

$$
\begin{align*}
\pi_{\mathcal{S}}(\theta')
&=
\int \mathrm{d} y \, \mathrm{d} \theta \,
\pi_{\mathcal{S}} (\theta' \mid y) \, \pi_{\mathcal{S}} (y, \theta)
\\
&=
\int \mathrm{d} y \, \pi_{\mathcal{S}} (\theta' \mid y)
\int \mathrm{d} \theta \, \pi_{\mathcal{S}} (y, \theta)
\\
&=
\int \mathrm{d} y \, \pi_{\mathcal{S}} (\theta' \mid y) \, \pi_{\mathcal{S}} (y).
\end{align*}
$$

This implies, for example, that the ensemble of samples from many posterior distributions,

$$
\begin{align*}
\tilde{\theta} &\sim \pi_{\mathcal{S}}(\theta)
\\
\tilde{y} &\sim \pi_{\mathcal{S}}(y \mid \tilde{\theta})
\\
\tilde{\theta}' &\sim \pi(\theta \mid \tilde{y}),
\end{align*}
$$

**will be indistinguishable from samples from the prior distribution. Consequently any deviation between the two ensembles indicates that either the prior predictive sampling has been implemented incorrectly or our computational method is generating biased samples.**

_Simulated-based calibration_ [[2](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#ref-TaltsEtAl:2018)] compares the ensemble posterior sample and the prior sample using _ranks_. For each simulated observation we generate R samples from the corresponding posterior distribution,

$$
\begin{align*}
\tilde{\theta} &\sim \pi_{\mathcal{S}}(\theta)
\\
\tilde{y} &\sim \pi_{\mathcal{S}}(y \mid \tilde{\theta})
\\\
(\tilde{\theta}'_{1}, \ldots, \tilde{\theta}'_{R}) &\sim \pi(\theta \mid \tilde{y}),
\end{align*}
$$
and compute the rank of the prior sample within the posterior samples, i.e. the number of posterior samples larger than the prior sample,

$$
\rho = \sharp \left\{ \tilde{\theta} < \tilde{\theta}'_{r} \right\}.
$$
If the ensemble posterior samples and the prior samples are equivalent then these ranks will be uniformly distributed, allowing us to visually examine the equivalence which histograms, empirical cumulative distribution functions, and the like.

For example if the samples are equivalent then each parameter histogram should within the expected statistical variation. Here I use an independent binomial approximation in each bin to estimate the expected variation and visualize it with a gray rectangle.

![[Pasted image 20220913125019.png]]

One of the massive advantages of this approach is that common computational problems manifest in _systematic_ deviations that are easy to spot. For example if our computational method generates samples that are underdispersed then the posterior samples will cluster, concentrating above or below the prior sample more strongly than they should. This tend results in prior ranks that are biased away from the middle and a SBC histogram concentrated at both boundaries.


![[Pasted image 20220913125129.png]]

Similarly if the estimated posterior is biased high then the posterior samples will concentrate above the prior sample more strongly than they should, resulting in larger prior ranks and a SBC histogram that concentrates at the right boundary.

![[Pasted image 20220913125221.png]]

Keep in mind that specific behavior depends on our definition of rank -- if the prior ranks are defined as

$$
\rho = \sharp \left\{ \tilde{\theta} > \tilde{\theta}'_{r} \right\}
$$
then a high bias in the posterior fit will manifest in fewer posterior samples smaller than the prior sample, lower prior ranks, and a SBC histogram that concentrates at the _left_ boundary. The rank convention is arbitrary so we just have to make sure that we use one of them consistently.

**For further discussion of common systematic deviations and their interpretations see the simulated-based calibration paper.**

**Technically simulation-based calibration requires exact posterior samples, which are not available if we are using, for example, Markov chain Monte Carlo. To use simulation-based calibration with Markov chain Monte Carlo we have to first thin our Markov chains to remove any effective autocorrelation. See [[2](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#ref-TaltsEtAl:2018)] for more details.**

**The primary limitation of simulation-based calibration is that it assesses the accuracy of a computational method only within the context of the posterior distributions arising from prior predictive observations. If the true data generating process is not well-approximated by one of our model configurations then our assessment of computational faithfulness will have little to no relevance to fits of real data. These checks are strongly recommended but definitely not sufficient until we believe that more model is close enough to the true data generating process.**

## 1.3 Inferential Calibration
Once we trust our computation, at least within the context of our model, we can consider whether or not the possible posterior distributions we might encounter yield inferences and decisions that are sufficient for the inferential goals of our analysis. Because some observations might be more informative than others we will have to consider ensembles of possible observations, and hence ensembles of posterior distributions and their resulting inferences, just as we did above.


_Calibration_ of inferential outcomes is foundational to frequentist statistics, including concepts like coverage of confidence intervals and sample size calculations, false discovery rates, and power calculations of significance tests. Here we take a Bayesian approach to calibration, using the the scope of observations and model configurations quantified by the complete Bayesian model to analyze the range of inferential outcomes, and in particular calibrate them with respect to the simulated truths [[3](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#ref-Betancourt2018a)]. Note that I use calibrate here in the sense of _determining_ what outcomes a model might return, rather than any process of _modifying_ a model to achieve a particular desired outcome.

### 1.3.1 Explicit Calibration
Calibration formally requires a utility function that quantifies how good an inference or decision is in the context of a simulated truth.

Consider, for example, a _decision making process_ that takes in an observation as input and returns an action from the space of possible actions, A,

$$
\begin{alignat*}{6}
a :\; &Y& &\rightarrow& \; &A&
\\
&y& &\mapsto& &a(y)&.
\end{alignat*}
$$
This process could be a Bayesian decision theoretical process informed by posterior expectations, but it need not be. It could just as easily be a process to reject or accept a null hypothesis using an orthodox significance test or any heuristic decision rule.

We then define the net benefit of taking action a∈A when the true data generating process is given by the model configuration θ as

$$
\begin{alignat*}{6}
U :\; &A \times \mathcal{S}& &\rightarrow& \; &\mathbb{R}&
\\
&(a, \theta)& &\mapsto& &U(a, \theta)&.
\end{alignat*}
$$

For example this might be a false discovery rate when choosing between two hypotheses or the outcome of an intervention minus any of its implementation costs. In this context the utility of a decision making process for a given observation becomes

$$
\begin{alignat*}{6}
U :\; &Y \times \Theta& &\rightarrow& \; &\mathbb{R}&
\\
&(y, \theta)& &\mapsto& &U(a(y), \theta)&.
\end{alignat*}
$$

In practice we don't know what the true data generating process is and before the measurement process resolves we don't know what the observed data will be, either. If we assume that our model is rich enough to capture the true data generating process, however, then the complete Bayesian model quantifies reasonable possibilities. Consequently we can construct a distribution of possible utilities by pushing the complete Bayesian model forward along the utility function to give πU(A,S)

![[Pasted image 20220914190532.png]]

$$
\tilde{\theta} \sim \pi_{\mathcal{S}}(\theta)
\\
\tilde{y} \sim \pi_{\mathcal{S}}(y \mid \tilde{\theta})
\\\
U(a(\tilde{y}), \tilde{\theta}).
$$

![[Pasted image 20220914190615.png]]

**This distribution of utilities is particularly useful for understanding how sensitive the measurement process is to the relevant features of the latent system that we're studying. By carefully quantifying what we want to learn in the experiment into an explicit utility function we can formalize how capable our model is at answering those questions.** (BUT FKING HOW)

Note the importance of accurate computation. If our computational methods didn't provide a faithful picture of each possible posterior distribution then we would derive only biased utility distributions that would give us a misleading characterization of our inferences and their consequences.

**For example our decision may be whether or not the true data generating process falls into an irrelevant region near a baseline model configuration, Θirrelevant or a relevant region further away, Θrelevant. The utility function would then be some combination of the false discovery rate, how often we choose the relevant region when the true data generating process lies in the irrelevant region, and the true discovery rate, how often we choose the relevant region when the true data generating process lies in the relevant region.**

By simulating from the prior predictive distribution and running our decision making process we can generate binary values of the indicator functions.

$$
\mathbb{I}[ \text{decide relevant} \mid \pi^{\dagger} \in \Theta_{\text{irrelevant}} ]
$$
and

$$
\mathbb{I}[ \text{decide relevant} \mid \pi^{\dagger} \in \Theta_{\text{relevant}} ].
$$

**The average of these outcomes then estimate Bayesian false discovery rates and Bayesian true discovey rates of the decision making process.**

### 1.3.2 A Bayesian Eye Chart
Regardless of the specific goals of an analysis we are often interested in the general behavior of the posterior distribution induced by possible observations, especially any pathological behavior that might manifest from our model assumptions. Conveniently there are two characteristics of the posterior distribution that can identify a variety of possible problems.

First let's consider the _posterior z__-score_ of a given parameter in the model configuration space,

$$
z[f \mid \tilde{y}, \theta^{\dagger}] =
\frac{ \mathbb{E}_{\mathrm{post}}[f \mid \tilde{y}] - f(\theta^{\dagger}) }
{ \mathbb{s}_{\mathrm{post}}[f \mid \tilde{y} ] },
$$
where θ† is the parameter corresponding to the true data generating process and spost the standard deviation of the function f. **The posterior z-score quantifies how accurately the posterior recovers the true model configuration along this coordinate. Smaller values indicate a posterior that more strongly concentrates around the true value while larger values indicate a posterior that concentrates elsewhere. Note that the posterior z-score captures neither the bias nor the precision of the posterior distribution but rather a combination of the two.**

Likewise the _posterior contraction_ of a given parameter,

$$
c[f \mid \tilde{y}] = 1 -
\frac{ \mathbb{V}_{\mathrm{post}}[f \mid \tilde{y} ] }
{ \mathbb{V}_{\mathrm{prior}}[f \mid \tilde{y} ] },
$$

where V denotes the variance, **quantifies how much the likelihood function from a given observation informs the given function. Posterior contraction near zero indicates that the data provide little information beyond the domain expertise encoded in the prior model, while posterior contraction near one indicates observations that are much more informative relative to the prior model.**

**These two posterior characterizations can identify an array of pathological behaviors that are prone to compromising our inferences. For example a posterior distribution with a high posterior z-score and a high posterior contraction is being forced away from the true value by the observed data and overfitting, at least if the prior model contains the true value. Likewise a posterior distribution with a small posterior z-score and a small posterior contraction is only poorly informed by the observations. On the other hand a posterior distribution with both a small posterior z-score and a large posterior contraction indicates ideal learning behavior. A posterior distribution with a large posterior z-score and a small posterior contraction indicates that the prior model conflicts with the true value.**

![[Pasted image 20220914193453.png]]

Indeed we can identify all of these pathological behaviors by plotting the two characteristics of a given posterior distribution against each other.

![[Pasted image 20220914193538.png]]

If we fit the posterior distribution corresponding to an ensemble of simulations from the prior predictive distribution

$$
\tilde{\theta} \sim \pi_{\mathcal{S}}(\theta)
\\
\tilde{y} \sim \pi_{\mathcal{S}}(y \mid \tilde{\theta}),

$$
then we can visualize the entire distribution of possible posterior behaviors,

$$
z[f \mid \tilde{y}, \tilde{\theta}_{n}]
\  
c[f \mid \tilde{y} ],
$$

with a scatter plot and quickly identify potential problems with our experimental design. **Note that by sampling true model configurations from the prior model we cannot get posterior behaviors that consistently fall into the "Bad Prior Model" neighborhood.**

For example the following scatter plot indicates that the posteriors arising from most prior predictive observations concentrate around the true value reasonably well. It also shows, however, that occasionally the posteriors will strongly more concentrate, and when they do they are prone to concentrating away from the true value and overfitting.

![[Pasted image 20220914193956.png]]

**Where good values transition into bad values depends entirely on the needs of a given application, but I typically start to worry when I see small excesses above a z-score of 4 or large excesses above a z-score of 3.**

**We can follow up on any problematic fits by investigating the corresponding observations, and the likelihood functions they induce (m' so each observation induces a likelihood function?), to see exactly what is leading the posterior distribution astray.**

![[Pasted image 20220914194207.png]]

### 1.3.3 The Limitations of Calibration
**Whether frequentist or Bayesian, model-based calibration is well-defined _only within the context of the assumed model_. In general these calibrations have no application to data generating processes outside of the observational model, at least not unless we expand the model and recompute the calibration to see what the change might be.**


**Consequently any modification to the phenomena, environment, or experimental probe spanned by the model will in general invalidate a Bayesian calibration.** For example even if the latent phenomena are the same, varying environments and experimental probes can lead to very different utilities. What is good enough to answer questions in one particular comtext may not be sufficient to answer questions in different contexts!

Because at least some aspect of the phenomena, environment, and probe are unique to each experiment this means that we cannot rely on black box calibrations derived from default, and typically unquestioned, models. The most robust calibrations are derived from bespoke models capturing the particular circumstances of each application.

The validity of even a bespoke calibration, however, presumes that with enough effort we can actually build a model that captures the true data generating process. A valid calibration requires that we model sufficiently well not only the experimental _design_ but also the often surprising ways that design is actually _implemented_ in practice. Calibrations derived before the data are collected are necessarily optimistic; we can fully understand the utility of our inferences only after we can investigate the revelations hiding in the observed data itself.

### 1.4.1 So Close, Yet So Far Away

In order to critique the adequacy of a given model we have to be able to compare it to the true data generating process.

#### 1.4.1.1 All Models Are Wrong

If our model were sufficiently rich then our observational model πS(y;θ)

would contain the true data generating process, π†; in other words the true data generating process would be one of the data generating processes in our model,

$$
\pi^{\dagger} = \pi_{\mathcal{S}}(y; \theta^{\dagger}), \, \theta^{\dagger} \in \Theta.
$$
![[Pasted image 20220914203028.png]]

Calibrations with respect to this model would then accurately reflect the inferential consequences over actual observations.

**Reality, however, is far richer than any model we could feasibly implement. Consequently any practical observational model will never exactly contain the true data generating process.**

![[Pasted image 20220914203429.png]]

**In this more realistic scenario posterior distributions can't concentrate around the true data generating process no matter the realized observation. _At best_ the posterior distributions will be able to concentrate around the model configurations that best approximate the true data generating process.**

![[Pasted image 20220914203506.png]]

**When the model doesn't contain the true data generating process we can't say much about how meaningful the answers to Questions 1-3 will be to real experiments. In this circumstance model-based calibrations can be arbitrarily distant from how our inferences would actually resolve when applied to real observations.**

#### 1.4.1.2 But Some Are Useful
The calibrations might be reasonable however, if the model captures the structure of the true data generating process that influences our desired inferences.

For example most physical systems that we might analyze are well-defined by Newtownian mechanics to extremely small precision. Even though we know that Newtownian mechanics breaks down at extremely small temporal and spatial scales, it is more than sufficient for most analyses _unless we need to resolve a system at those scales_. In other words the error inherent to phenomenological models based on Newtownian mechanics will be nearly impossible to resolve with most experimental probes.

**The same consideration holds for how we model the latent environment and experimental probe itself. Many experimental probes, for example, are well-approximated by modeling the variation in experimental outcomes with normal probability density functions that emerge from more complex latent interactions. Unless the experimental probe is precise enough, however, we won't be able to resolve the error inherent to this approximation in practice.**

**A model that doesn't capture every precise detail of the true data generating process can still be useful if it captures the details _relevant_ to our particular analysis goals.** To paraphrase George Box, our model is probably wrong but it might still be useful.

**Consequently in practice we shouldn't be asking whether or not our model contains the true data generating process but rather whether or not our model is _close enough_ to the true data generating process _in the directions that matter_.** Consider, for example, conceptually separating the space of all data generating processes P into the features relevant to our analysis goals and the features irrelevant to our analysis goals. In this context we can decompose the distance from a model to the true data generating process, or the total _misfit_, into a _relevant misfit_ and an _irrelevant misfit_.

**A model with both a large relevant misfit and a large irrelevant misfit will yield misleading model-based calibrations as well as ineffective inferences from actual observations.**

![[Pasted image 20220914204636.png]]

**A model with a small relevant misfit, however, will give useful calibrations and inferences _for our particular analysis goals_ no matter how large the irrelevant misfit might be.**

![[Pasted image 20220914204744.png]]

In the Bayesian statistical literature the relationship between an observational model and the true data generating process is often classified with the M categories [[4](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#ref-BernardoEtAl:2009)]. The ideal, and largely unattainable, circumstance where our model contains the true data generating process is known as the _M__-closed_ setting, while the more practical circumstance where our model doesn't contain the true data generating process is known as the _M__-open_ setting.

In this case study we'll consider a compromise between these two extremes, a _M__-good enough_ setting where our model is sufficient for our particular analysis.

