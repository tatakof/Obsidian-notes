----------------------------------------------------------
In statistics, one often deals with data sets and prob distribs that are too large to effectively examine each possible combination of values. Instead, we use statistical measures to represent, with some loss of information, meaningful features of the distribution. 

#### What is the expected value
The expected value is... 
minimizes the expected square error??? difference between functions and distributions? for functions is the minimization of the expected error and for distributions is a representation (with information loss) of meaningful features of a distribution?


#### Features of the distributions
##### Expected value (or Mean)
###### Of a Variable
This measure can be uses when variables take on numerical values. 
The expected value of a variable X, denoted E(X), is found by multiplying each possible value of the variable by the probability that the variable will take that value, and then summing the products. 

$$
E(X) = \sum_x xP(X = x)

$$
Note that this equation is the same a a regular mean value, where we sum all the values we have and the divide by the amount of values we have. Because if we have for example the following 8 values (1, 2, 2, 3, 3, 3, 5, 6), and we want to take the mean, we would do: 
$$
(1 + 2 + 2 + 3 + 3 + 3 + 5 + 7) / 8 = 3.25
$$
and if we distribute the 1/8 we have: 

$$

(1/8 + 2/8 + 2/8 + 3/8 + 3/8 + 3/8 + 5/8 + 7/8) = 3.25
$$
(Check the continuity of the explanation)
Since some values occur more than once (i.e. 2) we could shorten the mean calculation by multiplying each number by the frequency...
GRAB A PIECE OF PAPER, GET UR SHIT TOGETHER AND FINISH IT. 


###### of a Function
We can do the same for functions instead of variables [[bayes_glossary#Variable]] pretty much in the same way

$$
E[g(X)] = \sum_x g(x)P(x)


$$




###### Conditional Expected Values

$$
E(Y|X=x) = \sum_y y\ P(Y = y| X = x)

$$

in code (maybe easier to understand), this is only
```
for y in Y
	E(Y|X=x) += y * P(Y = y | X = x) # with x being a constant
```

with $+=$ being the addition assignment operator


Note that $E(Y| X = x)$ means the expected value of the variable Y (that is, all the values $y$ that $Y$ can take, given that the variable $X$ has taken the value $x$). We can also see this in the summation sign $\sum_{y} $ that only contains a $y$, which means that the summation is only done over the different values that Y can take and $x$ is constant. If it said $\sum_x$ $\sum_y$ then we would be doing the summation over all values that X and Y can take (like a nested for loop) 
```
for x in X
	for y in y
		E(Y = x|X = x) += y P(Y = y | X = x)	
```



##### So what is the expected value
E(X) is one way to make a best guess of X's value (imagine X can take many values and u have to guess which one it took this time). Specifically, out of all the guesses $g$ that we can make, the choice $g = E(X)$ minimizes the expected square error $E(g - X)^2$. That is, it minimizes $E(E(X) - X)^2$ I DONT REALLY GET THIS. 

Similarly, $E(Y|X = x)$ represents a best guess of $Y$, given that we observe $X = x$. If $g = E(Y|X = x), then $g$ minimizes the expected square error $E[(g - Y)^2 | X = x)]$ 

The use of expectations as a basis for predictions or "best guesses" hinges to a great extent on an implicit assumption regarding the distribution of X or Y|X = x, namely that such distributions are approximately symmetric. If the distribution of interest is highly skewed, other methods of prediction may be better. In such cases, for example, we might use the median of the distrib of X as our best guess; this estimate minimizes the expected absolute error E(|g - X |)


----------------------------------------------------------
ALL OF THIS CAME FROM PEARLS CAUSAL INFERENCE IN STATISTICS. 

ADD STUFF FROM INFO THEORY BOOK


