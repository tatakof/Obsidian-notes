### Definitions
- Data generating process
Probability distributions over the observation space. 

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
In practice it helps to assign distinct, numerical LABELS to each data generating processes within an observational model??????



## Doubts 
- the latent phenomenon is encompassed within the true data data generating process? what does this mean?. 
"In particular, successful inferences advice decisions about how to interact with the latent phenomenon encompassed within the true data generating process."


### Data generating process
If we have any uncertainty about the system that we're analyzing the the true data generating process will be unknown. **Inference is tasked with quantifying information about the true data generating process using observed data as its only expression.** In particular, successful inferences advice decisions about how to interact with the latent phenomenon encompassed within the true data generating process.

#### Why the data generating process is unknown?
Simply because if we have uncertainty about the system (m'what type of uncertainty'?) we cannot know for sure which is the *true* data generating process. 



Ignorance of the true data generating process also complicates the calibration of any decision making process informed by our inferences. 


In order to fin the appropriate data generating process we would ideally search though the space of all data generating processes, that is,  the collection $\mathcal{P}$ of all probability distributions over the observation space. 
But the big world of data generating processes is just too large and complex to be able to quantify in any practical application, so we have to limit our search to something more tractable in practical applications. 
That is, we have to consider only a small world, $\mathcal{S} \subset \mathcal{P}$, of data generating processes that is more manageable. 

This small world defines an *observational MODEL* consisting of individual data generating process that each define a possible mathematical narrative of how the data could be generated. m' so the observational MODEL consists of individual probability distributions over the observation space that each define a possible mathematical narrative of how the data could be generated'. 

![[Pasted image 20220623133926.png]]
