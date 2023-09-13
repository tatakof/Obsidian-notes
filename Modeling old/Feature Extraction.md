# Deep learning Feature extraction. 

Yann LeCun
https://m.alpha.facebook.com/story.php?story_fbid=10158252423107143&id=722677142


![[Pasted image 20220519113555.png]]

Yann LeCun comment: 

Researcher ins peech recognition, computer vision, and natural language processing in the 2000s were obsessed with accurate representations of uncertainty. 

This led to a flurry of work on probabilistic generative models such as Hidden Markov Models in speech, Markov random fields and constellation models in vision, and probabilistic topic models in NLP, e.g., with latent Dirichlet analysis. 

There were debates at computer vision workshops about "generative models vs discriminative models". There were heroic-yet-futile attempts to build object recognition systems with non-parametric Bayesian methods. 

Much of this was riding on previous work on Bayesian networks, factor graphs and other graphical models. THat's how one learned about exponential family, belief propagation, loopy belief propagation, variational inference, Chinese restaurant process, Indian buffet process, etc. 

But almost none of this work was concerned witht the problem of learning representations. 
Features were assumed to be given. The structure of the graphical model, with its latent variables, was assumed to be given. 
All one had to do was to compute some sort of log likelihood by linearly combining features, and then use on of the above-mentioned sophisticated inference methods to produce marginal distributions over the unknown variables, one of which being the answer, e.g. a category. 

In fact, "exponential family" pretty much means "shallow": the log-likelihood can be expressed as a linearly parameterized function of features (or simple combinations thereof). 

Learning the parameters of the model was seen as just another variational inference problem. 

It's interesting to observe that almost none of this is relevant to today's top speech, vision, and NLP systems. 
As it turned out, solving the problem of learning hierarchical representations and complex functional dependencies was a much more important issue than being able to perform accurate probabilistic inference with shallow models. 
This is not to say that accurate probabilistic inference is not useful. 


