Definitions:

- Observational process

 "It is any methodology that measures, collects, curates or manipulates observations sensitive to the latent phenomenon. This includes, for example, not only dedicated experiments explicitly designed to interrogate the phenomenon of interest but also retrospective analyses of incidental experiments or previously conducted experiments designed for other purposes."


Note that we distinguish *possible* outcomes of an observational process from *explicitly realized* observations. Betancourt distinguishes them as: $y$ denotes an arbitrary point in the observation space while $\tilde{y}$ denotes a particular point. 

- Observation space. 
the variation of possible outcomes of an observation process??
with variability sources being epistemological, ontological or others?

- Data generating process
Probability distributions over the observation space. 

- True data generating process
The probability distribution that exactly captures the observational process in a given application. 


- Observational process vs Observation space
???????


- Observational model 
This small world defines an *observational MODEL* consisting of individual data generating process that each define a possible mathematical narrative of how the data could be generated. m' so the observational MODEL consists of individual probability distributions over the observation space that each define a possible mathematical narrative of how the data could be generated'. 




### Doubts
- So depending on the probe you use, there's an emerging and distinct observational process. But the observational process doesn't produce constant observations, but rather a variation of possible outcomes within an observation space. I guess this observation space is also defined by the probe you use to inspect the phenomenon and its environment?. And the observation space is the consequence of there being sources of variability that doesn't allow the realized observations to be constant?
  And we model an observational process with a probability distribution over the observation space (i.e., the space of all possible observations that can emerge due to the probe we used, and due to the sources of variability of the system? with the system being the latent phenomenon + the environment). 



Our inferential target is the latent phenomenon we want to study, but no phenomenon exists in isolation. "Any phenomenon relevant to statistical inquiry instead manifests within some latent system that includes, at the very least, the mechanisms with which we can interact with it. In other word we can observe the phenomenon of interest only through its surrounding *environment*". m' dos that mean that the environment is the mechanisms with which we can interact with it????'

 ![[Pasted image 20220619125705.png]]



To make an inference we need an observational probe that explores the environment and hopefully the phenomenon of interest. 



 ### What is an observational process
 An observational process is defined by the interaction of the probe with the environment and the phenomenon. This observational process examines the latent system and induces (creates??) explicit observations that are sensitive to the phenomenon of interest. 
![[Pasted image 20220619130858.png]]

![[Pasted image 20220619130906.png]]


 "It is any methodology that measures, collects, curates or manipulates observations sensitive to the latent phenomenom. (WHATS THE MEANING OF LATENT PHENOMENOM???). This includes, for example, not only dedicated experiments explicitly designed to interrogate the phenomenon of interest but also retrospective analyses of incidental experiments or previously conducted experiments designed for other purposes."

"In encapsulating the phenomenon of interest our probe intersects only part of the surrounding environment. Consequently the observational process will be sensitive to only those elements of the environment relevant to the probe. Well-designed experiments offer the promise of better isolating the target phenomenon, yielding a much cleaner observational process and more informative observations"

An observational process is a conceptual abstraction that we need to define exactly how observations are *realized* from an observational process in order for it to take form as an explicit mathematical object. 


If we presume that the variations in an observational process? are sufficiently regular, the observational process can be quantified with a *distribution of observations* (but it cannot be quantified by any single observation). 
We model the the observational process with a probability distribution over the observation space, with realizations of the observation process modeled as exact samples from that distribution. 




### How observations arise
observations are *realized* from an observational process. But due to the nature of the observation process, the outcomes ((observations?)) are not constant but rather a *variation* of possible outcomes within an *observation space*.

#### Sources of variation of observations
The realized observations might exhibit variation due to physical, or *ontological*, stochasticity inherent to the latent phenomenon, its environment, or the probe used to interrogate them. This variation is also known as *aleatoric randomness* of the observational process. 

e.g., ontological variation is commonly posited when sampling individuals from a population. 

Epistemological variation is due to limitations in how accurately we can observe the latent system, like the precision of a ruler or the resolution of the human eye. 

Have in mind that the distinction between epistemological and ontological variation is ill-defined. For example one can argue that seemingly ontological variation is a result of the imprecise observation of complex but deterministic dynamics, as in chaos theory. Likewise one can argue that epistemological variation defines an ensemble of possible but unobserved, or counterfactual, outcomes which manifests as ontological variation if hte experiment were hypothetically repeated. 

A system can have probabilistic behaviour even if it has deterministic dynamics. 

------------------------------------------------------------
Ontology: 
"Relating to the branch of metaphysics dealing with the nature of being." 
"showing the relations between the concepts and categories in a subject area or domain".

