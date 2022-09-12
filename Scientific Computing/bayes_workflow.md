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

