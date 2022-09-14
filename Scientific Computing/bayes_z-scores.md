explain z scores


also explain that thing of speaking math where the division is like centering on the denominator or like asking how many numerators fit in the denominator. 



### 1.3.2 A Bayesian Eye Chart
Regardless of the specific goals of an analysis we are often interested in the general behavior of the posterior distribution induced by possible observations, especially any pathological behavior that might manifest from our model assumptions. Conveniently there are two characteristics of the posterior distribution that can identify a variety of possible problems.

First let's consider the _posterior z__-score_ of a given parameter in the model configuration space,

$$
z[f \mid \tilde{y}, \theta^{\dagger}] =
\frac{ \mathbb{E}_{\mathrm{post}}[f \mid \tilde{y}] - f(\theta^{\dagger}) }
{ \mathbb{s}_{\mathrm{post}}[f \mid \tilde{y} ] },
$$
where θ† is the parameter corresponding to the true data generating process and spost the standard deviation of the function f. The posterior z-score quantifies how accurately the posterior recovers the true model configuration along this coordinate. Smaller values indicate a posterior that more strongly concentrates around the true value while larger values indicate a posterior that concentrates elsewhere. Note that the posterior z-score captures neither the bias nor the precision of the posterior distribution but rather a combination of the two.