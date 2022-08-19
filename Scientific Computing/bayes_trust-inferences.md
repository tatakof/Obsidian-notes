Ideally the true data generating process, or at least the best approximation to it within our observational model, would fall into a neighborhood of high posterior probability. That accuracy would ensure that whatever conclusions we draw from our model, in particular the decisions informed by those inferences, would be faithful to the real latent system being analyzed.

In general, however, there are no such guarantee in Bayesian inference. The posterior distribution naively follows the information encoded in the model and the observation. Without a carefully designed model the posterior distribution is vulnerable to being led astray by irrelevant quirks in a given observation, ending up far away from the desired model configurations.
Bayesian inference provides a procedure for constructing inferences but it offers no general guarantees on the overall behavior of those inferences. If we want to ensure robust inferences then we at least need to attempt some _calibration_ in order to determine how we expect our model to perform. (see [[bayes_calibration]])