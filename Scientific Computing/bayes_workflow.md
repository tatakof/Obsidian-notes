


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

#### 1.4.1.3 Apples and Oranges
To determine whether or not our model is "good enough" we need to be able to make a more formal comparison between our model and the true data generating process. **This is complicated, however, by the fact that a probabilistic model and a single true data generating process are _different_ objects**.

**A probabilistic model is based on an observational model which itself is a _subset_ of the space of all data generating processes. A true data generating process, however, is just a point in this space. The only formal way to compare a set and a point is inclusion -- is the point within the set or not -- but we saw in the previous section that this was too crude of a comparison for our needs.**

In order to make more sophisticated comparisons we need to manipulate one, or even both, of these objects into the same form that we can then compare in a well-posed way. The most straightforward way to achieve this is to reduce our model into a single _predictive_ data generating process, πpred.

For example any single configuration of our model θ∈Θ defines a possible predictive distribution,
$$
\pi^{\text{pred}}(y) = \pi(y ; \theta).
$$
Typically we use inferences informed by an observation, y~, to select a predictive distribution compatible with our inferences. We could, for instance, select a predictive distribution with a frequentist estimator,
$$
\pi^{\text{pred}}(y \mid \tilde{y}) = \pi(y ; \hat{\theta}(\tilde{y})),
$$
or a posterior expectation value,
$$
\pi^{\text{pred}}(y \mid \tilde{y}) = \pi(y ; \mathbb{m}_{\text{post}}[\theta]),
$$
where

$$
\mathbb{m}_{\text{post}}[\theta] = \mathbb{E}_{\pi(\theta \mid \tilde{y})} [\theta].
$$
**In the Bayesian context we have two other natural ways to reduce the entire model into a single predictive distribution: the prior predictive distribution and the posterior predictive distribution. The former is informed by only the model assumptions while the latter also incorporates what we learn from any observed data. Consequently it is the posterior predictive distribution that best resolves the full inferential consequences of our model.**

Regardless of which prediction strategy we choose we still need to find a way of comparing the predictive data generating process to the true data generating process, ideally focusing on the aspects relevant to our analysis goals.

### 1.4.2 If Everyone Else Jumped Off A Bridge
In science and industry there is a strong aspiration is to reduce comparisons of any sort to a single number, if not a binary classification between "same" and "different". Reducing a comparison to something quantitative, however, often requires jettisoning crucial information and consequently compromising the original purpose of the comparison.

