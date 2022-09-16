Or betancourts glossary?


#### Observational process

 "It is any methodology that measures, collects, curates or manipulates observations sensitive to the latent phenomenon. This includes, for example, not only dedicated experiments explicitly designed to interrogate the phenomenon of interest but also retrospective analyses of incidental experiments or previously conducted experiments designed for other purposes."


Note that we distinguish *possible* outcomes of an observational process from *explicitly realized* observations. Betancourt distinguishes them as: $y$ denotes an arbitrary point in the observation space while $\tilde{y}$ denotes a particular point. 

#### Observation space. 
the variation of possible outcomes of an observation process??
with variability sources being epistemological, ontological or others?

#### Data generating process
Probability distributions over the observation space. 

#### True data generating process
The probability distribution that exactly captures the observational process in a given application. 


#### Observational process vs Observation space
???????


#### Observational model 
This small world defines an *observational MODEL* consisting of individual data generating process that each define a possible mathematical narrative of how the data could be generated. m' so the observational MODEL consists of individual probability distributions over the observation space that each define a possible mathematical narrative of how the data could be generated'.  I think this is 
$$
\pi_{\mathcal{S}}(\tilde{y} \mid \theta)$$

#### Data generating process
Probability distributions over the observation space. 
Mathematical narrative of how the data could be generated. 


#### True data generating process
The probability distribution that exactly captures the observational process in a given application. 

#### Model configuration space, $\mathcal{S}$
The subset of data generating processes considered in a given analysis. 
Model configuration space and Observational model can be used interchangeably. 


#### Model configuration
An individual data generating process considered in a given analysis. 

#### Observational model
its the same as the model configuration space (interchangeable). 
It consists of individual data generating process that each define a possible mathematical narrative of how the data could be generated. m' so the observational MODEL consists of individual probability distributions over the observation space that each define a possible mathematical narrative of how the data could be generated'. 

#### Parameterization of an observational model
Is the one-to-one mapping between the model configuration space and the numerical space $\Theta$, such as the real numbers. In other words, a parameterization is the assignment of a unique value, or *parameter* $\theta \in \Theta$, to each model configuration, $s \in \mathcal{S}$. Keep in mind that the parameterizations themselves are not unique; in general there will be many equivalent ways of LABELING model configurations. 
In practice it helps to assign distinct, numerical LABELS to each data generating processes within an observational model?????? are we labelling or assigning values to the parameters of the data generating process????


#### Generative model in machine learning: 
 
In machine learning a generative model is typically defined as a probabilistic model of all quantities that vary from observation to observation; in other words a model over the entire observational space, Y [[1](https://betanalpha.github.io/assets/case_studies/generative_modeling.html#ref-Bishop:2006)]. For example given an observational space parameterized by two variables y=(y1,y2) the conditional model π(y1|y2;θ) would not be generative because it lacks a probabilistic model for y2. Such incomplete model specifications, often denoted _discriminative_ models, commonly arise in regression modeling where the observational space Y×X separates into variates, y∈Y, and covariates, x∈X, and only the conditional relationship π(y|x;θ) is modeled.


#### Narratively generative:
In applied statistical settings "generative" more commonly refers not to how a model is implemented but rather how the model is _interpreted_. Here generative describes models that follow the progressive structure of some assumed data generating process; in other words they model not just the outcome of a measurement but also the internal composition of that measurement. I will refer to this notion of generative as _narratively generative_.


#### _Narratively generative structure_ of a model:
In statistics and computer science causality typically refers not to all possible influences but rather to only those influences that are explicitly modeled. In any practical model we ignore an infinity of physical interactions that we assume are too weak to meaningful affect a given data generating process.


#### KL Divergence

##### Delta estimators
Unfortunately in practice we don't have all that many observations. Typically we are so starved for information that we need to aggregate most, if not all of our data into a single monolithic observation to inform sufficiently precise inferences. Consequently the most common estimators, also known as _delta estimators_, use just N=1 which results large estimation error. (from [[bayes_workflow]])

##### Holdout estimators
_Holdout estimators_ partition a single observation into two groups, one for fitting the model and one for constructing delta estimators of relative predictive performance scores. Although this avoids the bias due to reusing the same observation twice, it introduces its own bias. The problem is that inferences based on subset of the data will not, in general, be characteristic of inferences based on the entirety of the data, especially in complex models. Moreover, the log predictive density evaluated at a subset of the data will not, in general, have any relationship to the log predictive density evaluated over the full data. In other words holdout estimators implicitly estimate the predictive performance in the context of a _a smaller observation_, and we don't know how to correct that to the predictive performance of the full observation except in very simple circumstances.

##### Jackknife estimators (cross validation)
_Jackknife estimators_ average holdout estimators over many different partitions in order to reduce the variance of the delta estimators. While this averaging can be effective it does not eliminate the bias inherent to holdout estimators. Moreover the averaging requires fitting a model multiple times which can quickly exhaust any available computational resources. Jackknife estimators of any predictive performance scores, not just the particular relative predictive performance score we have been considering, are collectively known as _cross validation_ in the machine learning and statistics literature.



#### Prior predictive check

#### Prior pushforward check


#### Posterior predictive check

#### Posterior retrodiction checks


#### Simulation based calibration

#### Residual analysis
Classical residual analysis arises in _curve fitting models_ where observed data fluctuates around one of a family of possible curves f(x;θ) parameterized by the parameters θ,
$$
\pi(y \mid x, \theta) = \text{normal}(y \mid f(x; \theta), \sigma).
$$

Given a "best fit" configuration, θ^(y~), we can overlay the curve f(x;θ^(y~)) and the observed data y~ to investigate possible disagreements. While we can't expect that every datum will be close to the best fit curve, especially when we observe many data each with their own opportunity to fluctuate, the model presumes that these fluctuations will be _uncorrelated_. In other words any deficiency of the curve fitting model will manifest as _systematic_ deviations that persist across many values of x is the residual plot. (from [[bayes_workflow]])

