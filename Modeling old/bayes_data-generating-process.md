### Definitions
- Data generating process
Probability distributions over the observation space. 
Mathematical narrative of how the data could be generated. 


- True data generating process
The probability distribution that exactly captures the observational process in a given application. 

- Model configuration space, $\mathcal{S}$
The subset of data generating processes considered in a given analysis. 
Model configuration space and Observational model can be used interchangeably. 


- Model configuration
An individual data generating process considered in a given analysis. 

- Observational model
its the same as the model configuration space (interchangeable). 
It consists of individual data generating process that each define a possible mathematical narrative of how the data could be generated. m' so the observational MODEL consists of individual probability distributions over the observation space that each define a possible mathematical narrative of how the data could be generated'. 

- Parameterization of an observational model
Is the one-to-one mapping between the model configuration space and the numerical space $\Theta$, such as the real numbers. In other words, a parameterization is the assignment of a unique value, or *parameter* $\theta \in \Theta$, to each model configuration, $s \in \mathcal{S}$. Keep in mind that the parameterizations themselves are not unique; in general there will be many equivalent ways of LABELING model configurations. 
In practice it helps to assign distinct, numerical LABELS to each data generating processes within an observational model?????? are we labelling or assigning values to the parameters of the data generating process????




## Doubts 
- the latent phenomenon is encompassed within the true data data generating process? what does this mean?. 
"In particular, successful inferences advice decisions about how to interact with the latent phenomenon encompassed within the true data generating process."
- Is a model configuration for e.g. for a gaussian a single value of mu and a a single value of sigma? so if in a bayesian context we have a distribution of posterior mu values, that means that we have a distribution of model configurations? I thought that a model configuration was like a model variant. "Once we limit out consideration to a given observational model, our inferential goal becomes the quantification of those model configurations that are somehow similar to the true data generating process, and hence useful for informing our ultimate decisions. If the observational model contains the true data generating process then basing our inferences on the observational model incurs no loss; an exhaustive search through the observational model will always be able to find the true data generating process. We are not always, however, so fortunate. What happens when the true data generating process lies outside the scope of the observational model?"
- Is a data generating process a model with point values of parameters? and the model configuration space is the same model but with distributions of parameters? If the true data generating process is a model with point parameters, then we are always assuming some sort of determinism of the world we are trying to understand. 

### Data generating process
If we have any uncertainty about the system that we're analyzing the the true data generating process will be unknown. **Inference is tasked with quantifying information about the true data generating process using observed data as its only expression.** In particular, successful inferences advice decisions about how to interact with the latent phenomenon encompassed within the true data generating process.

#### Why the data generating process is unknown?
Simply because if we have uncertainty about the system (m'what type of uncertainty'?) we cannot know for sure which is the *true* data generating process. 



Ignorance of the true data generating process also complicates the calibration of any decision making process informed by our inferences. 

"### problems for properly finding the true data generating process"
In order to fin the appropriate data generating process we would ideally search though the space of all data generating processes, that is,  the collection $\mathcal{P}$ of all probability distributions over the observation space. 
But the big world of data generating processes is just too large and complex to be able to quantify in any practical application, so we have to limit our search to something more tractable in practical applications. 
That is, we have to consider only a small world, $\mathcal{S} \subset \mathcal{P}$, of data generating processes that is more manageable. 

This small world defines an *observational MODEL* consisting of individual data generating process that each define a possible mathematical narrative of how the data could be generated. m' so the observational MODEL consists of individual probability distributions over the observation space that each define a possible mathematical narrative of how the data could be generated'. 

