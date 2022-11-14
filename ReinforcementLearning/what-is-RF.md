1.6
Summary
Reinforcement learning is a computational approach to understanding and automating
goal-directed learning and decision making. It is distinguished from other computational
approaches by its emphasis on learning by an agent from direct interaction with its
environment, without requiring exemplary supervision or complete models of the envi-
ronment. In our opinion, reinforcement learning is the first field to seriously address the
computational issues that arise when learning from interaction with an environment in
order to achieve long-term goals.
Reinforcement learning uses the formal framework of Markov decision processes to
define the interaction between a learning agent and its environment in terms of states,
actions, and rewards. This framework is intended to be a simple way of representing
essential features of the artificial intelligence problem. These features include a sense of
cause and e↵ect, a sense of uncertainty and nondeterminism, and the existence of explicit
goals.
The concepts of value and value function are key to most of the reinforcement learning
methods that we consider in this book. We take the position that value functions
are important for efficient search in the space of policies. The use of value functions
distinguishes reinforcement learning methods from evolutionary
END SUMMARY



Reinforcement learning is learning what to do—how to map situations to actions—so
as to maximize a numerical reward signal. The learner is not told which actions to
take, but instead must discover which actions yield the most reward by trying them. In
the most interesting and challenging cases, actions may a↵ect not only the immediate reward but also the next situation and, through that, all subsequent rewards. These two
characteristics—trial-and-error search and delayed reward—are the two most important
distinguishing features of reinforcement learning.

Reinforcement learning, like many topics whose names end with “ing,” such as machine
learning and mountaineering, is simultaneously a problem, a class of solution methods
that work well on the problem, and the field that studies this problem and its solution
methods. It is convenient to use a single name for all three things, but at the same time
essential to keep the three conceptually separate. In particular, the distinction between
problems and solution methods is very important in reinforcement learning; failing to
make this distinction is the source of many confusions.

Although one
might be tempted to think of reinforcement learning as a kind of unsupervised learning
because it does not rely on examples of correct behavior, reinforcement learning is trying
to maximize a reward signal instead of trying to find hidden structure. Uncovering
structure in an agent’s experience can certainly be useful in reinforcement learning, but by
itself does not address the reinforcement learning problem of maximizing a reward signal.
We therefore consider reinforcement learning to be a third machine learning paradigm,
alongside supervised learning and unsupervised learning and perhaps other paradigms.


Another key feature of reinforcement learning is that it explicitly considers the whole
problem of a goal-directed agent interacting with an uncertain environment. This is in
contrast to many approaches that consider subproblems without addressing how they
might fit into a larger picture.

Another key feature of reinforcement learning is that it explicitly considers the whole
problem of a goal-directed agent interacting with an uncertain environment. This is in
contrast to many approaches that consider subproblems without addressing how they
might fit into a larger picture. For example, we have mentioned that much of machine
learning research is concerned with supervised learning without explicitly specifying how
such an ability would finally be useful. Other researchers have developed theories of
planning with general goals, but without considering planning’s role in real-time decision
making, or the question of where the predictive models necessary for planning would
come from. Although these approaches have yielded many useful results, their focus on
isolated subproblems is a significant limitation.
Reinforcement learning takes the opposite tack, starting with a complete, interactive,
goal-seeking agent. All reinforcement learning agents have explicit goals, can sense
aspects of their environments, and can choose actions to influence their environments.
Moreover, it is usually assumed from the beginning that the agent has to operate despite
significant uncertainty about the environment it faces. When reinforcement learning
involves planning, it has to address the interplay between planning and real-time action
selection, as well as the question of how environment models are acquired and improved.
When reinforcement learning involves supervised learning, it does so for specific reasons
that determine which capabilities are critical and which are not. For learning research to
make progress, important subproblems have to be isolated and studied, but they should
be subproblems that play clear roles in complete, interactive, goal-seeking agents, even if
all the details of the complete agent cannot yet be filled in.

...

These examples share features that are so basic that they are easy to overlook. All
involve interaction between an active decision-making agent and its environment, within
which the agent seeks to achieve a goal despite uncertainty about its environment. The
agent’s actions are permitted to a↵ect the future state of the environment (e.g., the
next chess position, the level of reservoirs of the refinery, the robot’s next location and
the future charge level of its battery), thereby a↵ecting the actions and opportunities
available to the agent at later times. Correct choice requires taking into account indirect,
delayed consequences of actions, and thus may require foresight or planning.

At the same time, in all of these examples the e↵ects of actions cannot be fully predicted;
thus the agent must monitor its environment frequently and react appropriately.

In all of these examples the agent can use its experience to improve its performance
over time.

The knowledge the agent brings to the task at
the start—either from previous experience with related tasks or built into it by design or
evolution—influences what is useful or easy to learn, but interaction with the environment
is essential for adjusting behavior to exploit specific features of the task.






