"**Ontology** is the branch of [philosophy](https://en.wikipedia.org/wiki/Philosophy "Philosophy") that studies concepts such as [existence](https://en.wikipedia.org/wiki/Existence "Existence"), [being](https://en.wikipedia.org/wiki/Being "Being"), [becoming](https://en.wikipedia.org/wiki/Becoming_(philosophy) "Becoming (philosophy)"), and [reality](https://en.wikipedia.org/wiki/Reality "Reality"). It includes the questions of how entities are grouped into [basic categories](https://en.wikipedia.org/wiki/Category_of_being "Category of being") and which of these entities exist on the most fundamental level... Ontologists often try to determine what the _categories_ or _highest kinds_ are and how they form a _system of categories_ that provides an encompassing classification of all entities. Commonly proposed categories include [substances](https://en.wikipedia.org/wiki/Substance_(philosophy) "Substance (philosophy)"), [properties](https://en.wikipedia.org/wiki/Property_(philosophy) "Property (philosophy)"), [relations](https://en.wikipedia.org/wiki/Relations_(philosophy) "Relations (philosophy)"), [states of affairs](https://en.wikipedia.org/wiki/States_of_affairs "States of affairs") and [events](https://en.wikipedia.org/wiki/Event_(philosophy) "Event (philosophy)"). These categories are characterized by fundamental ontological concepts, like _particularity_ and _universality_, _abstractness_ and _concreteness_, or _possibility_ and _necessity_."


w
Aleatoric randomness:


Epistemic uncertainty: 
refering to a lack of knowledge, something we could in principle know for sure. 

Aleatoric vs epistemic uncertainty:
https://www.stat.berkeley.edu/~aldous/Real_World/ale_epi.html
"Philosophers have long emphasized a distinction between aleatoric and epistemic uncertainty. _Epistemic_ refers to lack of knowledge -- something we could in principle know for sure -- in contrast to _aleatoric_ "intrinsic randomness" involved in which of possible futures will actually occur. As a basic iconic example of the distinction between these two categories, consider whether the top card of a deck will be an Ace after I shuffle and look at it. The uncertainty here is _aleatoric_ before I shuffle, but becomes _epistemic_ after shuffling but before looking."

------------------------------------------------------------


### How we model an Observational process
We model an observational process with a probability distribution over the observational space (i.e. the space of all possible observations that can arise from a given observational process), with realizations of the observation process modeled as exact samples from that distribution. To model the observational process this way we have to make the assumption that the variation of the system that produces the observations is sufficiently regular that it can be quantified by a distribution of observations (but not by a single observation).
Once we define the probability distribution over the observation space we have what we call a *data generating process*. If our probability distribution exactly captures the observational process in a given application then we call it the *true data generating process*, $\pi ^ \dagger$ 
![[Pasted image 20220625152132.png]]
(
What i dont really get of this picture is: the observational process produces an observation space, Y, due to the inherent variability, and if we model the observational process correctly then we have a true data generating process, $\pi ^ \dagger$?
)

"To distinguish possible outcomes of an observational process from explicitly realized observations I will decorate the latter with a tilde. In other words y denotes an arbitrary point in the observation space while y~ denotes a particular point."
m' what are the possible outcomes of an observational process? the whole observation space?'




### Why we need well-designed experiments

"In encapsulating the phenomenon of interest our probe intersects only part of the surrounding environment. Consequently the observational process will be sensitive to only those elements of the environment relevant to the probe. Well-designed experiments offer the promise of better isolating the target phenomenon, yielding a much cleaner observational process and more informative observations"


"In encapsulating the phenomenon of interest our probe intersects only part of the surrounding environment. Consequently the observational process will be sensitive to only those elements of the environment relevant to the probe. Well-designed experiments offer the promise of better isolating the target phenomenon, yielding a much cleaner observational process and more informative observations"

but there's no unique procedure for interrogating and environment and the phenomena within it, so theres never a singular experimental probe and instead each of the many possible procedures results in its own probe. So Each procedure in an experiment yields a different observational experiments
![[Pasted image 20220619131449.png]]
![[Pasted image 20220619131455.png]]


Distinct observational processes can become the basis of of independent analyses or even  components in a single joint analysis that aggregates data from multiple sources. 

In consequence, the observational process are bespoke to both the given phenomenon and the specific details of the probe used to investigate it, especially the environment with which the probe intersects. A critical aspect of statistical modeling is capturing enough of these details to isolate inferences about the latent phenomenon that can then be fairly compared across different experiments. **this is especially true when the specific behavior of the environment or the probe is transient or otherwise not exactly repeatable**. Without a rich understanding of the observational process, phenomenological inferences can poorly generalize outside the of the exact context of the given experiment, promoting more confusion than comprehension. 


Latent Phenomenon: 
Latent: 
(of a quality or state) existing but not yet developed or manifest; hidden or concealed. 

Phenomenon: 
a fast or situation that is observed to exist or happen, especially one whose cause or expl


Retrospective analysis:

Incidental experiments: 



### Why it is important
"Without a rich understanding of the observational process, phenomenological inferences can poorly generalize outside of the exact context of the given experiment (WHY), promoting more confusion than comprehension"


**NEED TO REREAD THE HOLE SECTION**
https://betanalpha.github.io/assets/case_studies/modeling_and_inference.html#original_computing_environment  
