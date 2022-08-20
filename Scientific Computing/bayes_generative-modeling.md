# Definitions
- Generative model in machine learning: 
	In machine learning a generative model is typically defined as a probabilistic model of all quantities that vary from observation to observation; in other words a model over the entire observational space, Y [[1](https://betanalpha.github.io/assets/case_studies/generative_modeling.html#ref-Bishop:2006)]. For example given an observational space parameterized by two variables y=(y1,y2) the conditional model π(y1|y2;θ) would not be generative because it lacks a probabilistic model for y2. Such incomplete model specifications, often denoted _discriminative_ models, commonly arise in regression modeling where the observational space Y×X separates into variates, y∈Y, and covariates, x∈X, and only the conditional relationship π(y|x;θ) is modeled.
- Narratively generative: 
	
	


Generative modeling is often suggested as a useful approach for designing probabilistic models that capture the relevant structure of a given application. The specific details of this approach, however, is left vague enough to limit how useful it can actually be in practice. In this case study I present an explicit definition of generative modeling as a way to bridge implicit domain expertise and explicit probabilistic models, motivating a wealth of useful model critique and construction techniques.

# 1 Generating What Now?

An immediate problem with the concept of "generative modeling" is that the term isn't always used consistently. In particular what makes a model "generative" can be very different in fields dominated by machine learning and fields dominated by contemporary applied statistics. To construct any self-consistent formalization of the term we have to be careful to differentiate between these two colloquial uses.

## 1.1 Generative As Sampling

In machine learning a generative model is typically defined as a probabilistic model of all quantities that vary from observation to observation; in other words a model over the entire observational space, Y

[[1](https://betanalpha.github.io/assets/case_studies/generative_modeling.html#ref-Bishop:2006)]. For example given an observational space parameterized by two variables y=(y1,y2) the conditional model π(y1|y2;θ) would not be generative because it lacks a probabilistic model for y2. Such incomplete model specifications, often denoted _discriminative_ models, commonly arise in regression modeling where the observational space Y×X separates into variates, y∈Y, and covariates, x∈X, and only the conditional relationship π(y|x;θ) is modeled.

One immediate benefit of a model π(y;θ) that spans the entire observational space is that, at least in theory, we can construct exact sampling mechanisms for all of the variables in the observational space,

$$
\tilde{y} \sim \pi(y; \theta),
$$
for each model configurations θ. For example the non-generative conditional model π(y1|y2;θ) admits sampling mechanisms for y1 only once y2 has been fixed to a particular value, but we have no natural way to choose such a value. The generative model π(y1|y2;θ)π(y2;θ), however, admits sampling mechanisms for y2 which then enables ancestral sampling.

Indeed the phrase "generative model" is often used colloquially to imply probabilistic modelings equipped, if not outright defined, by an explicit, exact sampling mechanism from which we can "generate" samples in practice. I will refer to this notion as _procedurally generative_.

One way to construct explicit, exact sampling algorithms is to utilize a conditional decomposition of the observational model π(y;θ) into a sequence of one-dimensional conditional probability distributions,

$$
\pi(y_{1}, \ldots, y_{n}, \ldots, y_{N}; \theta)
=
\left[ \prod_{n = 2}^{N} \pi(y_{n} | y_{1}, \ldots, y_{n - 1}; \theta) \right]
\, \pi(y_{1}; \theta),
$$

where each yn is a one-dimensional variable. If we can efficiently generate exact samples from these one-dimensional distributions then we can generate exact samples from the entire model through ancestral sampling.

In contemporary machine learning ancestral sampling mechanisms have largely given way to _pushforward_ sampling mechanisms. Here the observational model π(y;θ) is defined only implicitly as the pushforward of some simple base distribution, π(x), along a family of complicated transformations, ϕθ:X→Y,
$$
\pi(y; \theta) = (\phi_{\theta})_{*} \pi(x).
$$
If the base distribution is engineered to admit an efficient exact sampling mechanism then we can immediately generate exact samples from these pushforward distributions by applying the transformations to base samples,

$$
\begin{align*}
\tilde{x} &\sim \pi(x)
\\
\tilde{y} &= \phi_{\theta}(\tilde{x}).
\end{align*}
$$
These families of complex transformations are often built out of popular machine learning techniques for function approximation, such as neural networks and kernel methods, resulting in popular methods such as Generative Adversarial Networks [[2](https://betanalpha.github.io/assets/case_studies/generative_modeling.html#ref-GoodfellowEtAl:2014)].

A procedurally generative _Bayesian model_ π(y,θ) requires an exact sampling mechanism that samples the variables in the observational space _and_ the model configuration space. For example by exploiting the conditional decomposition
$$
\pi(y, \theta) = \pi(y | \theta) \, \pi(\theta)
$$
we can build a procedurally generative Bayesian model by combining a procedurally generative observational model π(y|θ), as discussed above, with a procedurally generative prior model π(θ). Because we cannot generate samples from unnormalizeable prior models, such as those specified by uniform density functions over the real line, these improper prior models immediately obstruct procedurally generativity.

That said procedural generation doesn't require that we utilize this particular conditional decomposition. _Any_ conditional decomposition of the full Bayesian model π(y,θ) into well-defined, one-dimensional conditional probability distributions will admit ancestral sampling, and there are many of these conditional decompositions to consider. For example a relatively low-dimensional model π(y1,y2,θ1,θ2) admits 24 different one-dimensional conditional decompositions!

![[Pasted image 20220820110927.png]]

In practice some of these decompositions might result in simpler conditional dependencies which can facilitate the implementation of ancestral sampling. The practical challenge is engineering not just any conditional decomposition but a particularly useful one.

## 1.2 Generative As Story Telling
In applied statistical settings "generative" more commonly refers not to how a model is implemented but rather how the model is _interpreted_. Here generative describes models that follow the progressive structure of some assumed data generating process; in other words they model not just the outcome of a measurement but also the internal composition of that measurement. I will refer to this notion of generative as _narratively generative_.


Any model with a narrative interpretation tells a set of stories, and consequently we can utilize familiar storytelling techniques to understand the structure of these models. For example consider that stories are often told as a sequence of smaller, constituent stories, with each constituent story building upon and referencing previous constituent stories in the progression of the overall narrative. Books are constructed from chapters, television series from episodes, plays from acts, and so on. Likewise a narratively generative model can be built from smaller, component models, each capturing one part of some larger data generating story.

A narratively generative Bayesian model π(y,θ) defines a collection of mathematical stories for how the data could be generated, with the model configurations θ labeling each story. The narrative structure of these stories implies a distinguished conditional decomposition of π(y,θ) where each conditional distribution captures just one part of the data generating story. This distinguished conditional decomposition then immediately defines a distinguished directed graphical model representation where leaf nodes can contain only data variables and any root nodes can contain only model configuration variables.


For example consider the Bayesian model that we introduced in the previous section, π(y1,y2,θ1,θ2). The simplest narratively generative decomposition separates the joint model into an observational model, π(y1,y2|θ1,θ2), and a prior model, π(θ1,θ2).


![[Pasted image 20220820113304.png]]


A more refined story further decomposes the observational model or the prior model.

![[Pasted image 20220820113439.png]]

The most refined story decomposes both of these component models into one-dimensional component models.

![[Pasted image 20220820113455.png]]



Each of these directed graphical models captures a different set of mathematical narratives for how the assumed data generating process might behave. The fewer variables in each node the more refined those stories are. The simpler and more coherent the overall narrative the fewer arrows will connect each node, and the more linear the probabilistic graphical model will appear. The more convoluted the story the more the nodes will influence each other, and the more connected the network of arrows between the nodes will be.


![[Pasted image 20220820113801.png]]

Conditioning on observed data y~ results in a posterior distribution over the model configurations
$$
\pi(\theta \mid \tilde{y}) \propto \pi(\tilde{y}, \theta)
$$

that quantifies how consistent each the possible mathematical stories is with those observed outcomes.


![[Pasted image 20220820114242.png]]


In other words an ideal narratively generative model captures all of the possible data generating stories so that our posterior distribution can identify which of those stories well-approximate the true data generating process.

By introducing a precise interpretation for internal structure of a model, this narrative perspective provides a bridge between explicit mathematical models and our implicit domain expertise. This connection then provides a foundation for a wealth of powerful modeling techniques.

For example this bridge can help us understand the limitations of a given model and any derived inferences. If the mathematical stories captured by the model are meaningful only in a narrow circumstance then we know that we shouldn't expect any inferences or predictions derived from that model to be useful outside of those circumstances.

At the same time understanding the circumstances in which those mathematical stories are relevant also facilitates model critique. If none of the stories are even approximately relevant to a given application then we probably should consider another model. This critique is especially useful in the use of prefabricated models which are often applied without any consideration of relevance. By first recognizing the mathematical narratives implicit in a prefabricated model we make it easier to recognize when that model is applicable and when its not.


Perhaps most importantly a narrative perspective aids the development of bespoke models customized to a given application. Narrative structure provides the foundation on which we can translate our implicit domain expertise about a system being studied into explicit probabilistic models. We will explore narrative model building techniques in depth in [Section 2](https://betanalpha.github.io/assets/case_studies/generative_modeling.html#sec:building_techniques).


## 1.3 The Best of Both Worlds
**Models that are both procedurally _and_ narratively generative are particularly useful in practice. While the narrative focus facilitates model building through narratively meaningful conditional decompositions, the procedural focus allows us to _simulate_ from the data generating processes assumed by that model.**

These simulations are extremely useful for evaluating the consequences of our modeling assumptions, including prior checks, algorithmic Bayesian calibration, and inferential Bayesian calibration. For more see [my workflow case study](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html).


# 2 Advanced Narrative Techniques

Embracing a narrative focus not only clarifies many of the more subtle aspects of probabilistic model building but also motivates a variety of powerful model building techniques, each derived from an intuitive storytelling consideration. In this section we'll review many of these insights and their practical consequences.

## 2.1 Clear and Concise Language
Poor story telling can obfuscate even the simplest story, burying a straightforward narrative underneath confusing language and unnecessary complexity. In narratively generative modeling the language in which we tell our stories is the _parameterization_ of the observational space and the model configuration space; in particular these parameterizations determine the complexity of any conditional decomposition of the joint model. Consequently the apparent intricacy of a narratively generative model can be determined more by how these spaces are parameterized rather than any inherent complexity of the stories they describe.


For example consider the common assumption that an identical measurement is repeated N times without the outcome of the replications directly influencing each other in any way. If we directly parameterize the observational space with the variables that capture the individual outcome of these measurements, y1,…,yn,…,yN, then this narrative assumption implies that these variables are conditionally independent given a particular configuration of the measurement process,

$$
\begin{align*}
\pi(y_{1}, \ldots, y_{n}, \ldots, y_{N}, \theta)
&= \pi(y_{1}, \ldots, y_{n}, \ldots, y_{N} | \theta) \, \pi(\theta)
\\
&= \left[ \prod_{n = 1}^{N} \pi(y_{n} \mid \theta) \right] \pi(\theta).
\end{align*}
$$
Moreover these conditional distributions are exactly the same.


This conditional independence implies a particularly streamlined directed graphical model representation. Because the conditional distributions are identical we can also utilize the plate notation for an even more compact notation.


![[Pasted image 20220820121302.png]]


While reparameterizing the observational space away from this natural parameterization doesn't change the stories captured by the mathematical model, it does complicate the resulting narratively generative structure. For example if we consider parameterizing the observations in terms of the _differences_ of each measurement,

$$
\begin{align*}
\Delta_{1} &= y_{1}
\\
\Delta_{2} &= y_{2} - y_{1}
\\
&\ldots
\\
\Delta_{n} &= y_{n} - y_{n - 1}
\\
&\ldots
\\
\Delta_{N} &= y_{N} - y_{N - 1}
\end{align*}
$$

such that
$$
y_{n} = \sum_{n' = 1}^{N} \Delta_{n'},
$$

then the conditional decomposition becomes much complicated,

$$
\pi(\Delta_{1}, \ldots, \Delta_{n}, \ldots, \Delta_{N}; \theta)
=
\left[ \prod_{n = 2}^{N}
\pi(\Delta_{n} \mid \Delta_{1}, \ldots, \Delta_{n - 1}, \theta) \right]
\, \pi(\Delta_{1} \mid \theta) \, \pi(\theta).
$$
Even for the case N=3 the directed graphical model representation becomes difficult to draw clearly.

![[Pasted image 20220820121607.png]]

An insightful parameterization of the observational and model configuration spaces can better reveal the latent narrative structure of a model, facilitating not only model building but also computational inference with that model.

## 2.2 Flashbacks and Flashforwards
Stories proceed in a sequence of causes and effects, with each constituent story capturing one, the other, or both in the progression of the narrative. These constituent stories are often presented in a strict temporal order, but non-chronological presentation can be a useful technique for emphasizing certain aspects of the larger story.








