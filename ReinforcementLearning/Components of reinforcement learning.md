Agents and Environment. 


### Agent
The agent is the decision maker, and is the solution to a problem. Most agents have a three-step process: all agents have an interaction component, a way to gather data for learning: all agents evaluate their current behavior; and all agents improve something in their inner components that allows them to improve (or at least attempt to improve) their overall performance. 

An agent is a decision maker only and nothing else. In the example of a robot that picks up objects, only the code that makes decisions is referred to as the agent (the rest is the environment)

The agent has a three-step process: the agent interacts with the environment, the agent evaluates its behavior, and the agent improves its responses. The agent can be designed to learn mappings from observations to actions called policies. The agent can be designed to learn the model of the environment on mappings called models. The agent can be designed to learn to estimate reward-to-go on mappings called value functions. 


### Environment
The environment is everything outside the agent; everything the agent has no total control over. The decision maker is the agent, everything that comes after the decision gets bundled into the environment. 


The environment is the prepresentation of a problem. The environment is represented by a set of variables related to the problem. The combination of all the possible values this set of variables can take is reerred to as the state stace. A state is a specific set of values the variables take at any given time. 

Agents may or may not have access to the actual environment's statel however, one way or another, agents can observe something from the environment. The set of variables the agent perceives at any given time is called an observation. 

At every state, the environment makes available a set of action that the agent can choose from. Often the set of actions if the same for all states, but this isn't required. The set of all actions in all states is referred to as the action space. 



One of the fundamental distinctions of RL from other ML approaches is that the agent and the environment interact; the agent attempts to influence the environment through actions, and the environment reacts to the agent’s actions.


### The reinforcement learning-interaction cycle
1. The agent perceives the environment (observation and reward) 
2. The agent takes an action 
3. The environment goes through internal state change as a consequence of the agent's action. 
4. The environment reacts with new observation and a reward. 


