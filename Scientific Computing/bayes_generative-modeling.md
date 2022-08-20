# Definitions
- Generative model in machine learning: 
	In machine learning a generative model is typically defined as a probabilistic model of all quantities that vary from observation to observation; in other words a model over the entire observational space, Y [[1](https://betanalpha.github.io/assets/case_studies/generative_modeling.html#ref-Bishop:2006)]. For example given an observational space parameterized by two variables y=(y1,y2) the conditional model π(y1|y2;θ) would not be generative because it lacks a probabilistic model for y2. Such incomplete model specifications, often denoted _discriminative_ models, commonly arise in regression modeling where the observational space Y×X separates into variates, y∈Y, and covariates, x∈X, and only the conditional relationship π(y|x;θ) is modeled.
	


Generative modeling is often suggested as a useful approach for designing probabilistic models that capture the relevant structure of a given application. The specific details of this approach, however, is left vague enough to limit how useful it can actually be in practice. In this case study I present an explicit definition of generative modeling as a way to bridge implicit domain expertise and explicit probabilistic models, motivating a wealth of useful model critique and construction techniques.

# 1 Generating What Now?

An immediate problem with the concept of "generative modeling" is that the term isn't always used consistently. In particular what makes a model "generative" can be very different in fields dominated by machine learning and fields dominated by contemporary applied statistics. To construct any self-consistent formalization of the term we have to be careful to differentiate between these two colloquial uses.

## 1.1 Generative As Sampling

In machine learning a generative model is typically defined as a probabilistic model of all quantities that vary from observation to observation; in other words a model over the entire observational space, Y

[[1](https://betanalpha.github.io/assets/case_studies/generative_modeling.html#ref-Bishop:2006)]. For example given an observational space parameterized by two variables y=(y1,y2) the conditional model π(y1|y2;θ) would not be generative because it lacks a probabilistic model for y2. Such incomplete model specifications, often denoted _discriminative_ models, commonly arise in regression modeling where the observational space Y×X separates into variates, y∈Y, and covariates, x∈X, and only the conditional relationship π(y|x;θ) is modeled.