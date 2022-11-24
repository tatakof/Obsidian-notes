
### Deep reinforcement learning
A machine learning approach to artificial intelligence concerned with creating computer programs that can solve problems requiring intelligence. The distinct property of DRL programs is learning though trial and error from feedback that's simultaneously sequential, evaluative, and sampled by leveraging powerful non-linear function approximation. 
In this type of task, no human labels data, and no human collects or explicitly designs the collection of data. 
At its core, DRL is about complex sequential decision-making problems under uncertainty. 


### Supervised learning.
The task of learning from labeled data. The human dicides which data to collect and how to label it. the goal in SL is to generalize. 


### Unsupervised learning
the task of learning from unlabeled data. Even though data no longer need labeling, the methods used by the computer to gather data still need to be designed by a human. The goal in UL is to compress. e.g. in a clustering model, the clusters compress the information, uncovering underlying relationships. 




### Inverse Reinforcement Learning
a technique in which an agent learns from expert demonstrations. 


### Artificial neural networks
Multi-layered non-linear function approximators. 


### Policies
mappings from observations to actions. 

### Value functions
mappings from observations (and possibly actions) to reward-to-go estimates (aslice of the return)

### Models
Mappings from observations to new observations and/or rewards. 


### Time step
Each cycle of an interaction between the agent and the environment (these interactions go on for several cycles)

### Experience (also experience tuple)
The set of state, action, reward and new state. (at each time step, the agent observes the environment, takes and action, and receives a new observation and a reward)
Every experience tuple has an opportunity for learning and improving performance. 




### Episodic tasks
tasks that an agent is trying to solve that have a natural ending

### Episode
The sequence of time-steps from the begging to the end of an episodic task is called an episode. 


### Continuing tasks. 
Tasks that an agent is trying to solve that don't have a natural ending. 




### State space 
The environment is the prepresentation of a problem. The environment is represented by a set of variables related to the problem. The combination of all the possible values this set of variables can take is reerred to as the state stace. A state is a specific set of values the variables take at any given time. 
The state-space is defined as the set S. The state space can be finite or infinite. The state space is different than the set of variables that compose a single state. This other set must always be finite and of constant size from state to state. In the end, the state space is a set of sets. The inner set must be of equal size and finite, as it contains the number of variables representing the states, but the outer set can be infinite depending on the types of elements of the inner sets. 
A state space is a set of sets. 

### State
a state is a unique and self-contined configuration of the problem. A single state is composed of a set of variables and has to be finite and of constant size from state to state. The state set contians the number of variables representing the states. 


### Observation 
Agents may or may not have access to the actual environment’s state; however, one way or another, agents can observe something from the environment. The set of variables the agent perceives at any given time is called an observation.

### Observation space 
The combination of all posible observations is the observation space. Is composed by a set of variables. This set must always be finite and of constant size from state to state. 


### Action space
At every state, the environment makes available a set of action that the agent can choose from. Often the set of actions if the same for all states, but this isn't required. The set of all actions in all states is referred to as the action space. 



### Transition function
The function that is responsible for the transition betwen environment's states as a response to agent's actions. 

The way the environment changes as a response to actions is referred to as the state-transition probabilities, or more simply, the transition function, and is denoted by T(s, a, s'). The transition function T maps a transition tuple s, a, s' to a probability; that is, you pass in a state s, an action a, and a next state s', and it’ll return the corresponding probability of transition from state s to state s' when taking action a. You could also represent it as T(s, a) and return a dic-tionary with the next states for its keys and probabilities for its values.

Notice that T also describes a probability distribution p( · | s, a) determining how the system
will evolve in an interaction cycle from selecting action a in state s. When integrating over the next states s', as any probability distribution, the sum of these probabilities must equal one.

![[Pasted image 20221114101939.png]]





### Reward function
After an environment's state transition, the environment emits a new observation and may also provide a reward signal as a response. The function responsible for this mapping is called the reward function. That is, the reward function is the mapping between state's transition and reward signals??
The reward-function signals can be simultaneuosly sequential, evaluative and sampled. 


### Model of the environment. 
The set of the transition and reward function


### Temporal credit assignment problem. 
The challenge of determining which state and/or action is responsible for a reward. (when there's temporal component to a problem, and actions have delayed consequences, it's challenging to assign credit for rewards)




### Exploration versus exploitation trade-off
The reward receibed by the agent may be weak int he sense that it may provide no supervision. The reward may indicate goodness and not correctess (wtf?) meaning it may contain no information about other potential rewards. Thus the agent must be able to learn from evaluative feedback. Evaluative feedback gives rise to the need for exploration. The agent must be able to balance the gathering of information with the exploitation of current information. This is also referred to as the exploration versus exploitation trade-off


### Return 
The sum of rewards collected in a single episode (agents are often designed to maximize the return)



### Markov Decision Process (MDPs)
The general framework of MDPs allows us to model virtually any complex sequential decision-making problem under uncertainty in a way that RL agents can interact with and learn to solve solely through experience.

In RL, we assume all environments have an MDP working under the hood. Whether an Atari game, the stock market, a self-driving car, your significant other, you name it, every problem has an MDP running under the hood (at least in the RL world, whether right or wrong).

In the case of MDPs, the states are fully observable: we can see the internal state of the environment at each time step, that is, **the observations and the states are the same**. 

All the MDPs share the Markov property

### Partially observable Markov Decision Processes (POMDPs)
Is a more general framework (more general than MDPs) for modeling environments in which observations, which still depend on the internal state of the environment, are the only things the agent can see instead of the state. 


### Markov property
The probability of moving from one state s to another state s on two separate occasions, given the same action a, is the same regardless of all previous states or actions encountered before that point. 
The probability of the next state, given the current state and action, is independent of the history of interactions. The markov property is also referred as the memoryless property. 

![[Pasted image 20221114093450.png]]




### $S^+$
The set of all states in the MDP

### $S^i$ or the set of starting or initial states. 
A subset of $S^+$
To begin interacting with and MDP, we draw a state from $S^i$ from a prob distribution. This distribution can be anything, but it must be fixed throughout training: that is, the probabilities must be the same from the first to the last episode of training and for agent evaluation. 


### Absorbing or Terminal state
A unique state called like that. It's a special state: it must have all available actions transitioning, with probability 1, to itself, and these transitions must provide no reward. Note that I'm referring to the transifitons from the terminal state, not to the terminal state. 
While it's common practice to create a single terminal state (a sink state) to which all terminal transitions go, this isn't always implemented this way. What you'll see more often is multiple terminal states, and that's okay. 

![[Pasted image 20221114094604.png]]


terminal states are
defined as states with all
actions with deterministic
transitions to themselves




### $S$ 
The set of all non-terminal states. 



### Stationarity assumption
One key assumption of many RL (and DRL) algorithms is that this distribution is stationary.
That is, while there may be highly stochastic transitions, the probability distribution may not
change during training or evaluation. Just as with the Markov assumption, the stationarity
assumption is often relaxed to an extent. However, it’s important for most agents to interact
with environments that at least appear to be stationary.