![[Pasted image 20220623133926.png]]
In practice it helps to assign distinct, numerical labels to each data generating processes within an observational model. A _parameterization_ of an observational model is the one-to-one mapping between the model configuration space and a numerical space $Θ$, such as the real numbers. In other words, a parameterization is the the assignment of a *unique* value, or _parameter_ $θ∈Θ$, *to each* model configuration, $s∈S$  (m'SO THAT MEANS THAT A MODEL CONFIGURATION IS A MODEL WITH A GIVEN PARAMETER VALUE AND SO A MODEL WITH A DISTRIBUTION OF PARAMETER VALUES ITS AN MODEL CONFIGURATION SPACE?). Keep in mind that the parameterizations themselves are not unique; in general there will be many equivalent ways of labeling (m'WHY "LABELING"??') the model configurations.

Given a parameterization we can the specify the observational model (i.e., the subset of data generating processes (DGPs) considered in a given analysis) with a family (m'because there are many DGPs?) of probability density functions over the observational space, $\pi_\mathcal{S} (y; s)$. In practice, we index these densities a particular parameterization $\pi_\mathcal{S} (y;\theta)$ 

m' When we are modeling, we have to limit our consideration to a given observational model. For example, a distribution of gaussian probability density functions over the observational space (assuming our observational space is the one-dimensional real numbers, $Y = \mathbb{R}$.) 
$$
\pi_{\mathcal{S}} (y ; \mu, \sigma)
=
\frac{1}{ \sqrt{2 \pi \sigma^{2}} }
\exp \left( - \frac{1}{2} \left( \frac{y - \mu}{\sigma} \right)^{2} \right).

$$
Have in mind that for each value that $\mu$ and $\sigma$ takes, we have a gaussian probability density function. Once we have many values of $\mu$ and $\sigma$, then we have our observational model, because we have a distribution of gaussian probability density functions, determined by the distribution of $\mu$ values and the distribution of $\sigma$ values. ? '


Under $N$ repeated observations our observational space would become $Y = \mathbb{R}^N$ with the corresponding probability density functions. 

$$
\pi_{\mathcal{S}} (y_{1}, \ldots, y_{N} ; \mu, \sigma)
=
\prod_{n = 1}^{N} \pi_{\mathcal{S}} (y_{n} ; \mu, \sigma).
$$
m' Remember that this is assuming the observations are independent, and if so, the probability of a sequence of observations is the product of the probability of each observation $\pi_\mathcal{S}$'


"Once we limit our consideration to a given observational model, our inferential goal becomes the quantification of those model configurations (m'that is, the distribution of parameters of a model??') that are somehow similar to the true data generating process, and hence useful for informing our ultimate decisions."

If the observational model contains the true data generating process then basing our inferences on the observational model incurs no loss (m'loss of what? of information? no loss means no bias in the estimation of a parameter?'), an exhaustive search through the observational model will always be able to find the true data generating process (m'ADD HERE STUFF FROM GELMANS PAPER ON M-OPEN OR M-CLOSED).




#### what happens when the true data generating process lies outside the scope of the observational model?
![[Pasted image 20220702105320.png]]

This is the rule rather than the exception. 
In applications observational models are limited by the constraints of mathematical and computational feasibility, and will not completely capture the ridiculous complexity of the natural world. 

##### Then, are we doomed?
NO
The inferences generated from an observational model that doesn't contain the true data generating process may still be meaningful so long as the data generating processes captures the structure of the true data generating process *relevant* to our ultimate inferential goals. 
For example, an ecological model that neglects quantum mechanics and general relativity is too technically meager to capture the _full reality_ of any observation of animal migration. Most ecological research, however, is sufficiently useful without having to consider what might happen if birds started migrating at the speed of light or quantum tunneling through geographical impediments. At the same time, research considering bird navigation guided by following physiological sensitivity to magnetic fields might need some consideration of quantum mechanics.


Ultimately inference within an observational model will at best *approximate* the true data generating process (m' i guess that will approximate if it contains the true data generating process? because every model by definition is a simplification of nature and thus an approximation?')
Only with respect for the given application and careful work can we develop an observational model that contains model configurations that *sufficiently well approximate* the true data generating process, providing the foundation for useful inferences. 

Principled model development strives for an observational process that captures the relevant structure of the phenomenon, environment, and probe that give rise to the true data generating process. We always have to be careful, to recognize the limitations of even the most carefully designed observational model in any given analysis. 







##### The case of Linear Regression. 



------------------------------------------------------------
DOUBT
what does  $\pi_\mathcal{S} (y; s)$ mean?
$\pi$ is a probability distribution
$\pi_\mathcal{S}$ means probability density function over the observation space?
$\pi_\mathcal{S} (y; s)$ means that this function depends on $y$ and $s$?
$y$ are the realized observations? betancourt said that $y$ denotes an arbitrary point in the observation space whereas $\tilde{y}$ denotes a particular point.  
$s$ are the possible observations of the observational space? (note that here $s$ is lower case, whereas in $\pi$ it is upper case). Or $s$ is a given model configuration and $S$ is the model configuration space.





------------------------------------------------------------
"Once we limit our consideration to a given observational model, our inferential goal becomes the quantiication of those model configurations that are somehow similar to the true data generating process, and hence useful for informing our ultimate decisions"