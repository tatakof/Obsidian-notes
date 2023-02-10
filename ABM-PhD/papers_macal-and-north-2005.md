Agent-based modelling and simulation (ABMS) is a relatively new approach to modelling systems composed of
autonomous, interacting agents. Agent-based modelling is a way to model the dynamics of complex systems and
complex adaptive systems. Such systems often self-organize themselves and create emergent order. Agent-based models
also include models of behaviour (human or otherwise) and are used to observe the collective effects of agent behaviours
and interactions. The development of agent modelling tools, the availability of micro-data, and advances in
computation have made possible a growing number of agent-based applications across a variety of domains and
disciplines. This article provides a brief introduction to ABMS, illustrates the main concepts and foundations, discusses
some recent applications across a variety of disciplines, and identiﬁes methods and toolkits for developing agent models.


Agent-based modelling and simulation (ABMS) is a relatively
new approach to modelling complex systems composed of
interacting, autonomous ‘agents’. Agents have behaviours,
often described by simple rules, and interactions with other
agents, which in turn inﬂuence their behaviours. By mode-
lling agents individually, the full effects of the diversity that
exists among agents in their attributes and behaviours can be
observed as it gives rise to the behaviour of the system as a
whole. By modelling systems from the ‘ground up’—agent-
by-agent and interaction-by-interaction—self-organization
can often be observed in such models. Patterns, structures,
and behaviours emerge that were not explicitly programmed
into the models, but arise through the agent interactions. The
emphasis on modelling the heterogeneity of agents across a
population and the emergence of self-organization are two of
the distinguishing features of agent-based simulation as
compared to other simulation techniques such as discrete-
event simulation and system dynamics. Agent-based model-
ling offers a way to model social systems that are composed
of agents who interact with and inﬂuence each other, learn
from their experiences, and adapt their behaviours so they
are better suited to their environment.


Applications of agent-based modelling span a broad range
of areas and disciplines. Applications range from modelling
agent behaviour in the stock market (Arthur et al, 1997) and
supply chains (Macal, 2004a) to predicting the spread of
epidemics (Bagni et al, 2002) and the threat of bio-warfare
(Carley et al, 2006), from modelling the adaptive immune
system (Folcik et al, 2007) to understanding consumer pur-
chasing behaviour (North et al, 2009), from understanding
the fall of ancient civilizations (Kohler et al, 2005) to model-
ling the engagement of forces on the battleﬁeld (Moffat et al,
2006) or at sea (Hill et al, 2006), and many others.

Some of
these applications are small but elegant models, which
include only the essential details of a system, and are aimed
at developing insights into a social process or behaviour.
Other agent-based models are large scale in nature, in which
a system is modelled in great detail, meaning detailed data
are used, the models have been validated, and the results are
intended to inform policies and decision making. These
applications have been made possible by advances in the
development of specialized agent-based modelling software,
new approaches to agent-based model development, the
availability of data at increasing levels of granularity, and
advancements in computer performance

Following the conventional deﬁnition of simulation,
we use the term ABMS in this article to refer to both
agent-based simulation, in which a dynamic and time-dependent process is modelled, and more general kinds of
agent-based modelling that includes models designed to do
optimization (see, eg, Olariu and Zomaya, 2006) or search
(see, eg, Hill et al, 2006). For example, particle swarm
optimization and ant optimization algorithms are both
inspired by agent-based modelling approaches and are used
to achieve an end (optimal) state rather than to investigate a
dynamic process, as in a simulation.

1. A set of agents, their attributes and behaviours.
2. A set of agent relationships and methods of interaction:
An underlying topology of connectedness deﬁnes how
and with whom agents interact.
3. The agents’ environment: Agents interact with their
environment in addition to other agents.
A model developer must identify, model, and program these
elements to create an agent-based model.

To run an
agent-based model is to have agents repeatedly execute their
behaviours and interactions. This process often does, but is
not necessarily modelled to, operate over a timeline, as in
time-stepped, activity-based, or discrete-event simulation
structures.

