----------------------------------------------------------
FROM PEARLS BOOK CAUSAL INFERENCE IN STATISTICS   

Often, in statistics, we wish to predict the value of one variable Y based on the value of another variable X. Example. We noted earlier that the best prediction of Y based on X is given by the conditional expectation $E[Y|X = x ]$, at least in terms of mean-squared error. But this assumes that we know the conditional expectation, or can compute it, from the joint distribution $P(y, x)$. With *regression*, we make our prediction directly from the data (without the need to know P(y, x)) 
**DNT
Why is is so hard to get P(y,x)? because we need all of the data (instead of a sample) to compute it? is regression the method for a sample but if we had infinite data we would never use regression and just compute $E[Y|X = x]$ from $P(y, x)$ ?

We try to find a formula, usually a linear function, that takes observed values of X as input and gives values of Y as output, such that the square error between the predicted and actual values of Y is minimized, *on average*. 

The least squares regression line is the line for which the sum of the squared vertical distances of the points on the scatter plot from the line (from a line that we are testing if its the best fit, from that regression line on the scatter plot) is minimized. That is, if there are $n$ data points $(x, y)$ on our scatter plot, and for any data point $(x_i, y_i)$, the value $y′_i$  represents the value of the line $y = \alpha + \beta x$ at $x_i$, then the least squares regression line is the one that minimizes the value: 
$$
\sum_i (y_i - y'_i)^2 = \sum_i (y_i - \alpha - \beta x_i)^2 

$$

**DNT, TO READ ON A BETTER DAY**


















----------------------------------------------------------