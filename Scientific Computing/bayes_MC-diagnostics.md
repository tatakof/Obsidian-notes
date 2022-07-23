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

Regarding your request for more information about effective sample size, close after the portion I cited above in the same book, they discuss R-hat connection with effective sample size neff as well as recommended settings for both. In particular, they mention that it might suffice to have as few as 10 or 100

as an effective sample size, and only aiming for more if an increased amount of precision is desired. Here's a quote:

> As a default rule, we suggest running the simulation until n^eff

is at least 5m... Having an effective sample size of 10 per sequence should typically correspond to stability of all the simulated sequences