2.3. Autonomous agents
The single most important deﬁning characteristic of an agent
is its capability to act autonomously, that is, to act on its
own without external direction in response to situations it
encounters. Agents are endowed with behaviours that allow
them to make independent decisions. Typically, agents are
active, initiating their actions to achieve their internal goals,
rather than merely passive, reactively responding to other
agents and the environment.

There is no universal agreement in the literature on the
precise deﬁnition of an agent beyond the essential property
of autonomy. Jennings (2000) provides a computer science
deﬁnition of agent that emphasizes the essential character-
istic of autonomous behaviour. Some authors consider any
type of independent component (software, model, indi-
vidual, etc) to be an agent (Bonabeau, 2001). In this view, a
component’s behaviour can range from simplistic and
reactive ‘if-then’ rules to complex behaviours modelled by
adaptive artiﬁcial intelligence techniques. Other authors
insist that a component’s behaviour must be adaptive, able
to learn and change its behaviours in response to its
experiences, to be called an agent. Casti (1997) argues that
agents should contain both base-level rules for behaviour
and higher-level rules that are in effect ‘rules to change the
rules’. The base-level rules provide more passive responses to
the environment, whereas the ‘rules to change the rules’
provide more active, adaptive capabilities.
From a practical modelling standpoint, based on how
and why agent-models are actually built and described in
applications, we consider agents to have certain essential
characteristics:
 An agent is a self-contained, modular, and uniquely
identiﬁable individual. The modularity requirement im-
plies that an agent has a boundary. One can easily
determine whether something is part of an agent, is not
part of an agent, or is a shared attribute. Agents have
attributes that allow the agents to be distinguished from
and recognized by other agents.
 An agent is autonomous and self-directed. An agent can
function independently in its environment and in its
interactions with other agents, at least over a limited range
of situations that are of interest in the model. An agent
has behaviours that relate information sensed by the agent
to its decisions and actions. An agent’s information comes
through interactions with other agents and with the
environment. An agent’s behaviour can be speciﬁed by
anything from simple rules to abstract models, such as
neural networks or genetic programs that relate agent
inputs to outputs through adaptive mechanisms.
 An agent has a state that varies over time. Just as a system
has a state consisting of the collection of its state
variables, an agent also has a state that represents the
essential variables associated with its current situation. An
agent’s state consists of a set or subset of its attributes.
The state of an agent-based model is the collective states
of all the agents along with the state of the environment.
An agent’s behaviours are conditioned on its state. As
such, the richer the set of an agent’s possible states, the
richer the set of behaviours that an agent can have. In an
agent-based simulation, the state at any time is all the
information needed to move the system from that point
forward.


An agent is social having dynamic interactions with other
agents that inﬂuence its behaviour. Agents have protocols
for interaction with other agents, such as for communica-
tion, movement and contention for space, the capability
to respond to the environment, and others. Agents
have the ability to recognize and distinguish the traits of
other agents.

Agents may also have other useful characteristics:
 An agent may be adaptive, for example, by having rules
or more abstract mechanisms that modify its behaviours.
An agent may have the ability to learn and adapt its
behaviours based on its accumulated experiences. Learn-
ing requires some form of memory. In addition to
adaptation at the individual level, populations of agents
may be adaptive through the process of selection, as
individuals better suited to the environment proportio-
nately increase in numbers.
 An agent may be goal-directed, having goals to achieve
(not necessarily objectives to maximize) with respect to its
behaviours. This allows an agent to compare the out-
come of its behaviours relative to its goals and adjust its
responses and behaviours in future interactions.
 Agents may be heterogeneous. Unlike particle simulation
that considers relatively homogeneous particles, such as
idealized gas particles, or molecular dynamics simulations
that model individual molecules and their interactions,
agent simulations often consider the full range of agent
diversity across a population. Agent characteristics and
behaviours may vary in their extent and sophistication,
how much information is considered in the agent’s deci-
sions, the agent’s internal models of the external world,
the agent’s view of the possible reactions of other agents
in response to its actions, and the extent of memory of
past events the agent retains and uses in making its
decisions. Agents may also be endowed with different
amounts of resources or accumulate different levels of
resources as a result of agent interactions, further differen-
tiating agents.

