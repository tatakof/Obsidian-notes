Making a principled decision between a set of actions, $A$, is straight forward if each possible action is assigned an *utility* [[math_concepts#Utility]]
$$
\begin{aligned}
U : A \rightarrow \mathbb{R}^+ \\ 
a \mapsto U(x)

\end{aligned}
$$
because then we can simply select the action with the highest utility
$$
a^* = \underset{a \in A}{argmax\ U(a)}

$$
m' this means, "return the action 'a' from the set of actions A that gives the highest value U(a)". Remember that *argmax* means "return the argument that maximizes the function" whereas *max* means "find the argument that maximizes the function but return the function value, not the argument"
'

The big problem is assigning an utility function to each action. And even the most rigorous utility assignments will depend on circumstances we do not know with perfect certainty, and thus we must rely on inferences to inform those circumstances and motivate effective decision making. 

