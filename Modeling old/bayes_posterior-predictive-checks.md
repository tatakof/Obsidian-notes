statistical rethinking 2nd edition

"Posterior predictive checks combine uncertainty about parameters, as described by the posterior distribution, with uncertainty about outcomes, as described by the assumed likelihood function.  These checks are useful for verifying that your software worked correctly. They are also useful for prospecting for ways in which your models are inadequate"


------------------------------------
https://stats.stackexchange.com/questions/115157/what-are-posterior-predictive-checks-and-what-makes-them-useful
Posterior predictive checks are, in simple words, "simulating replicated data under the fitted model and then comparing these to the observed data" ([Gelman and Hill, 2007, p. 158](http://www.stat.columbia.edu/~gelman/arm/)). So, you use posterior predictive to "look for systematic discrepancies between real and simulated data" ([Gelman et al. 2004, p. 169](http://www.stat.columbia.edu/~gelman/book/)).




Posterior predictive checks are helpful in assessing if your model gives you "valid" predictions about the reality - do they fit the observed data or not. It is a helpful phase of model building and checking. It does not give you a definite answer on if your model is "ok" or if it is "better" then other model, however, it can help you to check if your model makes sens.

This is nicely described in **LaplacesDemon** vignette [_Bayesian Inference_](https://cran.r-project.org/web/packages/LaplacesDemon/vignettes/BayesianInference.pdf):

"Comparing the predictive distribution $yrep$ to the observed data $y$ is generally termed a "posterior predictive check". This type of check includes the uncertainty associated with the estimated parameters of the model, unlike frequentist statistics.

Posterior predictive checks (via the predictive distribution) involve a double-use of the data, which violates the likelihood principle. However, arguments have been made in favor of posterior predictive checks, provided that usage is limited to measures of discrepancy to study model adequacy, not for model comparison and inference (Meng 1994).

Gelman recommends at the most basic level to compare $yrep$ to $y$, looking for any systematic differences, which could indicate potential failings of the model (Gelman et al. 2004, p. 159). It is often first recommended to compare graphical plots, such as the distribution of $y$ and $yrep$.""


----------------------------------------------