In this section we'll strive for a numerical quantification of proximity between a predictive distribution and a true data generating process, ultimately deriving many of the popular model comparison approaches in the statistics literature while also investigating why they don't provide the critical information we need. For a more detailed discussion of this derivation along with extensive references see [[5](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#ref-Betancourt:2015b)].

Because we will not be using any of the techniques introduced here in the ultimately workflow this section can be skipped. It does, however, help to contextualize how these popular methods relate to that workflow and hence will be useful when communicating the workflow to others.

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
Once we recognize that a Kullback-Leibler divergence is limited to relative comparisons between multiple models and the true data generating process we can simplify the divergence in this context into something a bit more manageable.

Given a parameterization of the observational space we can write the divergence in terms of probability density functions

$$
\begin{align*}
\mathrm{KL} \! \left( \pi^{\dagger} \mid\mid \pi^{\text{pred}} \right)
&=
- \int_{Y} \mathrm{d} y \, \pi^{\dagger}(y)
\log \frac{ \pi^{\text{pred}} (y) }{ \pi^{\dagger}(y) }
\\
&=
- \int_{Y} \mathrm{d} y \, \pi^{\dagger}(y)
\left( \log \pi^{\text{pred}} (y) - \log \pi^{\dagger}(y) \right)
\\
&=
- \int_{Y} \mathrm{d} y \, \pi^{\dagger}(y) \log \pi^{\text{pred}} (y)
+ \int_{Y} \mathrm{d} y \, \pi^{\dagger}(y) \log \pi^{\dagger}(y).
\end{align*}
$$

Because the second term depends only on the true data generating process it cancels when we look at the difference of divergences from multiple models,

$$
\begin{align*}
\Delta(\pi_{1}, \pi_{2})
&\equiv
\mathrm{KL} \! \left( \pi^{\dagger} \mid\mid \pi_{1} \right)
- \mathrm{KL} \! \left( \pi^{\dagger} \mid\mid \pi_{2} \right)
\\
&=
- \int_{Y} \mathrm{d} y \, \pi^{\dagger}(y) \log \pi_{1} (y)
+ \int_{Y} \mathrm{d} y \, \pi^{\dagger}(y) \log \pi^{\dagger}(y)
+ \int_{Y} \mathrm{d} y \, \pi^{\dagger}(y) \log \pi_{2} (y)
- \int_{Y} \mathrm{d} y \, \pi^{\dagger}(y) \log \pi^{\dagger}(y)
\\
&=
- \int_{Y} \mathrm{d} y \, \pi^{\dagger}(y) \log \pi_{1} (y)
+ \int_{Y} \mathrm{d} y \, \pi^{\dagger}(y) \log \pi_{2} (y).
\end{align*}
$$

Consequently in the context of these relative comparisons we need to compute only a

$$
\begin{align*}
\delta_{\pi^{\text{pred}}} \! \left( \pi^{\dagger} \mid\mid \pi^{\text{pred}} \right)
&\equiv
- \int_{Y} \mathrm{d} y \, \pi^{\dagger}(y) \log \pi^{\text{pred}} (y)
\\
&=
\mathbb{E}_{\pi^{\dagger}}[ - \log \pi^{\text{pred}}(y) ].
\end{align*}
$$

These relative predictive performance scores also have the welcome interpretation as the expectation value of logarithmic score functions [[7](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#ref-GneitingEtAl:2007)].

**While relative predictive performance scores allow us to _rank_ models by their relative predictive performance they don't have any meaning when considering a single model in isolation. Consequently they don't actually help in our goal of identifying _why_ a model might be deficient and hence what improvements it needs.**

**Another limitation of this quantification is that it defines only a relative ordering between models. The actual difference between relative predictive performance scores is not particularly interpretable -- regardless of whether the gap is large or small all we can really say is that one model appears to have better predictive performance, and then only in the very narrow context of the Kullback-Leilber divergence.**

**Finally there is one critical limitation that we have so far ignored, but becomes impossible to disregard once we try to actually compute a relative predictive performance score. In order to compute a relative predictive performance score, or the Kullback-Leibler divergence that proceeded it, we need to know the probability density function of both the predictive distribution _and the true data generating process_. In other words all this time we've been presuming that we know already know the truth in order to quantify the performance of a given model. This is an unrealistic assumption, to say the least.**

In practice the only manifestation of the true data generating process to which we have access are actual observations. If we want to utilize relative predictive performance scores in practice then we have to _estimate_ expectations with respect to the true data generating process using only these observations.

#### 1.4.2.3 The Glass Menagerie of Relative Predictive Performance Score Estimators

**Because relative predictive performance scores take the form of an expectation with respect to the true data generating process we can estimate them with Monte Carlo methods using only samples from the true data generating process.** For example if we had many observations 

$$
\{ \tilde{y}_{1}, \ldots, \tilde{y}_{N} \},
$$

then we could construct the Monte Carlo estimator

$$
\hat{\delta} \! \left( \pi \mid\mid \pi^{\text{pred}} \right)
\equiv
\sum_{n = 1}^{N} - \log \pi^{\text{pred}} (\tilde{y}_{n}).
$$
Because Monte Carlo estimators have quantifiable error this could be quite useful if N were large enough to ensure small errors.

Unfortunately in practice we don't have all that many observations. Typically we are so starved for information that we need to aggregate most, if not all of our data into a single monolithic observation to inform sufficiently precise inferences. **Consequently the most common estimators, also known as _delta estimators_, use just N=1 which results large estimation error.**

The situation is even more dire when we need to derive a predictive distribution from our inference. In this case we are left with no auxiliary observations for estimating relative predictive performance scores at all! Most estimation strategies compensate for the dearth of data by _reusing_ the same observation in some way to both fit and evaluate a model.

_Reuse delta estimators_, for example, simply use the same data set for _both_ inference and evaluation. While convenient this results in biased estimators that are particularly insensitive to overfitting.

_Holdout estimators_ partition a single observation into two groups, one for fitting the model and one for constructing delta estimators of relative predictive performance scores. Although this avoids the bias due to reusing the same observation twice, it introduces its own bias. The problem is that inferences based on subset of the data will not, in general, be characteristic of inferences based on the entirety of the data, especially in complex models. Moreover, the log predictive density evaluated at a subset of the data will not, in general, have any relationship to the log predictive density evaluated over the full data. In other words holdout estimators implicitly estimate the predictive performance in the context of a _a smaller observation_, and we don't know how to correct that to the predictive performance of the full observation except in very simple circumstances.

_Jackknife estimators_ average holdout estimators over many different partitions in order to reduce the variance of the delta estimators. While this averaging can be effective it does not eliminate the bias inherent to holdout estimators. Moreover the averaging requires fitting a model multiple times which can quickly exhaust any available computational resources. Jackknife estimators of any predictive performance scores, not just the particular relative predictive performance score we have been considering, are collectively known as _cross validation_ in the machine learning and statistics literature.

**All of these estimation strategies also presume that we can evaluate the log predictive density function exactly, which is unfortunately unrealistic in the the Bayesian setting. While it is straightforward to simulate from the prior predictive and posterior predictive distributions we cannot derive prior predictive or posterior predictive density functions in closed form in all but the simplest models. Consequently in order to estimate relative predictive performance scores based on these predictive distributions we have to go through the additional challenge of estimating the log densities themselves.**

Interestingly different choices of predictive distribution and estimation strategy reproduce many of the model comparison methods popular in statistics and machine learning. Although they can be derived in multiple ways, this unifying relative predictive performance score perspective helps clarify the assumptions implicit in each choice and hence facilitates comparisons between them.


![[Pasted image 20220916093829.png]]

The robust use of relative predictive performance score estimators in practice is both subtle and arduous. If we can even construct an estimator then we still have to carefully quantify its error, including both bias and variance, in order to determine what differences, and hence what ordering of models, is significant. Although some estimation methods do offer heuristics for quantifying some contributions to the overall error, the ultimate success of these heuristics depends on how much those contributions dominate the overall error, which we can rarely if ever quantify.

Most importantly relative predictive performance scores inform only _model comparison_, not the _model criticism_ that we need to address our question. In order to offer constructive criticism we need another way of comparing a predictive distribution to the true data generating process or, more realistically, to the observed data.

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

# 2 Building a Mystery
**If there are no indications that a given model answers any of these four questions poorly then we can proceed to apply it in practice with some confidence that it will provide reasonably robust inferences for the considered inferential goals. On the other hand if there are signs of trouble when investigating these questions then we have to consider improving the model, or occasionally even reducing the ambition of our inferential goals entirely.**

The goal of a principled Bayesian workflow is to guide a practitioner through a regimented model critique that first identifies and then resolves serious deficiencies. Importantly criticisms need to be _interpretable_ in order to inform the practitioner how they can be resolved. This feedback provides the basis for _iterative_ model development that hopefully converges to a model that's just good enough for a given application.

## 2.1 Setting the Stage
Before we can iterate we need to _initialize_ by defining an appropriate context and an initial model.

In order to define an appropriate context we begin with a conceptual analysis of the model that we would fit without being limited by computational resources, time, and mathematical tools. This _aspirational model_, SA, incorporates all of the systematic effects that might influence the measurement process; it might include heterogeneity across individuals or variation across space and time. We might consider background contributions or any other corruption of the latent phenomena as it interacts with the environment and experimental probe. At the same time we might contemplate increasingly more elaborate models of the latent phenomena itself.

Importantly the aspirational model is purely hypothetical and not something that we would ever actually write down. Reasoning about the the aspirational model forces us to reflect on the subtleties of the latent system being studied and the measurement process being used to probe that system. It is an opportunity to brainstorm so that later in model development we might be prepared with plausible hypotheses for any deviant behavior we observe.

Within this abstract aspirational model we can then build an _explicit_ initial model, S1⊂SA.

![[Pasted image 20220918111952.png]]

The initial model should be just sophisticated enough to incorporate the phenomena of scientific interest, but little else. **It will typically include few, if any, systematic effects and only as much domain expertise as needed to motivate a self-consistent initial prior model. Initial models often take the form of some deterministic phenomenological model with the environment and experimental probe being reduced to normal variation, similar to the curve fitting model we considered in [Section 1.4.3](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:retro_check),**

$$
\mathcal{S}_{1}(y \mid \psi, \sigma) = \text{normal}(y \mid f(x; \psi), \sigma).
$$

The _difference_ between the explicit initial model and the conceptual aspirational model, SA∖S1, encapsulates all of the potentially relevant structure ignored by the initial model.

![[Pasted image 20220918113431.png]]

**In particular this abstract difference can be used to motivate summary statistics that isolate these ignored structures, providing the foundations of constructive prior predictive and posterior retrodictive checks. A check isolating possible heterogeneity across groups, for example, is naturally equipped with a possible resolution: the introduction of heterogeneity into the model.**

## 2.2 Computer, Enhance
**If our initial model proves adequate then we have no need of going further. In the more realistic situation where our initial model proves to be inadequate, then we have to address the revealed inadequacies one way or another. This can mean improving our model, but it could also mean changing the experiment or our inferential goals entirely.**

### Issues with Question One: Domain Expertise Consistency

If we learn that our model is not consistent with our domain expertise then we have to modify the aspects of our model in conflict. This often requires more careful consideration of the prior model, but occasionally it can require modifying the observational model as well. For example an observational model violating known constraints often enough might have to changed to explicitly enforce those constraints.

The identification of exactly where to change our model is facilitated by well-chosen summary functions in prior pushforward and prior predictive checks. **Investment in the design of these summary functions rarely goes unrewarded, if not in the current analysis then in future analyses.**

### Issues with Question Two: Computational Faithfulness
Insufficient computational tools can be more challenging to address.

If we are proficient in the current algorithms being used then we can consider more sophisticated configurations and implementations of that algorithm. Alternatively we can reparameterize our model configuration space to implicitly reconfigure the algorithm [[10](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#ref-Betancourt:2019)]. At some point we might have to consider new algorithms entirely.

**By investigating the posterior fits to many simulated observations we might be able to identify the structure of the data, and hence the structure of the simulated true model configuration, that frustrates the current algorithm.** **If, and only if, these model configurations are in conflict with our domain expertise then we can then consider suppressing the pathological behavior with a stronger prior model. We have to take care here, however, as we don't want to rationalize erroneous domain expertise just to ameliorate computational issues. The computational issues might trigger more precise domain expertise, but they shouldn't rationalize fantasies.**

Sometimes computational issues cannot be resolved and instead demonstrate that we are not equipped with the resources needed to tackle the presumed analysis. In that case we might have to consider less ambitious inferential goals, and the simpler, more-computationally-friendly models they require.

### Issues with Question Three: Inferential Adequacy
When model calibration indicates that we are unlikely to meet our inferential goals we need to consider ways to improve our inferences, or weaken the inferential goals entirely.

**Inferences underperform when they cannot exploit enough information about the system being analyzed**. **The only way we can improve our inferences, then, is to incorporate more information into our model**.

**One critical source of information is the domain expertise encoded in the prior model. By reevaluating our domain expertise we might be able to build a more precise prior model that captures more information**. **This is especially critical if we can use our calibrations to identify for what information our inferences are most starved to guide our prior refinement**.

**The other source of information is the observations as encoded in the realized likelihood functions. In particular we can always improve our inferences by considering more elaborate or more precise experimental probes, collecting more data or possibly different kinds of data to better inform the relevant aspects of the true data generating process.** **New data that complements an existing measurement can be particularly effective. For example measurements with the latent phenomena removed or suppressed can help to inform the behavior of the experimental probe or the latent environment, breaking degeneracies that limit how well we can resolve the latent phenomena in the full measurement.**

Finally we have to acknowledge that a better model is not always sufficient to obtain the desired inferences. **Sometimes our initial inferential goals are just too ambitious, and our experiments are too insensitive to the phenomena of interest.** In these cases we might have to use the calibration studies to suggest more realistic goals for the current experiment design.

### Issues with Question Four: Model Adequacy

Finally, if we learn that our model isn't capturing the relevant features of the true data generating process then **we need to _expand_ its boundaries in those relevant directions.**

**Model expansion gives us a sequence of _nested models_, or nested subsets in the space of all possible data generating processes,**
$$
\mathcal{S}_{1} \subset \mathcal{S}_{2} \subset \mathcal{S}_{3} \subset \mathcal{P},
$$
that hopefully move closer and closer to the true data generating process, at least in the relevant directions.

![[Pasted image 20220919111357.png]]

**This iterative model development can be compared to the basic scientific method where we operationalize the vague “compare hypothesis predictions to experiment" and "form new hypotheses" with posterior retrodictive checks identifying inconsistencies and our aspirational model motivating new hypotheses**. That said the proper implementation of the scientific method is a contentious subject spanning philosophy, science, and statistics...so maybe it's best to avoid such comparisons.

We don't want to add complexity arbitrarily, however, lest we end up with an unwieldy model that isn't even adequate for our inferential goals. Instead **we want to expand our model carefully, prioritizing the features that could alleviate the most extreme observed deviations**.

Fortunately the context of the aspirational model, and the summary statistics it motivates, helps to guide this prioritization and make it less overwhelming. **In particular posterior retrodictive checks based on interpretable summary statistics not only identify potential problems but also suggest the structure needed to resolve those problems. We can then focus on the summary statistics that reveal the strongest deviations, laying a deliberately path through the aspiration model that takes us from our initial model towards the true data generating process.**

**If deviations aren't strong enough to motivate an expansion we can also take a closer look by collecting more data or complementary data that induces more precise inferences. This allows us to not only better resolve the latent phenomenology but also any deficiencies of the current model, and hence motivate more principled improvements.**

## 2.3 Stay Where a Kiss Won't Mislead You

Using the data to both fit and evaluate our model is dangerous, but that danger is unavoidable in practice because we can rarely trust that an experiment will be implemented exactly according to its design. In order to figure out how the experimental design was actually implemented in reality, and reason able the intricate systematic effects that arise as a consequence of that implementation, we need to investigate the observed data. In other words we can't trust any of our model calibrations until we can explore what surprises lurk in the data.

An immediate corollary is that while ideas like preregistration can be helpful for documenting the initial inferential goals of an experiment they are nowhere near _sufficient_ for a successful analysis in practice. Preserving a preregistered model only perpetuates its optimistic assumptions about the realization of an experiment. In practice we almost always have to adapt our model to the peculiarities of the observed data.

Fortunately an principled Bayesian workflow can ameliorate the potential danger of using the data to both inform our posterior distribution and our posterior retrodictive checks. In particular by developing a model through iterative _expansion_ where each model iteration is subsumed _within_ a new model model our inferences can always retreat to the previous model configurations if the added structure doesn't better capture the relevant parts of the true data generating process.

Consider for example the previous model configuration space Θi and the new model configuration space Θi+1. If we restrict ourselves to model expansion then the former will always nest within the latter, Θi⊂Θi+1, and all of the previous model behaviors will be available in the new model as well.

![[Pasted image 20220919121315.png]]

Expansion is made more robust when we use prior models that concentrate around the previous, simpler model, similar to the behavior of _penalized complexity priors_ [[11](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#ref-SimpsonEtAl:2017)] The fact that we prioritized the previous model by trying it first suggests that these prior models are naturally compatible with our domain expertise. **Moreover these prior models are straightforward to implement in practice once we parameterize the new model such that the previous model is recovered when one or more new parameters are set to zero, effectively "turning off" the new structure.**

![[Pasted image 20220919121330.png]]

If the additional flexibility introduced into the new model doesn't improve the fit to the observed data then the posterior distributions will collapse back to simpler model configurations that overlap with the previous model.

![[Pasted image 20220919121344.png]]

When the additional flexibility provides a better, fit, however, the posteriors distributions will venture deeper into the new model.

![[Pasted image 20220919121359.png]]

**If the observational data is consistent with model configurations in the previous and the new model then the posterior distribution will stretch across _both_.**

![[Pasted image 20220919121416.png]]

**Because the posterior distribution quantifies _all_ of the model configurations consistent with an observation, the previous model configurations will continue to influence our inferences _until they are no longer compatible with the data_.** **Consequently the worst outcome of adding unneeded structure is only larger uncertainties**. **This makes Bayesian inference particularly robust against overfitting relative to point estimators that quantify only a single model configuration and are easily seduced by the complexity of the new model**.

In other words the combination of model expansion, parsimonious prior models, and full Bayesian inference makes it harder to reach towards unneeded complexity and limits how iterative model development based on posterior retrodictive checks can overfit. That said, just because overfitting is more difficult doesn't mean that it is impossible. **Extreme realizations of a measurement can mimic systematic behavior so well that even a posterior distribution can be fooled away from a simpler truth.**

**Careful calibrations with simulated data can identify when a model is vulnerable to overfitting, as can posterior predictive checks with held out observations if they are available.** **The best protection, however, is thorough documentation of the model development process that allows a community to leverage their collective domain and statistical expertise to identify any signs of overfitting.**

# 3 Work it, Make it, Do it, Makes Us Harder, Better, Faster, Stronger
Iterative evaluation and refinement guides the development of Bayesian models appropriate for the bespoke details of a particular application. Implementing that development, however, can be overwhelming given just how many ways a model can be deficient.

In this section I introduce a _principled Bayesian workflow_ that integrates each of the evaluation techniques we have introduced into a coherent sequence of investigations. This workflow can be thought of as a sort of conceptual checklist to help organize all of the ways a model might disappoint you, and hence manage all of the red flags for which you have to be vigilant.
![[Pasted image 20220919141148.png]]

Each iteration of the workflow proceeds in three phases: the first without considering an explicit model or observed data, the second using a model but no observation, and the third utilizing both. After reviewing each step in these phases we'll review some demonstrative examples of how an iteration might be realized in various circumstances.

In order to implement the steps in this workflow we need access to both _domain expertise_ and _statistical expertise_. **Here domain expertise refers to the experience of those responsible for collecting, curating, or otherwise manipulating the data, as well as stakeholders who will make decisions using the final inferences or any intermediaries who will help stakeholders in that decision-making process.** Statistical expertise refers to proficiency in probabilistic modeling and computation. A robust analysis requires input from both sets of expertise, whether contributed from a single person or multiple individuals in collaboration.

## Pre-Model, Pre-Data

The first phase of this workflow sets the foundations on which we will build our model.

### Step One: Conceptual Analysis

We begin by reasoning about the aspirational model.

In the first iteration we consider exactly what our inferential goals are before contemplating the measurement process, from the latent phenomena of interest through its interactions with the environment and experimental probe and how those interactions manifest as observations.

When we return to this step in future iterations our objective is to expand the aspirational model to encompass any behavior that we had not previously anticipated.

Importantly the outcomes of this step should be only informal, conceptual narratives of the measurement process. All we're trying to do is sit down with the domain experts, whether ourselves or our colleagues, and ask _"How is are data being generated?"_.

**Requirements:** Domain Expertise

### Step Two: Define Observational Space

Given a conceptual understanding of the measurement process we can take our first steps towards a formal mathematical model by defining the observational space, Y in which observations take values. This includes, for example, the number of components and their type, as well as any available metadata informing the context of each component observation.

In later iterations we return to this step only when we expand the observation to include, for example, repeated or complementary measurements.

**Requirements:** Domain Expertise and Statistical Expertise

### Step Three: Construct Summary Statistics

With the observational space formally defined we can construct summary statistics that isolate the consequences of the measurement process that we think will influence our inferential goals, as well as those that we expect to be difficult to model well. These summary statistics then provide the basis for prior predictive checks and posterior retrodictive checks that help to answer [Question One:Domain Expertise Consistency](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:question_one) and [Question Four: Model Adequacy](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:question_four), respectively.

In preparation for prior predictive checks we also want to complement these summary statistics with conceptual thresholds that capture our domain expertise.

**Requirements:** Domain Expertise and Statistical Expertise

## Post-Model, Pre-Data

With the conceptual foundation laid the second phase considers an explicit Bayesian model and its internal consequences.

### Step Four: Model Development

The construction a complete Bayesian model πS(y,θ)

is often facilitated by modeling in stages, first building an observation model, πS(y∣θ), and then building a complementary prior model, πS(θ).

From this perspective the observational model translates the conceptual narrative considered in [Step One](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:conceptual) into formal mathematical narratives of how observations are generated.

In the initial iteration this model should be just sophisticated enough to be able to provide an answer to the inferential questions of interest, although not necessarily a good one. If we return to this step in later iterations then we will need to provide a more detailed translation of those conceptual narratives.

The prior model then complements the observational model with just enough domain expertise to ensure that the complete Bayesian model is well-behaved and compatible with our domain expertise [[12](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#ref-GelmanEtAl:2017a)]. If our initial prior model isn't adequate then when we return to this step in later iterations we will need to incorporate additional information with a more careful prior model that refines our domain expertise.


That said, as our models grow in sophistication the story of the data generating process becomes harder and harder to encapsulate entirely within the observational model. Consider, for example, a model that generates each component of the observational space, yn, from a corresponding _local_ parameter, θn,
$$
\pi_{\mathcal{S}}(y_{n} | \theta_{n}),
$$
while the local parameters are moderated by a _global_ parameter ϕ, parameters,
$$
\pi_{\mathcal{S}}(\theta_{n} \mid \phi).
$$
In this case our observational model is formally given by only
$$
\pi_{\mathcal{S}}(y \mid \theta, \phi) =
\prod_{n = 1}^{N} \pi_{\mathcal{S}}(y_{n} | \theta_{n})
$$
while the prior model is given by
$$
\pi_{\mathcal{S}}(\theta, \phi) =
\left[ \prod_{n = 1}^{N} \pi_{\mathcal{S}}(\theta_{n} \mid \phi) \right]
\cdot \pi_{\mathcal{S}}(\phi).
$$
The data generating narratives, however, might more naturally encapsulate both how the data are generated from the local parameter configurations and how the local parameter configurations are generated from the global parameter configuration,

$$
\pi_{\mathcal{S}}(y, \theta \mid \phi)
=
\prod_{n = 1}^{N}
\pi_{\mathcal{S}}(y_{n} | \theta_{n}) \, \pi_{\mathcal{S}}(\theta_{n} \mid \phi).
$$
We can avoid this ambiguity entirely by developing the complete Bayesian model as a whole, with a conditional decomposition that spans the all of the model configuration and observational spaces,
$$
\pi_{\mathcal{S}}(y, \theta, \phi) =
\left[ \prod_{n = 1}^{N}
\pi_{\mathcal{S}}(y_{n} | \theta_{n}) \, \pi_{\mathcal{S}}(\theta_{n} \mid \phi)
\right] \cdot \pi_{\mathcal{S}}(\phi).
$$
**Such _generative_ modeling allows us to tell our data generating story sequentially without having to worry about which chapters fall into the prior model and which fall into the observational model.**

**Requirements:** Domain Expertise and Statistical Expertise

### Step Five: Construct Summary Functions

Given an explicit model, and hence model configuration space, we can construct principled summary functions over the model configuration space to set the stage for prior pushforward checks.

**We might also use the structure of the model to introduce new summary statistics for prior predictive and posterior retrodictive checks. For example we might add summary statistics that are sensitive to the heterogeneity of certain components in our model.**

**In future iterations we can also take this opportunity to exploit any information about the deficiencies encountered in previous iterations to motivate new summary functions.**

### Step Six: Simulate Bayesian Ensemble

We are now ready to evaluate the consequences of our model assumptions by investigating the behavior of an ensemble of reasonable model configurations and observations sampled from the Bayesian joint distribution, πS(y,θ).

Given a conditional decomposition of the complete Bayesian model we can readily generate this ensemble with ancestral sampling. In particular if we've specified a prior model and an observational model then we can first simulate model configurations from the prior distribution,
$$
\tilde{\theta} \sim \pi_{\mathcal{S}}(\theta),
$$
and then observations from the corresponding data generating process,
$$
\tilde{y} \sim \pi_{\mathcal{S}}(y \mid \tilde{\theta} ).
$$
**Together each simualated pair (y~,θ~)adds an independent sample to our ensemble.**

**Without a useful conditional decomposition we have to consider other means of generating samples from the complete Bayesian model, such as Markov chain Monte Carlo.**

**Requirements:** Statistical Expertise

### Step Seven: Prior Checks

**We can answer [Question One: Domain Expertise Consistency](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:question_one) with the information provided by prior pushforward checks of the summary functions constructed in [Step Five](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:summary-functions) or with prior predictive checks of the summary statistics constructed in [Step Three](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:summary-stats) and [Step Five](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:summary-functions).**

**If the prior predictive checks indicate conflict between the model and our domain expertise then we have to return to [Step Four](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:model-development) and refine our model.**

**Requirements:** Domain Expertise

### Step Eight: Configure Algorithm

Once satisfied with the consistency of the domain expertise in our model we move onto the possible posterior distributions that result from our complete Bayesian model, which itself requires setting up a probabilistic computational algorithm.

Here we specify our algorithm and any configurable settings, for example we might decide to use `Stan` along with its default settings. In future iterations we might have to tweak those settings in response to computational failures.

**Requirements:** Statistical Expertise

### Step Nine: Fit Simulated Ensemble

With an algorithm locked and loaded we can proceed to **_fit_, or estimate expectation values with respect to,** the posterior distributions induced from each of our simulated observations,

$$
\pi_{\mathcal{S}}(\theta \mid \tilde{y}).
$$
**Requirements:** Statistical Expertise

### Step Ten: Algorithmic Calibration

By fitting the entire ensemble of posterior distributions we can probe the utility of our chosen algorithm and help answer [Question Two: Computational Faithfulness](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:question_two), at least within the context of the model assumptions.

For example if the designated computational method features self-diagnostics, such as R^ for Markov chain Monte Carlo in general and divergences for Hamiltonian Monte Carlo in particular, **then we can look for failed diagnostics across the distribution of posterior fits.** **Even if our chosen method doesn't have its own diagnostics we can evaluate its performance by performing simulation-based calibration**.

Failures indicate that we may need return to [Step Eight](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:config-algo) and improve the tuning or implementation the chosen computational method, or select another method altogether.

**We can also correlate failed fits with the corresponding simulated observations and model configurations.** **This can potentially identify poorly-identified likelihood functions that result in posterior distributions pathological to the computational method being used.** The propensity for such poor behavior can then be ameliorated by returning to [Step Four](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:model-development) and incorporating additional domain expertise or even returning to [Step One](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:conceptual) and considering new experimental designs that might result in more manageable likelihood functions.

**Requirements:** Statistical Expertise

### 3.0.1 Step Eleven: Inferential Calibration

Once we trust the faithfulness of our reconstructed posterior distributions we can consider the breadth of inferences they provide to help answer [Question Three: Inferential Adequacy](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:question_three).

**In general we can always consider the distribution of posterior z-scores against posterior contractions to identify common pathologies in our inferences. If there are indications of undesired behavior, such as overfitting or non-identifiability, then our model may not be sufficient.**

**When an explicit decision-making process has been established we can also calibrate the performance of this process by constructing the distribution of utilities over our simulated Bayesian ensemble**. **For example if a discovery claim is to be made then we might compute the corresponding false discovery rates and true discovery rates within the context of our model.** If these utilities are not satisfactory then we have to consider a more informed model or maybe even a different decision-making process.

In either case we might have to return to [Step One](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:conceptual) to consider an improved experimental design or tempered scientific goals. Sometimes we may only need to return to [Step Four](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:model-development) to incorporate additional domain expertise to improve our inferences.

**Requirements:** Domain Expertise and Statistical Expertise

## Post-Model, Post-Data

If [Question One: Domain Expertise Consistency](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:question_one), [Question Two: Computational Faithfulness](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:question_two), and [Question Three: Inferential Adequacy](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:question_three) have been satisfactorily answered within the scope of the model then we can finally proceed to fitting the observed data and confront [Question Four: Model Adequacy](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:question_four). **Once we consider the observed data we introduce a vulnerability to overfitting and so we must be extremely vigilant in how we further develop our model in subsequent iterations of the workflow.**

### Step Thirteen: Diagnose Posterior Fit

**We have to be careful, however, as the algorithmic calibration won't be relevant to the observed data if our model isn't close enough to the true data generating process.** Consequently we need to be careful to check any diagnostics of our computational method on the fit of the observed data as well.

**If any diagnostics indicate poor performance then not only is our computational method suspect but also our model might not be rich enough to capture the relevant details of the observed data. At the very least we should return to [Step Eight](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:config-algo) and enhance our computational method.**

**Requirements:** Statistical Expertise

### Step Fourteen: Posterior Retrodictive Checks

To really get a handle on [Question Four: Model Adequacy](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:question_four) we have to perform careful posterior retrodictive checks for each of our summary statistics.

**If there are indications of problems that we already suspected in our aspirational model then we can return to [Step Four](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:model-development) and augment the model to account for the observed deviant behavior.** **When the behavior is more surprising, however, then we really should go all the way back to [Step One](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:conceptual) and reconsider our conceptual analysis of the experiment to motivate principled model improvements. If the indications are weak then we can also return to [Step One](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:conceptual) to consider expanding our observation to improve our inferences and better resolve the potential deviation.**

**In order to avoid biasing our model development by overfitting to the observed data we have to be careful with what information we take with us when we start a new iteration of the workflow**. **Specifically we want the _qualitative failure_ of a posterior retrodictive check to motivate model expansion, not the _quantiative features of the observed data itself_. In other words a posterior retrodictive check should serve only to trigger our domain expertise, and our domain expertise should then be solely responsible for the continued model development. The more disciplined we can be here the more less vulnerable our model development will be to overfitting.**

**Requirements:** Domain Expertise and Statistical Expertise

### Step Fifteen: Celebrate

Finally if we can make it through the workflow with a model that indicates no deficiencies relevant to our inferential goals then the iterations terminate and we can celebrate a hard-earned success.

**Requirements:** A Tasty Beverage


## 3.1 Example Workflow Executions

Each iteration of this principled Bayesian workflow will play out a little bit differently depending on what deficiencies we encounter. Perhaps most importantly the realized workflow will depend on which steps we actually consider. While implementing the entire workflow is the most robust we often have to make compromises due to limited time or computational resources. Or maybe we just want to live dangerously.

### 3.1.1 Total Body Workout

The most robust workflow is a complete workflow. Each iteration resolves differently depending on which step encounters problems.

#### Dealing With Incompatible Model Assumptions

For example consider a model where the consequences of the inherent assumptions are inconsistent with our domain expertise. In that case the prior checks would fail and lead us back to the model development step for the next round of iteration.

![[Pasted image 20220920164628.png]]

#### Dealing With Inadequate Inferences

Similarly if our model isn't expected to be precise enough or answer the questions we need then the inferential calibration would fail. Here we respond by going all the way back to the conceptual analysis to consider experiments with larger observations and, hopefully, enough information to answer our questions.

![[Pasted image 20220920164656.png]]

#### Dealing With An Inadequate Model

A model that doesn't approximately capture the true data generating process well enough should result in a failed posterior retrodictive check.

If the failure was a behavior that we had previously considered then we can restart at the model development step.

![[Pasted image 20220920164721.png]]

When the behavior is more surprising, however, we have to go all the way back up to step one to consider the conceptual context of the observed behavior.

![[Pasted image 20220920164737.png]]

#### Exhaustive Success

The most desirable outcome of the workflow is an iteration that reaches step fifteen after implementing each intermediate step. **This doesn't mean that our model is an exact representation of reality, just one that is good enough for the context of our particular application.**

![[Pasted image 20220920164804.png]]

### 3.1.2 Compromised Integrity

In practice we might have to pick and choose amongst the steps in the complete workflow. Some compromises, however, are more useful than others.

### 3.1.3 Only Fits

Most Bayesian analyses one will encounter in practice just want to build and fit a model without asking too many questions. The utility of these analyses depends on how lucky one gets with that initial model and the robustness of the computational algorithm.

![[Pasted image 20220920164829.png]]

### 3.1.4 Fits With Algorithm Tuning

More sophisticated users might also follow up on diagnostic problems encountered during the fit of the posterior distribution from the observed data, for example by modifying the `adapt_delta` configuration in the dynamic Hamiltonian Monte Carlo implementation in `Stan`, until there are no indications of computational problems.

![[Pasted image 20220920164856.png]]

### 3.1.5 No Calibration

By far the most expensive step of the complete workflow is [Step Nine](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:fit-simu) which requires fitting not just one posterior but an entire ensemble of them. Consequently this step, and the calibration steps that proceed it, can be impractical in practice.

Implementing every other step, however, provides much more robustness than a single naive fit alone. This reduced workflow is particularly robust if we are using modeling techniques that have already been studied for their algorithmic and inferential pathologies so that we already know how to implement them effectively.

![[Pasted image 20220920164914.png]]

### 3.1.6 Simulation Study

Complementing a calibration free workflow is a pure simulation study that studies the potential problems of a model, and the experimental design it encodes, solely within the assumptions of that model. This is a powerful way both to evaluate experiments before the experiment is build -- let alone any data are collected -- and to study the behavior of particular modeling techniques in isolation.

![[Pasted image 20220920164946.png]]

**Simulation studies are incredibly useful to help build our understanding and prepare us for more principled modeling. Consequently we should be sure to celebrate these analyses, too.**

![[Pasted image 20220920165001.png]]

# 4 Close Enough For An Effective Demonstration

In order to demonstrate this workflow properly let's a consider a relatively simple example of an analysis that might arise in a science lab. We have been tasked with analyzing data collected by a precocious young student who was instructed to aim a collection of detectors onto a radioactive specimen that emits a constant flow of particles. They dutifully collected data and collated it into a file which has just arrived in our inbox.


...

### Step Three: Construct Summary Statistics

There are N=1000 components in each observation, one for each detector. We could analyze each component independently but, because we have assumed that the detectors are all identical, we can analyze their ensemble response with a _histogram_ of their counts. **In other words we consider the histogram of detector counts _as a collection of summary statistics_!**

