### R-hat
https://mc-stan.org/rstan/reference/Rhat.html

The `Rhat` function produces R-hat convergence diagnostic, which compares the between- and within-chain estimates for model parameters and other univariate quantities of interest. If chains have not mixed well (ie, the between- and within-chain estimates don't agree), R-hat is larger than 1. We recommend running at least four chains by default and only using the sample if R-hat is less than 1.05. Stan reports R-hat which is the maximum of rank normalized split-R-hat and rank normalized folded-split-R-hat, which works for thick tailed distributions and is sensitive also to differences in scale.



https://stats.stackexchange.com/questions/418142/low-effective-sample-size-but-good-r-hat-is-this-a-problem

In [BDA3](http://www.stat.columbia.edu/%7Egelman/book/) on page 285, they mention that R-hat is an estimate of "the factor by which the scale of the current distribution for [a particular univariate parameter] might be reduced if the simulations were continued in the limit n→∞." Because your R-hat is so close to 1, this means that it's unlikely that running the simulation any longer will be of much use.





### Bulk-ESS

The `ess_bulk` function produces an estimated Bulk Effective Sample Size (bulk-ESS) using rank normalized draws. Bulk-ESS is useful measure for sampling efficiency in the bulk of the distribution (related e.g. to efficiency of mean and median estimates), and is well defined even if the chains do not have finite mean or variance.

Both bulk-ESS and tail-ESS should be at least 100 (approximately) per Markov Chain in order to be reliable and indicate that estimates of respective posterior quantiles are reliable.



### Tail ESS
The `ess_tail` function produces an estimated Tail Effective Sample Size (tail-ESS) by computing the minimum of effective sample sizes for 5% and 95% quantiles. Tail-ESS is useful measure for sampling efficiency in the tails of the distribution (related e.g. to efficiency of variance and tail quantile estimates).
Both bulk-ESS and tail-ESS should be at least 100
(approximately) per Markov Chain in order to be reliable and indicate that estimates of respective posterior quantiles are reliable.





### Effective sample size
https://mc-stan.org/docs/reference-manual/effective-sample-size.html
The second technical difficulty posed by MCMC methods is that the samples will typically be autocorrelated (or anticorrelated) within a chain. This increases the uncertainty of the estimation of posterior quantities of interest, such as means, variances, or quantiles; see [Charles J. Geyer](https://mc-stan.org/docs/reference-manual/effective-sample-size.html#ref-Geyer:2011) ([2011](https://mc-stan.org/docs/reference-manual/effective-sample-size.html#ref-Geyer:2011)).

Stan estimates an effective sample size for each parameter, which plays the role in the Markov chain Monte Carlo central limit theorem (MCMC CLT) as the number of independent draws plays in the standard central limit theorem (CLT).




https://stats.stackexchange.com/questions/418142/low-effective-sample-size-but-good-r-hat-is-this-a-problem
Regarding your request for more information about effective sample size, close after the portion I cited above in the same book, they discuss R-hat connection with effective sample size neff as well as recommended settings for both. In particular, they mention that it might suffice to have as few as 10 or 100 as an effective sample size, and only aiming for more if an increased amount of precision is desired. Here's a quote:

> As a default rule, we suggest running the simulation until n^eff is at least 5m... Having an effective sample size of 10 per sequence should typically correspond to stability of all the simulated sequences. For some purposes, more precision will be desired, and then a higher effective sample size threshold can be used. Once  R-hat is near 1 and ˆn eff is more than 10 per chain for all scalar estimands of interest, just collect the mn simulations (with warm-up iterations already excluded, as noted before)  and treat them as a sample from the target distribution

Here, m is the "number of chains (after splitting)" [BDA3 pg. 284](http://www.stat.columbia.edu/%7Egelman/book/BDA3.pdf) you're simulating . Notice that in particular that the desired number they suggest does not depend on the number of draws, retained or otherwise. The reason why these two metrics are "typically" related is because their formulas make use of the same quantities.

However, they are getting at the dispersion of two different quantities. R^ measures the potential reduction in scale for the posterior distribution, while effective sample size gives you the reduction in the variance of the estimate for an expected value of this distribution. In the ideal case, we wouldn't have to resort to sampling, and we could just derive, say, the posterior expected value; here, we would have zero error on the latter, but a possibly very large number for the former. For more information take a look at page 286 and 287.