In an
agent-based model, everything associated with an agent
is either an agent attribute or an agent method that operates
on the agent. Agent attributes can be static, not change-
able during the simulation, or dynamic, changeable as the 
simulation progresses. For example, a static attribute is an
agent’s name; a dynamic attribute is an agent’s memory of
past interactions. Agent methods include behaviours, such as
rules or more abstract representations such as neural net-
works, which link the agent’s situation with its action or set
of potential actions. An example is the method that an agent
uses to identify its neighbours.

A theory of agent behaviour for the situations or contexts
the agent encounters in the model is needed to model agent
behaviour. One may begin with a normative model in which
agents attempt to optimize proﬁts, utility, etc, as a starting
point for developing a simpler, more descriptive, but
realistic, heuristic model of behaviour. One may also begin
with a behavioural model if there is available behavioural
theory and empirical data to support the application.

In agent-based modelling applications in which learning
is important, theories of learning by individual agents or
collectives of agents become important. The ﬁeld of machine
learning is another source of learning algorithms for
recognizing patterns in data (such as data mining) through
techniques such as supervised learning, unsupervised learn-
ing, and reinforcement learning (Alpaydỳn, 2004; Bishop,
2007). Genetic algorithms (Goldberg, 1989) and related
techniques such as learning classiﬁer systems (Holland et al,
2000) are also commonly used in agent-based models.

One of the tenets of complex systems and agent-based
modelling is that only local information is available to an
agent. Agent-based systems are decentralized systems. There
is no central authority that either pushes out globally
available information to all agents or controls their beha-
viour in an effort to optimize system performance. Agents
interact with other agents, but not all agents interact directly
with all the other agents all the time, just as in real-world
systems. Agents typically interact with a subset of other
agents, termed the agent’s neighbours. Local information is
obtained from interactions with an agent’s neighbours (not
any agent or all agents) and from its localized environment
(not from any part of the entire environment). Generally, an
agent’s set of neighbours changes rapidly as a simulation
proceeds and agents move through space.

In the
geographic information system (GIS) topology, agents move
from patch to patch over a realistic geo-spatial landscape
(Figure 3d).

2.5. Agent environment
Agents interact with their environment and with other
agents. The environment may simply be used to provide
information on the spatial location of an agent relative to 
other agents or it may provide a rich set of geographic
information, as in a GIS. An agent’s location, included
as a dynamic attribute, is sometimes needed to track
agents as they move across a landscape, contend for space,
acquire resources, and encounter other situations. Complex
environmental models can be used to model the agents’
environment.


3.2. Applications overview

In ecology, agent-based modelling is used to model diverse
populations of individuals and their interactions. Mock and
Testa (2007) develop an agent-based model of predator-prey
relationships between transient killer whales and threatened
marine mammal species (sea lions and sea otters) in Alaska.



4. Methods for agent-based modelling
4.1. Agent model design
When developing an agent-based model, it is useful to ask a
series of questions, the answers to which will lead to an
initial model design:
1. What speciﬁc problem should be solved by the model?
What speciﬁc questions should the model answer? What
value-added would agent-based modelling bring to the
problem that other modelling approaches cannot bring?
2. What should the agents be in the model? Who are the
decision makers in the system? What are the entities that
have behaviours? What data on agents are simply
descriptive (static attributes)? What agent attributes
would be calculated endogenously by the model and
updated in the agents (dynamic attributes)?
3. What is the agents’ environment? How do the agents
interact with the environment? Is an agent’s mobility
through space an important consideration?
4. What agent behaviours are of interest? What decisions do
the agents make? What behaviours are being acted upon?
What actions are being taken by the agents?
5. How do the agents interact with each other? With the
environment? How expansive or focused are agent
interactions?
6. Where might the data come from, especially on agent
behaviours, for such a model?
7. How might you validate the model, especially the agent
behaviours?
Answering these questions is an essential part of the
agent-based model design process. There are a variety of
approaches to designing and implementing agent-based
models. North and Macal (2007) discuss both design metho-
dologies and selected implementation environments in
depth. Marsh and Hill (2008) offer an initial methodology
for deﬁning agent behaviours in an application for
unmanned autonomous vehicles. Overall, bottom-up, highly
iterative design methodologies seem to be the most effective
for practical model development.

