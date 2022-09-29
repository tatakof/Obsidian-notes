### Notes

------------------------------------------------------------------------

# Why make bayesian stacking
explain that thing of its just an approximation after all de betancourt

# Bayesian stacking
from: <https://statmodeling.stat.columbia.edu/2021/08/11/bayesian-hierarchical-stacking-some-models-are-somewhere-useful/>

What I really want you to do is read section 3.1, All models are wrong, but some are somewhere useful, where Yuling describes how and why a mixture of wrong models can give better predictive performance than a correct model, even if such a correct model is included in the set of candidates.

**The background of this paper is that for a long time it's been clear that when doing predictive model averaging, it can make sense to have the weights vary by x (see for example figure 12 of [this paper](http://www.stat.columbia.edu/~gelman/research/published/loo_stan.pdf))---as Yuling notes, different models can be good at explaining different regions in the input-response space, which is why model averaging can work better than model selection---but it's tricky because if you let the weights vary without regularization, you'll just overfit.**

------------------------------------------------------------------------

from yao et al 2018 paper

[@yao2018]

A general challenge in statistics is prediction in the presence of multiple candidate mod-els or learning algorithms M = (M1 , . . . , MK ). Choosing one model that can give opti-mal performance for future data can be unstable and wasteful of information (see, e.g., Piironen and Vehtari, 2017). An alternative is model averaging, which tries to find an optimal model combination in the space spanned by all individual models. In Bayesian context, the natural target for prediction is to find a predictive distribution that is close to the true data generating distribution (Gneiting and Raftery, 2007; Vehtari and Ojanen, 2012).

In Bayesian model comparison, the relationship between the true data generator and the model list M = (M1 , . . . , MK ) can be classified into three categories: M-closed, M-complete and M-open.

• M-closed means the true data generating model is one of Mk ∈ M, although it is unknown to researchers.

• M-complete refers to the situation where the true model exists and is out of model list M. But we still wish to use the models in M because of tractability of computations or communication of results, compared with the actual belief model. Thus, one simply finds the member in M that maximizes the expected utility (with respect to the true model).

• M-open refers to the situation in which we know the true model Mt is not in M, but we cannot specify the explicit form p(ỹ\|y) because it is too difficult conceptually or computationally, we lack time to do so, or do not have the expertise, etc.

...

Wong and Clarke (2004) emphasize that the BMA weights reflect the fit to the data rather than evaluation the prediction accuracy.

...

**Stacking**.

*Stacking* (citations) is a direct approach for averaging point estimates from multiple models. In supervised learning, where the data are $((x_i, y_i), i = 1,\ ...,\ n)$ and each model $M_k$ has a parametric form $\hat{y}_k =\ f_k(x |\theta_k)$, stacking is done in two steps (citation). First, each model is fitted separately and the leave-one-out (LOO) predictor $\hat{f}_k^{(-i)}(x_i) = E[y_i |\ \hat{\theta}_{k, y-i},\ M_k]$ is obtained for each model $k$ and each data point $i$ is obtained for each model $k$ and each data point $i$. In the second step, a weight for each model is obtained by minimizing the LOO mean squared error

\$\$ \hat{w} = \arg\max*{w}\* \sum{i = 1}\^{n}

```{=tex}
\begin{pmatrix} y_i \sum_{k} w_k \hat{f}_k^{(-i)}(x_i) \end{pmatrix}
```
\^2

\$\$

The point prediction for a new data point with feature vector $\tilde{x}$ is

$$
\hat{\tilde{y}} = \sum_{k = 1}^K\ \hat{w_k}\  f_k(\tilde{x}\ | \hat{\theta}_{k, y_{1:n}})
$$

Stacking is not widely used in Bayesian model combination because the classical stacking only works with point estimates, not the entire posterior distribution (Hoeting et al., 1999).

description of some bayesian solutions to stacking and their problems...

Yao 2018 extends stacking from minimizing the squared eeror to maximizing scoring rules, hence make stacking applicable to combining a set of Bayesian posterior predictive distributions. They argue this is the appropriate version of Bayesian model averaging in the M-open situation.

------------------------------------------------------------------------

from ben lambert's vids and book

