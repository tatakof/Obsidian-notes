 ----------------------------------------------------------
MAYBE EXPLAIN ALL OF THESE IN TERMS OF MOMENTS (at the beggining or at the end of the whole writing)
#### Variance 
The variance of a variable X, noted Var(X) or $\sigma_X^2$, is a measure of roughly how spread out the values of X in a a data set or population are from their mean. If all values of X are close to one value, then the variance will be low. In the other hand, if all the values of X are spread out (cover a large range), the variance will be comparatively large.  
Mathematically, we define the variance of a variable as the expected//average square difference of that variable from its mean. 

$$
Var(X) = E((X - \mu)^2)

$$
To compute it, one can find the mean and then, if the generator of the random variable X is discrete with a probability mass function $x_1 \rightarrow p_1,\ ...,\ x_n \rightarrow p_n$  we do:  
$$
Var(x) = \sum_{i = 1}^n p_i\ (x_i - \mu)^2  
$$
If  the random variable X is continuous and thus has a probability density function $f(x)$, then we do: 
$$
Var(X) = \int_{\mathbb{R}} (x - \mu)^2 f(x)dx

$$
	where $\int$ is a platonic infinite sum? CHECK INFO THEORY BOOK




#### Standard deviation
The standard deviation $\sigma$ is just the square root of the variance. 
$$
\sigma = \sqrt{Var(X)} = \sqrt{\sigma^2}
$$

It has the advantage of having the same units as X (the variance has the units of X but squared), and it's also useful for Z scores? [[bayes_Zscores]]

And it's also useful because once we know the standard deviation, we can know how which percentage of the values of X are $\sigma$ away from the mean of X. This percentage varies according to the probability distribution of X. 

#### Covariance
The covariance of X and Y measures the degree at which X and Y *covary*, that is, the degree to which the two variables vary together, or are "associated". And this is a special case of Mutual Information (EXPLAIN). The covariance measures the association between two variables in a special way: it measures hwo X and Y **linearly** covary. This can be thought as plotting Y vs X and considering the extent to which a straight line captures the way in which Y varies as X changes. 

The covariance formula is 
$$
𝜎XY ≜ E[(X − E(X))(Y − E(Y))]
$$

where $≜$ means "is equal by definition" or ... EXPLAIN

The covariance $\sigma_{XY}$ is often normalized to yield the *correlation coefficient* $\rho_{XY}$ , which is a dimensionless number that ranges from -1 to 1 and represents the slope of the best fit line after we normalize both X and Y by their respective standard deviations. 
The formula is: 
$$
\rho{XY} = \sigma_{XY} / (\sigma_X\ \sigma_Y)
$$
The covariance equals 1 only when one variable can completely predict the other in a linear fashion, and is equal to zero when the prediction is no better than a random guess. 
"These degrees of covariation can be readily computed from the joint distribution $P(x, y)$" using the $\sigma_{XY}$ equation and the $\rho_{XY}$ equation.'' **DNT**

Both $\sigma_{XY}$ and $\rho_{XY}$ vanish when X and Y are independent. 

Note that nonlinear relationships between Y and X cannot naturally be captured by a simple numerical summary: they require a full specification of the conditional probability $P(Y = y | X = x)$ **DNT**




----------------------------------------------------------
ALL OF THIS CAME FROM PEARLS CAUSAL INFERENCE IN STATISTICS BOOK


ADD EXPLANATION FROM INFO THEORY BOOK 