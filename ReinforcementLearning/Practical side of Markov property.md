But why do you care about this? Well, in the environments we’ve explored so far it’s not that
obvious, and it’s not that important. But because most RL (and DRL) agents are designed to
take advantage of the Markov assumption, you must make sure you feed your agent the nec-
essary variables to make it hold as tightly as possible (completely keeping the Markov assump-
tion is impractical, perhaps impossible).
For example, if you’re designing an agent to learn to land a spacecraft, the agent must
receive all variables that indicate velocities along with its locations. Locations alone are not
sufficient to land a spacecraft safely, and because you must assume the agent is memoryless,
you need to feed the agent more information than just its x, y, z coordinates away from the
landing pad.
But, you probably know that acceleration is to velocity what velocity is to position: the
derivative. You probably also know that you can keep taking derivatives beyond acceleration.
To make the MDP completely Markovian, how deep do you have to go? This is more of an art
than a science: the more variables you add, the longer it takes to train an agent, but the fewer
variables, the higher the chance the information fed to the agent is not sufficient, and the
harder it is to learn anything useful. For the spacecraft example, often locations and velocities
are adequate, and for grid-world environments, only the state id location of the agent is
sufficient.