+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Prior vs Posterior Predictive distribution                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
+============================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+
| It's important to note that we have both a **prior** and a **posterior** predictive distribution.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| The **prior** predictive distribution is just the distribution of data which we think we are going to obtain before we actually see the data $y$, thus the $prior\ predictive\ distribution = p(y)$. This is based on our sort of prior knowledge about the situation. How can we calculate it? the idea is that we're trying to obtain is the probability of our data $y$. This is a marginal probability and we know that we can get to a marginal probability by integrating out all dependences, in this case $\theta$, of our joint probability $p(y, \theta)$ across all the range of values theta can take ($\theta \in \Theta$) . So by integrating this out we're removing all this theta dependence and we're just left with the marginal probability $p(y)$. So |
|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| $$                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| p(y) = \int_{\theta \in \Theta} p(y,\theta)d\theta                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| $$                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| and through the product rule of probability, which states that $p(A, B) = p(A|B)p(B)$, we get:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| $$                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| p(y) = \int_{\theta \in \Theta} p(y,\theta)d\theta = \int_{\theta \in \Theta} p(y|\theta)p(\theta)d\theta.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| $$                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| where $p(y|\theta)$ is the likelihood and $p(\theta)$ the prior.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| And with the posterior predictive distribution we essentially mean what value of data we would expect to obtain (that is, what our model would suggest after using the first observed data for fitting said model) if were to repeat the observation. We will call this new observation of data, $y'$. So how do we calculate this posterior predictive distribution? The idea is that we are trying to calculate the probability of certain value of the new data $y'$ given that we have observed the current data $y$ (the one used to fit the model), that is, $p(y'|y)$. We can get this conditional probability by integrating out the joint probability of $y'$ and $\theta$, acrross al range of theta ($\Theta$). Thus,                                           |
|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| $$                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| p(y'|y) = \int_{\theta \in \Theta} p(y',\theta |y)d\theta                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| $$                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| and through the chainrule of probability?, which states that $p(A, B |C) = p(A|B, C) p(B|C)$, we get:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| $$                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| p(y'|y) = \int_{\theta \in \Theta} p(y',\theta |y)d\theta = \int_{\theta \in \Theta} p(y'|\theta, y) p(\theta|y)d\theta                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| $$                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| and normally when you condition on $\theta$, our new observation $y'$ is independent of the current observation $y$ (that is, once you know $\theta$, $y$ doesn't provide any extra information about $y'$ ) and thus we can eliminate the dependency of $y'$ on $y$, so we get:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| $$                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| p(y'|y) = \int_{\theta \in \Theta} p(y'|\theta) p(\theta|y)d\theta                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| $$                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| where $p(y'|\theta)$ is the likelihood and $p(\theta|y)$ is the posterior distribution.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Given a posterior distribution $p(\theta | \pmb{y})$, we can produce a posterior predictive distribution, which for a single new data point equals $p(y^{new} | \pmb{y})$ (m' more detail on this on here NOTE), and this just tells us what is our sort of best prediction or distribution which ecompasses what we think about predictions for the next data point given that we have observed a data vector $\pmb{y}$. This distribution $p(y^{new} | \pmb{y})$ is an approximation to some unkown true data generating process which, we can call $f(y^{new})$. Ideally, if we knew what the distribution $f(y^{new})$ was, we could compare it with our posterior predictive distribution $p(y^{new} | \pmb{y})$. The best way we could compare this two distributions (if we knew both of them), is with what is called the Kullback-Leibler divergence ($D_{KL}$, also known as "relative entropy"), which is just a general measure of the difference between two distributions.

There are two sources of uncertainty in prediction: first, we do not know the true value of the parameters; and second, there is sampling variability <!--# i guess he means data sampling variability -->. The first of these sources of uncertainty is represented by the posterior. The second is represented by our choice of likelihood. To account for both these sources of variation, we typically derive an approximate distribution that represents our uncertainty over future data by iterating the following steps:

1.  sample a parameter from the **posterior** distribution

    $$
    \theta_i \sim p(\theta | data)
    $$

2.  plug that value of $\theta_i$ into our sampling distribution (likelihood) and then sample a datapoint.

$$
data^{'}_i \sim p(data | \theta_i) 
$$

<!--# this comes from the vid: Then if we draw a histogram of all the sampled $data^{'}_{i}$ , we get an approximation to our posterior predictive distribution. -->

By repeating these steps a large number of times (keeping each sampled data value), we eventually obtain a reasonable approximation to the posterior predictive distribution. This distribution represents our uncertainty over the outcome of a future data collection effort, accounting for our observed data and model choice. <!--# have to see if jags log_likelihood function actually does this -->

We build statistical models to explain the variation in a data sample because we believe that the insight this gives us applies to wider circumstances. One way to measure the wider applicability of a statistical model is to evaluate its predictive power on out-of-sample data. By fitting our model to one sample of data and then using it to predict data in another, we hope to produce an unbiased measure of a model's capacity to generalise. The problem is that we generally do not have access to out-of-sample data (If we did, we would usually include this as part of our sample!). One way out of this issue is to use the same sample twice: once to fit the statistical model and again to test its predictive power. The trouble with this approach is that we bias the odds in our favour and leave ourselves susceptible to overfitting.

If we try hard enough we can build a model that predicts a given data set perfectly, by adding layer upon layer of additional complexity. In producing a more complex model, we make more extreme assumptions about the data-generating process that may or, more likely, may not, be true. When we obtain a fresh data set, these assumptions are tested and often found wanting <!--# is "wanting" really the word? or is  -->, meaning that the model is terrible for prediction.

In machine learning (a statistical framework for developing the most predictive models), overfitting is avoided by splitting a data set into a training set and a cross-validation set. The models are fitted to the training set, which is then assessed by its performance on an independent cross- validation set.

<!--# why IC has been used more often than CV -->

While we would ideally carry out this sort of partitioning in statistical inference (in fact, one measure we discuss, LOO-CV, does exactly this), often the computational task of refitting a model on many data sets makes it prohibitive to do so. **Also, the nature of the data can make it difficult to decide on an appropriate data split**. Among other reasons, these two issues have led to a demand for other measures of model predictive capability, which can be calculated without the need for re-estimation on a cross-validation set.

These measures are, at best, approximations to the cross-validation ideal $$15$$. They aim to correct for the bias inherent in trying to assess a model's performance on the same data set which was used to fit the model in the first place.

<!--# notice that earlier Ben asseses the problem with complex models, mainly that they assume too many things about the data generating process (if each thing assumed has a probability of being true, then the more things we assume are happening, the less likely it is), and this tends to make the model fit the "noise" (random jitter not inherent to the true generating process or "signal") instead of only the signal (i.e., the model overfits) -->

If we obtain new data $\pmb{y^{new}} = \{y^{new}_1 , \ ..., \ y^{new}_n \}$ there are a few different ways we might measure the fit of a model. A popular way of summarising the discrepancy between the model's predictions $\pmb{y^{pred}} = \{y^{pred}_1 ,\ ..., \ y^{pred}_n \}$ and the real data $\pmb{y^{new}}$ is to measure the mean squared error (MSE) (maybe add the equation if you are not that lazy).

This measure is easy to calculate but does not have any theoretical justification (apart from when a normal likelihood is used), which limits its scope. A more theoretically justified Bayesian measure would be to use the posterior predictive distribution to measure a model's ability to predict new data. In particular, we could choose a model with the highest posterior probability of generating the new data, $p(\pmb{y^{new} \ | \ y ) }$.

Since the log function is a monotonic transformation, the score obtained by using the logarithm of the posterior predictive distribution will mirror the posterior predictive distribution. We favour using the log form because of its connection with a concept called the Kullback--Leibler (KL) divergence, which is a measure of the difference between the true density and the estimated one. If we maximise the log of the posterior predictive distribution, this is equivalent to estimating the posterior predictive density with the lowest KL divergence from the true density.

The scoring function hence used is:

$$
prediction \ accuracy = log[p(\pmb{y^{new} | \ y})]
$$

which can also be written as:

$$
prediction \ accuracy = log \ \int p(\pmb{y^{new}} | \theta) \ p(\theta | \pmb{y}) d\theta  \ \ (10.4) 
$$

$$
prediction\ accuracy = log[E_{posterior}(p(\pmb{y^{new}}\  |\ \theta  ))] 
$$

where $E_{posterior}$ denotes the expectation with respect to the posterior distribution.

10.5.3 The ideal measure of a model's predictive accuracy.

Imagine that we start by considering a single new data point, $y^{new}$. Usually, we do not have access to this extra data, and so the new data $y^{new}$ is unknown. If we knew the true distribution $f(y)$ for a single new data point, we could evaluate the expectation of the expression (10.4), which gelman et al $$14$$ call the expected log predictive density (elpd):

$$
elpd = E_f(log[p(y^{new} | \pmb{y})])
$$

$$
elpd = \int_{y^{new}\ \epsilon\ Y} f(y^{new})log[p(y^{new} | \pmb{y})]dy^{new} \ \ (10.6)
$$

where $E_f$ denotes the expectation under the true data distribution $f(y)$. This measure quantifies how close the estimated posterior predictive distribution, $p(y^{new} | \pmb{y})$, is to the true distribution, $f(y)$. Accordingly, expression (10.6) is maximised when the estimated distribution equals the true one (because in that case the $D_{KL} = 0$ and thus both distributions are the same).

If we choose a model to maximise $elpd$, we also minimise the KL divergence between our posterior predictive distribution and the true data distribution.

If we then consider the $elpd$ for our $n$ new data points, taken one at a time, we have what Gelman et al. $$14$$ call the "expected log **pointwise** predictive density" (elppd):

$$
elppd = \sum_{i = 1}^{n}E_f( log[ p(y^{new} | \pmb{y} ])     (10.10)
$$

The pointwise measure defined in (10.10) is preferable to using the full joint predictive distribution $E_f(\ log\ [p(\pmb{y^{new}}\ |\ \pmb{y})]\ )$ because it enables a range of expressions representing out of sample error to be calculated from it $$14$$

<!--# shouldnt there be an average? or is just the straight sum? -->

... So, in general, we can think about the KL divergence as measuring some sort of informational penalty in going from something optimised to distribution p to code for another distribution q.

10.5.8 LOO-CV

As we discussed previously, the ideal measure of a model's predictive accuracy would be to split a data set into a training set and a cross-validation set. The model is then fitted on the training set, and its predictive performance gauged on the independent cross-validation set. The use of this independent cross-validation set **circumvents the issue of selection bias**, and allows us to be more confident in our estimates of the model's out-of-sample predictive capability.

While the use of training and cross-validation sets provides a better measure of predictive accuracy in principle, there are practical concerns which limits its use. Here, we consider a method known as leave-one-out cross-validation (LOO-CV), where we use a single data point to test the model's predictive power, $y_{cv}$, and use the rest of the sample, $\pmb{y_{train}}$, to train the model. Ideally, this process is iterated $n$ times (where $n$ is the size of the data sample) so that each data point in the sample is used only once as the single cross-validation test datum in one of the iterations. This can be extremely expensive computationally speaking, particularly if the data set is large. Also, if the data are structured, as in te case of time series, it may be difficult to estimate the model with gaps in the data series (with the "gap" being the left out datum for testing).

In each iteration of LOO-CV we evaluate the log posterior predictive density (across all samples from our posterior distribution):

$$
lpd = log[p(y_i|\pmb{y_{-i}})]
$$

where $\pmb{y_{i-1}}$ denotes the training data vector with all data points included apart from $y_i$ (the bold letter indicates that it's a vector instead of a scalar). If this process is iterated $n$ times, we can estimate the overall expected log pointwise predictive density by summing the invidiual $lpd$ values. Thus:

$$
\widehat{elppd} = \sum_{i = 1}^{n}\ log[p(y_i|\pmb{y_{-i}})]
$$

Estimates of $elppd$ by this method may underestimate the predictive accuracy of the full model because the training sample consists of only $n - 1$ data points rather than the full sample $$14$$. So a corrective term can be added for completeness; however, in paractice this term is small (particularly for large data sets), so it can usually be ignored. <!--# CHECK GELMANS PAPER BECAUSE WE MAY HAVE TO ADD THE CORRECTION TERM BECAUSE WE DONT HAVE THAT MANY DATA -->

In using LOO-CV to choose between models, we also run the risk of overfitting. This is because, if we use LOO-CV to select a model, we will likely pick one that fits both the signal and noise in the cross-validation set. <!--# this is not really an explanation --> This is well documented in the machine-learning literature and merits the use of a third data set called the $test$ set, which is used only once to evaluate a model.

PPCs (Posterior Predictive Check) assess the fit of your model to the data at hand, whereas WAIC and LOO-CV assess the fit of your model to out-of-sample data. The trouble with blindly using PPCs to construct a model is that this can result in an overly complex model, which is overfit to the sample of data on which it was estimated. We guard against this overfitting by using WAIC and LOO-CV.

------------------------------------------------------------------------

[**FROM "Understanding predictive information criteria for Bayesian models" GELMAN ET AL 2013.**]{.ul}

[@gelman2013]

2\. Log predictive density as a measure of model accuracy

**One way to evaluate a model is through the accuracy of its predictions. Sometimes we care about this accuracy for its own sake, as when evaluating a forecast. In other settings, predictive accuracy is valued not for its own sake but rather for comparing different models.** We begin by considering different ways of defining the accuracy or error of a model's predictions, then discuss methods for estimating predictive accuracy or error from data.

Consider data $y_1,\ …,\ y_n$, modeled as independent given parameters $\theta$, thus $p(y|\theta) = \prod_{i = 0}^{n}\ p(y_i | \theta)$. With regression, one would work with $p(y|\theta, x) = \prod_{i = 0}^{n}\ p(y_i | \theta,\ x_i)$. In our notation, we suppress any dependence on $x$.

Preferably, the measure of predictive accuracy is specifically tailored for the application at hand, and it measures as correctly as possible the benefit (or cost) of predicting future data with the model. Often explicit benefit or cost information is not available and the predictive performance of a model is assessed by generic scoring functions and rules.

**Measures of predictive accuracy for probabilistic prediction are called scoring rules** <!--# maybe just say whats behind the comment and add that there are other scoring rules besided the logarithmic one -->. Examples include the quadratic, logarithmic, and zero-one scores, whose properties are reviewed by Gneiting and Raftery (2007). Bernardo and Smith (1994) argue that suitable scoring rules for prediction are proper and local: propriety of the scoring rule motivates the decision maker to report his or her beliefs honestly, and for local scoring rules predictions are judged only on the plausibility they assign to the event that was actually observed, not on predictions of other events. The logarithmic score is the unique (up to an affine transformation) <!--# In Euclidean geometry, an affine transformation, or an affinity, is a geometric transformation that preserves lines and parallelism (but not necessarily distances and angles) --> local and proper scoring rule (Bernardo, 1979), and appears to be the most commonly used scoring rule in model selection.

**Mean squared error**. A model's fit to new data can be summarized numerically by mean squared error, $\frac{1}{n}\ \sum_{i = 1}^{n}(y_i - E(y_i |\theta))^2$ , or a weighted version such as $\frac{1}{n}\ \sum_{i = 1}^{n}(y_i - E(y_i |\theta))^2 /var(y_i | \theta)$. These measures have the advantage of being easy to compute and, more importantly, to interpret, but the disadvantage of being less appropriate for models that are far from the normal distribution.

**Log predictive density or log-likelihood**. Log predictive density or log-likelihood. A more general summary of predictive fit is the log predictive density, $log\ p(y|\theta)$ <!--# this is different from the log predictive density of ben lambert's book log p(ynew | \pmb{y}) -->, which is proportional to the mean squared error if the model is normal with constant variance. [**The log predictive density is also sometimes called the log-likelihood**]{.ul} <!--# SUPERRRR IMPORTNAT, THIS WHY I DIDNT REALLY GET THE CODE -->. **The log predictive density has an important role in statistical model comparison because of its connection to the Kullback-Leibler information measure** (see Burnham and Anderson, 2002, and Robert, 1996). **In the limit of large sample sizes, the model with the lowest Kullback-Leibler information---and thus, the highest expected log predictive density---will have the highest posterior probability. Thus, it seems reasonable to use expected log predictive density as a measure of overall model fit**.

We are not saying that the prior cannot be used in assessing a model's fit to data <!--# with "prior" does he mean the "the new posterior" and thus by "likelihood" he means the posterior predictive density? which would be some sort of "posterior" likelihood, the likelihood after fitting the model, that is, the likelihood with the posterior parameters instead of the prior parameters. -->; **rather we say that the prior density is not relevant in computing predictive accuracy**. **Predictive accuracy is not the only concern when evaluating a model, and even within the bailiwick** <!--# Bailiwick nowadays means "one's area of skill, knowledge, authority, or work" --> **of predictive accuracy, the prior is relevant in that it affects inferences about** $\theta$ and thus af**fects any calculations involving** $p(y|\theta)$. In a sparse-data setting, a poor choice of prior distribution can lead to weak inferences and poor predictions.

2.3. Predictive accuracy for a single data point.

**The ideal measure of a model's fit would be its out-of-sample predictive performance for new data produced from the true data-generating process**. We label $f$ as the true model, $y$ as the observed data (thus, a single realization of the dataset $y$ from the distribution $f(y)$, and $\tilde{y}$ as future data or alternative datasets that could have been seen. The out-of-sample predictive **fit** for a **new** data point $\tilde{y_i}$ **using logarithmic score** <!--# NOTE THAT WE ARE USING LOGARITHMIC SCORE, SO NOW U CAN SAY SOMETHING LIKE "THERE ARE OTHER'S SCORING RULES BESIDES THE LOGARITHMIC SCORE" --> is then,

$$
log\ p_{post}(\tilde{y_i}) = log\ E_{post} (p(\tilde{y_i} | \theta) = log\ \int p(\tilde{y_i} | \theta)\ p_{post}(\theta)d \theta
$$

In the above expression, $p_{post}(\tilde{y_i})$ is the predictive density <!--# or posterior predictive density, which i think is the probability of generating ytilde with the given model, or in other way, how likely is this ytilde for the given model  --> for $\tilde{y_i}$ induced by the posterior distribution $p_{post}(\theta)$. We have introduced the notation $p_{post}$ here to represent the posterior distribution because our expressions will soon become more complicated and it will be convenient to avoid explicitly showing the conditioning. <!--# E_{post} denotes the expectation under the posterior distribution, that is the \int p_{post}\theta d\theta part. -->

We must then take on further step. The future data $\tilde{y_i}$ are themselves unknown and thus we define the **expected** out-of-sample log predictive density,

$$
elpd = expected\ log\ predictive\ density\ for\ a\ new\ \pmb{single}\ data\ \pmb{point}
$$

$$
elpd = E_f(log\ p_{post}(\tilde{y_i})) = \int (log\ p_{post}(\tilde{y_i}))\ f(\tilde{y_i})d \tilde{y}\ \ \ \ (1)
$$

($E_f$ denotes the expectation under the true data distribution $f(y)$).

In the machine learning literature this is often called the mean log predictive density. In any application, we would have some $p_{post}$ but we do not in general know the data distribution $f$. A natural way to estimate the expected out-of-sample log predictive density would be to plung in an estimate for $f$, but this will tend to imply too good a fit, as we discuss in Section 3. For now we consider the estimation of predictive accuracy in a Bayesian context.

To keep comparability with the given dataset <!--# EXPLAINED IN THE PARAGRAPH BELOW -->, one can define a measure of predictive accuracy for the $n$ data points taken one at a time:

$$
elppd = expected\ log\ \pmb{pointwise}\ predictive\ density\ for\ a\ new\ data\pmb{set}
$$

$$
elppd = \sum_{i = 1}^{n}E_f(log\ p_{post}(\tilde{y_i}))\ \ \ \   (2)
$$

**which must be defined based on some agreed-upon division of the data** $y$ **into individual data points** $y_i$ <!--# THIS SEEMS TO BE SUPER IMPORTANT FOR HIERARCHICAL MODELS -->. The advantage of using a pointwise measure, rather than working with the joint posterior predictive distribution, $p_{post}(\tilde{y})$ is in the connection of the pointwise calculation to cross-validation, which allows some fairly general approaches to approximation of out-of-sample fit using available data.

2.4 Evaluating predictive accuracy for a fitted model

In practice the parameter $\theta$ is not known, so we cannot know the log predictive density $log\ p(y|\theta)$ <!--# i guess this is the probability density function of y given an exact value of theta, that is, how likely is each possible value of y if theta takes a certain form but there's no uncertainty on the form or value theta takes -->. For the reasons discussed above we would like to work with the posterior distribution, $p_{post}(\theta) = p(\theta | y)$, and summarize the predictive accuracy of the fitted model **to data** <!--# THIS IS OF OBSERVED DATA, NOT NEW DATA --> by,

$$
lppd = log\ pointwise\ predictive\ density
$$

$$
lppd = log \prod_{i=1}^{n} p_{post}(y_i) = \sum_{i = 1}^{n}log \int p(y_i|\theta)\ p_{post}(\theta)d \theta \ \ \ \ (4)
$$

(remember that logs turn products into sums)

To compute this predictive density in practice <!--# this seems to be what ben lambert explains above about how to compute the predictive density. Do a comparation between both of them later -->, we can evaluate the expectation using draws from $p_{post}(\theta)$, the usual posterior simulations, which we label $\theta^s$, $s = 1,\ …,\ S$:

$$
\pmb{computed}\ lppd = \pmb{computed}\ log\ pointwise\ predictive\ density
$$

$$
= \sum_{i=1}^{n} log\ (\frac{1}{S} \sum_{s= 1}^{S} p(y_i | \theta^s)\ ) \ \ \ (5)
$$

(when we compute the lppd, we "replace" the $\int p_{post}(\theta)d\theta$ with $\frac{1}{S}\sum_{s=1}^{S}$, and we do it *pointwise* with the $\sum_{i=1}^n$ part)

(remember that this is estimating out of sample predictive accuracy using in sample data and thus is an overestimation of $(2)$. That is, lppd is a biased estimate of elppd)

We typically assume that the number of simulation draws $S$ is large enough to fully capture the posterior distribution; thus we shall refer to the theoretical value $(4)$ and the computation $(5)$ interchangeably as the "log pointwise predictive density" or lppd of the data.

As we shall discuss in Section 3, the lppd of **observed** data $y$ is an overestimate of the elppd for future data $(2)$ <!--# SUPPA IMPORTANT -->. Hence the plan is like to start with $(5)$ and then apply some sort of bias correction to get a reasonable estimate of $(2)$. <!--# is this done automatically by the loo package? do we have to do it by hand when computing the exact LFO? see what buerkner does. -->

2.5. Choices in defining the likelihood and predictive quantities

As is well known in hierarchical modeling, the line separating prior distribution from likelihood is somewhat arbitrary <!--# WHY --> and is related to the question of what aspects of the data will be changed in hypothetical replications. In a hierarchical model with direct paramenters $\alpha_1,\ ...,\ \alpha_J$ and hyperparameters $\phi$, factored as $p(\alpha,\phi|y)\ \propto\  p(\phi) \prod_{j = 1}^{J} p(\alpha_j | \phi)\ p(y_j | \alpha_j)$ <!--# p(\alpha_j | \phi)p(\phi) seems to be the prior, whereas p(y_j | \alpha_j) seems to be the likelihood --> we can imagine replicating new data in **existing** groups (with the 'likelihood' being proportional to $p(y |\alpha_j)$) or new data in **new** groups (a new $\alpha_{J+1}$ is drawn, and the 'likelihood' is proportional to $p(y | \phi) = \int p(y|\alpha_{J+1})\ p(\alpha_{J+1} | \phi) d\alpha_{J+1}$ <!--# i wrote the equation the other way around because I prefer it like that -->. In either case, we can easily compute the posterior predictive density of the **observed** data $y$:

-   When prediction $\tilde{y} |\alpha_j$ (that is, new data from **existing** groups), we can compute $p(y|\alpha_{j}^s)$ for each posterior simulation $\alpha_{j}^s$ and then take the average, as in $(5)$.

-   When predicting $\tilde{y} |\alpha_{J+1}^s$ (that is, new data from a new group), we sample $\alpha_{J+1}^s$ from $p(\alpha_{J+1} |\phi^s)$ to compute $p(y|\alpha_{J+1}^s)$.

We are not bothered by the nonuniqueness of the predictive distribution. Just as with posterior predictive checks, different distributions correspond to different potential uses of a posterior inference. <!--# SUPPA IMPORTANT FOR OUR CUSTOM LFO, WHICH I BELIEVE WE WOULD LIKE TO KNOW HOW WELL WE WOULD PREDICT ON A NEW LOCATION GIVEN THE DATA THAT WE CURRENTLY HAVE. MAYBE WE SHOULD HAVE THAT CORRECTIVE TERM GIVEN THE FEW ACTUAL DATA POINTS THAT WE HAVE (DOES A HIERARCHICAL MODEL REDUCE THE "EFFECTIVE" NUMBER OF DATAPOINTS?  -->. Given some particular data, a model might predict new data accurately in some scenarios but not in others <!--# WE HAVE TO DEFINE OUR SCENARIO, do we have one scenario or two? we clearly have the scenario of predicting data from a new location, so thats one. But for now, the scenario of predicting data from inside a location doesnt seem to matter that much. --> .

Vehtari and Ojanen (2012) discuss different prediction scenarios where the future explanatory variable $\tilde{x}$ is assumed to be random, unknown , fixed, shifted, deterministic, or constrained in some way. Here we consider only scenarios with no $x$, $p(\tilde{x})$ is equal to $p(x)$, or $\tilde{x}$ is equal to $x$...

3\. Information criteria and effective number of parameters

...

We are interested in prediction accuracy for two reasons: first, to measure the performance of a model that we are using; second, to compare models. Our goal in model comparison is not necessarily to pick the model with lowest estimated prediction error or even to average over condidate models - ... - but at least to put different models on a common scale. **Even models with completely different parameterizations can be used to predict the same measurements**.

**When different models have the same number of parameters estimated in the same way, one might simply compare their best-fit log predictive densities directly, but when comparing models of differing size or differing effective size** (for example, comparing logistic regressions fit using uniform, spline, or Gaussian process priors), **it is important to make some adjustment for the natural ability of a larger model to fit data better, even if only by chance** <!--# important for comparing our different models -->.

3.1. Estimating out-of-sample predictive accuracy using available data

**Several methods are available to estimate the expected predictive accuracy without waiting for out-of-sample data. We cannot compute formulas suchs as** $(1)$ **directly because we do not know the true distribution,** $f$**. Instead we can consider various approximations. We know of no approximation that works in general, but predictive accuracy is important enough that it is still worth trying... Each of these methods has flaws, which tells us that any predictive accuracy measure that we compute will be only approximate.**

-   *Within-sample predictive accuracy*. A naive estimate of the expecte log predictive density for *new* data is the log predictive density for *existing* data. As discussed above, we would like to work with the bayesian pointwise formula, that is, lppd as computed using the simulation $(5)$. This summary is quick and easy to understand but is in general an overestimate of $(2)$ because it is evaluated on the data from which the model was fit.

-   *Adjusted within-sample predictive accuracy*. Given that lppd is a biased estimate of elppd, the nest logical step is to correct that bias. Formulas such as AIC, DIC, and WAIC give approximately unbiased estimates of elppd by starting with something like lppd and then subtracting a correction for the number of parameters, or the effective number of parameters, being fit. These adjustments can give reasonable answers in many cases but have the general problem of being correct at best only in expectation, not necessarily in any given case.

-   *Cross-validation.* One can attempt to capture out-of-sample prediction error by fitting the model to training data and then evaluating this predictive accuracy on a holdout set. **Cross-validation avoids the problem of overfitting but remains tied to the data at hand and thus can be correct at best only in expectation**. In addition, cross-validation can be computationally expensive: to get a stable estimate typically requires many data partitions and fits. At the extreme, leave-one-out cross-validation (LOO-CV) requires $n$ fits except when some computation shortcut can be used to approximate the computations.

3.8. Leave-one-out cross-validation

In Bayesian cross-validation, the data are repeatedly partitioned into a training set $y_{train}$ and a holdout set $y_{holdout}$, and then the model is fit to $y_{train}$ (thus yielding a posterior distribution $p_{train}(\theta) = p(\theta | y_{train})$), with this fit evaluated using an estimate of the log predictive density of the holdout data, $log\ p_{train}(y_{holdout}) = log \int p_{pred}(y_{holdout}|\theta)p_{train}(\theta)d\theta$. Assuming the posterior distribution $p(\theta|y_{train})$ is summarized by $S$ simulation draws $\theta^s$, we calculate the log predictive density as $log\ (\ \frac{1}{S} \sum_{s=1}^S p(y_{holdout} | \theta^s)\ )$.

((i guess that $p_{train}(y_{holdout})$ is the predictive density for $y_{holdout}$ induced by the posterior distribution given by the data used to train, and thus the $p_{train}()$ part; this is a "parallel" that is made from the following thing written above "$p_{post}(\tilde{y_i})$ is the predictive density for $\tilde{y_i}$ induced by the posterior distribution $p_{post}(\theta)$."))

For simplicity, we will restrict our attention here to leave-one-out cross-validation (LOO-CV), the special case with $n$ partitions in which each holdout set represents a single data point. Performing the analysis for each of the $n$ data points (or perhaps a random subset for efficient computation if $n$ is large) yields $n$ different inferences $p_{post(-1)}$, each summarized by $S$ posterior simulations, $\theta^{is}$.

The Bayesian LOO-CV estimate of out-of-sample predictive fit is

$$
lppd_{loo-cv} = \sum_{i = 1}^{n} log\ p_{post(i-1)}(y_i),\ calculated\ as\ \sum_{i=1}^{n}log\ (\frac{1}{S} \sum_{s=1}^{S} p(y_i|\theta^{is})\ )\ \ \ \ (14) 
$$

Each prediction is conditiones on $n-1$ data points, which causes underestimation of the predictive fit. For large $n$ the difference is negligible, but for small $n$ (or when using k-fold cross-validation) we can use a first order bias correction $b$ by estimating how much better predictions would be obtained if conditioning on $n$ data points:

$$
b = lppd - \overline{lppd}_{-i}
$$

where

$$
\overline{lppd}_{-1} = \frac{1}{n} \sum_{i=1}^{n}\sum_{j=1}^{n} log\ p_{post(-i)}(y_j),\ calculated\ as\ \frac{1}{n} \sum_{i=1}^{n} \sum_{j=1}^{n} log\ (\ \frac{1}{S} \sum_{s=1}^{S} p(y_j | \theta^{is})\ )
$$

(don't really know what the $j$ subindex stands for here)

The bias-corrected Bayesian LOO-CV is then

$$
lppd_{cloo-cv} = lppd_{loo-cv} + b
$$

The bias correction $b$ is rarely used as it is usually small, but we include it for completeness.

To make comparisons to other methods, we compute an estimate of the effective number of parameters as

$$
p_{loo-cv} = lppd - lppd_{loo-cv}\ \ \ (15)
$$

or, using bias-corrected LOO-CV,

$$
p_{cloo-cv} = lppd - lppd_{cloo}
$$

$$ 
= \overline{lppd}_{-i} - lppd_{loo}
$$

<!--# check if the loo package makes this bias-correction -->

Cross-validation is like WAIC in that it requires data to be divided into disjoint, ideally conditionally independent, pieces. This represents a limitation of the approach when applied to structured models. In adittion, cross-validation can be computationally expensive except in settings where shortcuts are available to approximate the distributions $p_{post(-i)}$ without having to re-fit the model each time.

Bayesian cross-validation works also with singular models <!--# according to https://arxiv.org/abs/1309.0911 "In this paper, we are concerned with Bayesian information criteria in the context of singular model selection problems, that is, problems that involve models with Fisher-information
matrices that may fail to be invertible".  -->, and Bayesian LOO-CV has been proven to asymptotically equal to WAIC. For finite $n$ there is a difference, as LOO-CV conditions the posterior predictive densities on $n - 1$ data points. These differences can be apparent for small $n$ or in hierarchical models. <!--# i dunno if this is that important because is just about the difference between WAIC and LOO, but we aint doing WAIC, just LFO. -->

Other differences arise in regression or hierarchical models. LOO-CV assumes the prediction task $p(\tilde{y_i} | \tilde{x_i}, y_{-i}, x_{-i})$ while WAIC estimates ... <!--# included this part only for the equation, the rest is a comparison with WAIC that doesn't seem relevant. -->

The cross-validation estimates are similar to the jackknife (Efron and Tibshirani, 1993). Even though we are working with the posterior distribution, our goal is to estimate an expectation averaging over $y^{rep}$ <!--# not explained what yrep is -->in its true, unknown distribution, $f$; thus, we are studying the frequency properties of a Bayesian procedure.

...

In expectation. As can be seen above, AIC, DIC, WAIC, and $lppd_{loo-cv}$ all are random variables, in that their values depend on the data $y$, even if the model is known... <!--# maybe should re-check the example. -->

...

<!--# few equations evaluating the example -->

...

Despite what the notation might seem to imply, elppd is *not* the same as E(lppd); the former is the expected log pointwise predictive density for future data $\tilde{y}$, while the latter is this density evaluated at the observed data $y$ <!--# need to check -->.

The correct 'effective number of parameters' (or bias correction) is the difference between $E(lppd)$ and $elppd$. <!--# more equations below. Might have to check. -->

------------------------------------------------------------------------

```{r setup}

knitr::opts_knit$set(root.dir = here::here())

```

We will use bayesian stacking to average bayesian predictive distributions.

To acomplish this we will first grab the loo_model\_\*\_2017 targets which contain the computed loo's. We will use the loo scores for the following models: M1_b0, M2 and M3.

```{r }

library(tidyverse)


loo_M1 <- targets::tar_read(loo_model_M1_2017)
loo_M1_b0 <- targets::tar_read(loo_model_M1_b0_2017)
loo_M2 <- targets::tar_read(loo_model_M2_2017)
loo_M3 <- targets::tar_read(loo_model_M3_2017)



data_list <- list(
    "M1_b0" = loo_M1_b0, 
    "M2" = loo_M2,
    "M3" = loo_M3
)


lpd_point <- data_list %>% 
  ## extract pointwise loglik values for each model
  map(~ pluck(.x, 'pointwise')[, 'elpd_loo']) %>% 
  ## reshape for loo:: functions
  as_tibble %>% as.matrix



## Merge model averaging results and round
results <- cbind(
  # Bayesian stacking weights. 
  'stacking_wts' = loo::stacking_weights(lpd_point),
  # Pseudo-BMA weights without Bayesian bootstrap
  'pbma_wts' = loo::pseudobma_weights(lpd_point, BB = FALSE),
  # Pseudo-BMA+ weights (with bootstrap)
  'pbma_BB_wts' = loo::pseudobma_weights(lpd_point)
) %>% 
  round(digits = 3)



## add rownames
names <- colnames(lpd_point)
rownames(results) <- names

## rownames to column
results <- results %>% 
  as.data.frame() %>% 
  rownames_to_column(var = 'models') %>% 
  as_tibble()


## return
results



############ OLD WAY OF DOING IT ################

# loo_M1 <- targets::tar_read(loo_model_M1_2017)
# loo_M1_b0 <- targets::tar_read(loo_model_M1_b0_2017)
# loo_M2 <- targets::tar_read(loo_model_M2_2017)
# loo_M3 <- targets::tar_read(loo_model_M3_2017)
# 
# lpd_point <- list(
#   '1' = cbind(
#     "M2" = loo_M2$pointwise[, "elpd_loo"],
#     "M3" = loo_M3$pointwise[, "elpd_loo"]
#   ),
#   
#   '2' = cbind(
#     "M1_b0" = loo_M1_b0$pointwise[, "elpd_loo"], 
#     "M2" = loo_M2$pointwise[, "elpd_loo"],
#     "M3" = loo_M3$pointwise[, "elpd_loo"]
#   ),
#   
#   '3' = cbind(
#     "M1" = loo_M1$pointwise[, "elpd_loo"],
#     "M1_b0" = loo_M1_b0$pointwise[, "elpd_loo"], 
#     "M2" = loo_M2$pointwise[, "elpd_loo"],
#     "M3" = loo_M3$pointwise[, "elpd_loo"]
#   )
# )
# 
# 
# # Bayesian stacking weights. 
# stacking_wts <- map(lpd_point, ~ loo::stacking_weights(.x))
# 
# # Pseudo-BMA weights without Bayesian bootstrap
# pbma_wts <- map(lpd_point, ~ loo::pseudobma_weights(.x, BB = FALSE))
# 
# # Pseudo-BMA+ weights (with bootstrap)
# pbma_BB_wts <- map(lpd_point, ~ loo::pseudobma_weights(.x))
# 
# # Merge all results into a list, round numerical values and add row names. 
# 
# results <- list(
#     'stacking_wts' = stacking_wts, 
#     'pbma_wts' = pbma_wts, 
#     'pbma_BB_wts' = pbma_BB_wts
#   ) %>% 
#   ## Merge results
#   pmap(cbind) %>% 
#   ## Round numerical values 
#   map(~ round(.x, digits = 3))
# 
# 
# 
# 
# 
# ## add rownames
# names <- map(lpd_point, colnames)
# rownames(results$`1`) <- names$`1`
# rownames(results$`2`) <- names$`2`
# rownames(results$`3`) <- names$`3`
# 
# 
# results





```
