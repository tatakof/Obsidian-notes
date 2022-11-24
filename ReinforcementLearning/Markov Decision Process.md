The general framework of MDPs allows us to model virtually any complex sequential decision-making problem under uncertainty in a way that RL agents can interact with and learn to solve solely through experience.

In RL, we assume all environments have an MDP working under the hood. Whether an Atari game, the stock market, a self-driving car, your significant other, you name it, every problem has an MDP running under the hood (at least in the RL world, whether right or wrong).


MDPs make available a set of actions A that depends on the state. That is, there might be
actions that aren’t allowed in a state—in fact, A is a function that takes a state as an argument;
that is, A(s). This function returns the set of available actions for state s. If needed, you can
define this set to be constant across the state space; that is, all actions are available at every
state. You can also set all transitions from a state-action pair to zero if you want to deny an
action in a given state. You could also set all transitions from state s and action a to the same
state s to denote action a as a no-intervene or no-op action.

Just as with the state, the action space may be finite or infinite, and the set of variables of a
single action may contain more than one element and must be finite. However, unlike the
number of state variables, the number of variables that compose an action may not be con-
stant. The actions available in a state may change depending on that state. For simplicity,
most environments are designed with the same number of actions in all states.

The environment makes the set of all available actions known in advance. Agents can select
actions either deterministically or stochastically. This is different than saying the environ-
ment reacts deterministically or stochastically to agents’ actions. Both are true statements,
but I’m referring here to the fact that agents can either select actions from a lookup table or
from per-state probability distributions.

