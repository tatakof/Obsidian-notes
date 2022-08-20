from https://betanalpha.github.io/assets/case_studies/generative_modeling.html#ref-Bishop:2006

In machine learning a generative model is typically defined as a probabilistic model of all quantities that vary from observation to observation; in other words a model over the entire observational space, Y [1](https://betanalpha.github.io/assets/case_studies/generative_modeling.html#ref-Bishop:2006)]. For example given an observational space parameterized by two variables y=(y1,y2) the conditional model π(y1|y2;θ) would not be generative because it lacks a probabilistic model for y2. Such incomplete model specifications, often denoted _discriminative_ models, commonly arise in regression modeling where the observational space Y×X separates into variates, y∈Y, and covariates, x∈X, and only the conditional relationship π(y|x;θ) is modeled. see [[bayes_generative-modeling]]