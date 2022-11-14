Reinforcement learning relies heavily on the concept of state—as input to the policy and
value function, and as both input to and output from the model. Informally, we can
think of the state as a signal conveying to the agent some sense of “how the environment
is” at a particular time. The formal definition of state as we use it here is given by
the framework of Markov decision processes presented in Chapter 3. More generally,
however, we encourage the reader to follow the informal meaning and think of the state
as whatever information is available to the agent about its environment. In e↵ect, we
assume that the state signal is produced by some preprocessing system that is nominally
part of the agent’s environment. We do not address the issues of constructing, changing,
or learning the state signal in this book (other than briefly in Section 17.3). We take this
approach not because we consider state representation to be unimportant, but in order
to focus fully on the decision-making issues. In other words, our concern in this book is
not with designing the state signal, but with deciding what action to take as a function
of whatever state signal is available.

Most of the reinforcement learning methods we consider in this book are structured
around estimating value functions, but it is not strictly necessary to do this to solve
reinforcement learning problems. For example, solution methods such as genetic algo-
rithms, genetic programming, simulated annealing, and other optimization methods never
estimate value functions. These methods apply multiple static policies each interacting
over an extended period of time with a separate instance of the environment. The policies
that obtain the most reward, and random variations of them, are carried over to the
next generation of policies, and the process repeats. We call these evolutionary methods
because their operation is analogous to the way biological evolution produces organisms
with skilled behavior even if they do not learn during their individual lifetimes. If the
space of policies is sufficiently small, or can be structured so that good policies are common or easy to find—or if a lot of time is available for the search—then evolutionary
methods can be e↵ective. In addition, evolutionary methods have advantages on problems
in which the learning agent cannot sense the complete state of its environment.

Our focus is on reinforcement learning methods that learn while interacting with the
environment, which evolutionary methods do not do. Methods able to take advantage
of the details of individual behavioral interactions can be much more efficient than
evolutionary methods in many cases. Evolutionary methods ignore much of the useful
structure of the reinforcement learning problem: they do not use the fact that the policy
they are searching for is a function from states to actions; they do not notice which states
an individual passes through during its lifetime, or which actions it selects. In some cases
this information can be misleading (e.g., when states are misperceived), but more often it
should enable more efficient search. Although evolution and learning share many features
and naturally work together, we do not consider evolutionary methods by themselves to
be especially well suited to reinforcement learning problems and, accordingly, we do not
cover them in this book

