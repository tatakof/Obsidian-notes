-  explain conditional probability in terms of filtering a data set

"
The *conditional probability of A given B* is the probability that some event A occurs, given that we know some other event B has occurred. $P(X = x | Y = y)$ or shortened to $P(x | y)$.
Often, the probability that we assign to the event $X = x$ changes drastically depending on the knowledge $Y = y$ that we condition on. 

When dealing with probabilities represented by frequencies in a data set, one way to think of conditioning is *filtering* a data set based on the values of one or more variables. 
e.g., if we want to know the prob of a voter is younger than 30, we simply filter the whole dataset to voters younger than 30, count the number of rows, and then divide by the total number of rows. 

This is important for causal questions, as we often want to compare how the probability (or equivalently the risk) of an outcome changes under different filtering, or exposure conditions. e.g., prob of developing lung cancer for smokers vs non smokers. 
"






- explain conditional probability as zooming into a part of a venn diagram and taking that zoomed part as the new "space"

Check brilliant venn diagrams