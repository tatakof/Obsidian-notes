From Ecological Forecasting, Dietze 2017. 

Chapter 13. Data Assimiliation 1: Analytical methods


Synopsis: A frequent goal in forecasting is to update analysis in light of new information. Bayesian analysis are inherently updateable as the posterior from one analysis becomes the prior for the next. Classic sequential data assimilation methods are designed to exploit this property to make iterative forecasts. In the first of two data assimilation chapters we focus on such methods, such as the Kalman filter, that are computationally efficient and have analytical solutions, but require strong assumptions and or signiuficant modifications of the model code. 





If we just need to make this forecast once, the state-space framework (chapter 8) provides a general approach that could be used to estimate model parameters (chapter 5), partition uncertainties (chapter 6), assimilate one or more data sources (chapter 9), and projec tthe state of the system into the future (chapter 11). 
THIS SEEMS TO BE OUR ACTUAL STATE NOW WITH THE JAGS MODELS AND THE NAIVE WAY TO DO IT WITH STAN. 



A common porblem is the need to make forecast repeatedly, updating predictions and or hindcasts as new information becomes available. The brute force wat to do this is to redo the whole process from scratch, performing the analysis witha combined data set of the old observations and the newly acquired data. For simple models and small data sets this approach is straightforward, but as models and data grow in complexity and volumen, the obvious question is wheter ther's a way to update forecast iteratively. Indeed, for many problems (both forecasting and hindcasting) it may be computationally too expensive to assimilate the entirety of the data all at once, and thus the data need to be assimilated sequentially, a bit at a time, in the order that they were observed. 
 THIS SEEMS TO BE THE PROPER WAY TO DO IT. 

The problem we are describing is known as the sequential or operational data assimilation problem, with the latter referring to the fact that this is the way that almost all real-time forecast systems operate (e.g., weather forecast).


Sequential data assimilation occurs through two steps: the forecast step projects our estimated state forward in time, with uncertainty, the analysis step updates our estimate of that state based on new observations. The continual iteration between these two steps is known as the forecast cycle (figure 13.1)



13.2 Kalman Filter

**If we combine the forecast and analysis components of our simplest possible gaussian Linear model with known parameters (!!!!!), the overall forecast cycle has an analytical solution. This solution ins known as the Kalman filter.** 

One of the powerful features of the multivariate Kalman filter is that it allows us to make inferences about unobserved state variables based on the covariance between the observed and unobserved variables...

13.3 Extenden Kalman Filter
As noted earlier, the Kalman filter KF is a special case of the state-space model where the model is linear and both the process and observation errors are Normally distributed. The Extended Kalman Filter EKF allows the process model to be an arbitrary non-linear function. ... MORE TO READ IF WE ARE GOING TO IMPLEMENT IT. 

The KF and EKF have a number of advantages over the more general state-space framework, most important.... KEEP READING LATER

**Finally, the KF and EKF make the assumption that all the parameters are known, which is usually a much less tenable assumption in ecological forecasting problems that more physical applications.** .... This is an unsatisfying approach ... in the following chapter we will look at alternative numerical approaches to further relax the assumptions of KF and EKF.



Chapter 14: Data Assimilation 2: Monte Carlo Methods. 

Synopsis: In the previous chapter we introduced the concept of the forecast cycle and derived the classic Kalman filter KF and Extendend Kalman Filter EKF based on analytical approaches to uncertainty propagation (linear transformation and Taylor Series respectively). In this chapter we extend these approaches using the numerical methods for error propagation discussed in chapter 11, ensemble and Monte Carlo methods, to the data assimilation problem. This leads to the Ensemble Kalman filter and the Particle filter, respectively. We then discuss the generalization of these approaches to the ecological forecasting problem. Finally, we touch on the issue of forecasting with multiple models, discussing approaches such as Bayesian model averaging and reversible-jump MCMC. 

As noted in the previous chapter, the EKF was derived as a means to linearly approximate the forecast step of the forecast cycle when working with nonlinear models. ... In discussing uncertainty propagation we also presented two numerical methods: ensembles and Monte Carlo. In the ensemble-based approach the size of the sample is typically large enough to allow the accurate estimation of the mean and covariance, but not so large as to represent the full probability distribution. This same approach can be applied in the forecast cycle. Specifically, the joint posterior distribution from the analysis step is sampled, and the forecast step is performed by running the model forward independently for each ensemble member (figure 14.1). The result is an ensemble-based filter. The basic steps involved in an ensemble filter are thus...

... 

Compared to the EKF, this approach has the advantage of being relatively easy to implement, as it does not require the analytical Jacobian (matrix of first derivatives) or any changes to the underlying model structure or code. It is also easy to understand, and capable of dealing with a high degree of nonlinearity. Since it is using an ensemble-based method, we do not need to worry about the impact of Jensen's inequality on the forecast statistics (e.g., mean, variance, CI) which was an issue for the analytical methods (for ecample, EKF). The ensemble-based approach also makes it easier to accommodate other sources of uncertainty, such as uncertainty in parameters and model drivers, or stochastic processes such as disturbance. These can be included by sampling them as well, at the same time as the sampling of the initial conditions, thus producing an ensemble forecast that includes multiple sources of uncertainty simultaneously. The disadvantage of the ensemble approach is that it requires the additional computation of a larger number of model runs, rather than running the model once (as was done in KF and EKF). All in all, these trade-offs have made ensemble forecasting one of the most popular data assimilation approaches in ecology. 

...
...

190 

