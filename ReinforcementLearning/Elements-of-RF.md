Beyond the agent and the environment, one can identify four main subelements of a
reinforcement learning system: a **policy, a reward signal , a value function, and, optionally,
a model of the environment.**

A **policy** defines the learning agent’s way of behaving at a given time. Roughly speaking,
a policy is a mapping from perceived states of the environment to actions to be taken
when in those states. It corresponds to what in psychology would be called a set of
stimulus–response rules or associations. In some cases the policy may be a simple function
or lookup table, whereas in others it may involve extensive computation such as a search
process. The policy is the core of a reinforcement learning agent in the sense that it alone
is sufficient to determine behavior. In general, policies may be stochastic, specifying
probabilities for each action.

A **reward signal** defines the goal of a reinforcement learning problem. On each time
step, the environment sends to the reinforcement learning agent a single number called
the reward. The agent’s sole objective is to maximize the total reward it receives over
the long run. The reward signal thus defines what are the good and bad events for the
agent. In a biological system, we might think of rewards as analogous to the experiences
of pleasure or pain. They are the immediate and defining features of the problem faced
by the agent. The reward signal is the primary basis for altering the policy; if an action
selected by the policy is followed by low reward, then the policy may be changed to
select some other action in that situation in the future. In general, reward signals may
be stochastic functions of the state of the environment and the actions taken.

Whereas the reward signal indicates what is good in an immediate sense, **a value
function** specifies what is good in the long run. Roughly speaking, the value of a state is
the total amount of reward an agent can expect to accumulate over the future, starting
from that state. Whereas rewards determine the immediate, intrinsic desirability of
environmental states, values indicate the long-term desirability of states after taking into
account the states that are likely to follow and the rewards available in those states. For
example, a state might always yield a low immediate reward but still have a high value
because it is regularly followed by other states that yield high rewards. Or the reverse
could be true. To make a human analogy, rewards are somewhat like pleasure (if high)
and pain (if low), whereas values correspond to a more refined and farsighted judgment
of how pleased or displeased we are that our environment is in a particular state.


Rewards are in a sense primary, whereas values, as predictions of rewards, are secondary.
Without rewards there could be no values, and the only purpose of estimating values is to
achieve more reward. Nevertheless, it is values with which we are most concerned when
making and evaluating decisions. Action choices are made based on value judgments. We
seek actions that bring about states of highest value, not highest reward, because these
actions obtain the greatest amount of reward for us over the long run. Unfortunately, it
is much harder to determine values than it is to determine rewards. Rewards are basically
given directly by the environment, but values must be estimated and re-estimated from
the sequences of observations an agent makes over its entire lifetime. In fact, the most
important component of almost all reinforcement learning algorithms we consider is a method for efficiently estimating values. The central role of value estimation is arguably
the most important thing that has been learned about reinforcement learning over the
last six decades.


The fourth and final element of some reinforcement learning systems is **a model of
the environment**. This is something that mimics the behavior of the environment, or
more generally, that allows inferences to be made about how the environment will behave.
For example, given a state and action, the model might predict the resultant next state
and next reward. Models are used for planning, by which we mean any way of deciding
on a course of action by considering possible future situations before they are actually
experienced. Methods for solving reinforcement learning problems that use models and
planning are called model-based methods, as opposed to simpler model-free methods that
are explicitly trial-and-error learners—viewed as almost the opposite of planning. In
Chapter 8 we explore reinforcement learning systems that simultaneously learn by trial
and error, learn a model of the environment, and use the model for planning. Modern
reinforcement learning spans the spectrum from low-level, trial-and-error learning to
high-level, deliberative planning.






















