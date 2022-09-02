# 1. Preliminaries: Statistical and Causal Models

## 1.1 Why study causation
Need to complete

## 1. 2 Simpson's Paradox

Need to complete



## 1.3 Probability and Statistics. 
Statistics generally concerns itself not with absolutes but with likelihoods, thus probability is important to it, as it is to causal statements because most of them are uncertain (and probability is how we express uncertainty).

### 1.3.1 Variables
A variable is any property or descriptor that can take multiple values. A variable can be thought of as a question, to which the value is the answer. 
e.g., "How old is this participant? 38 years old". Age is the variable, 38 is the value. 

The probability that variable X takes values x is written $P(X = x)$ . When the context allows it, this is often shortened to $P(x)$. $P(X = 38)$ is specifically interpreted as the probability that an individual *randomly* selected from the population is aged 38. 

A variable can be either discrete or continuous. 
Discrete variables (also called categorical variables) can take one of a finite or countably infinite set of values in any range. 
Continuous variables can take any one of an infinite set of values on a continuous scale. 

### 1.3.2 Events.

**An event is any assignment of a value or set of values to a variable or set of variables**
e.g., X = 1, the subject is older than 40. 

This definition of "event" runs counter to our everyday notion, which requires that some change occur. For instance we would not refer to a person being a certain age as an event, but we would refer to that person *turning* a year older as en event. Anothewr way of thinking of an event in probability is this: Any declarative statement (a statement that can be true or false) is an event.


### 1.3.3 Conditional Probability. 

The *conditional probability of A given B* is the probability that some event A occurs, given that we know some other event B has occurred. $P(X = x | Y = y)$ or shortened to $P(x | y)$.
Often, the probability that we assign to the event $X = x$ changes drastically depending on the knowledge $Y = y$ that we condition on. 

When dealing with probabilities represented by frequencies in a data set, one way to think of conditioning is *filtering* a data set based on the values of one or more variables. 
e.g., if we want to know the prob of a voter is younger than 30, we simply filter the whole dataset to voters younger than 30, count the number of rows, and then divide by the total number of rows. 

This is important for causal questions, as we often want to compare how the probability (or equivalently the risk) of an outcome changes under different filtering, or exposure conditions. e.g., prob of developing lung cancer for smokers vs non smokers. 

### 1.3.4 Independence. 
Two events are *independent* if the probability of one event remains unaltered with the observation of another. That is, the knowledge that one event has ocurred gives us no additional information about the probability of the other event occuring. Formally, events A and B are said to be independent if 
$$
$P(A|B) = P(A)
$$
If this doesn't hold, then A and B are said to be *dependent*. 
Dependence and independence are symmetric relations. If A is dependent on B, then B is dependent on A, and same with independence. 

Two events A and B are *conditionally independent* given a third event C if

$$
P(A|B, C) = P(A|C)
$$
(note that adding the conditioning on B makes no difference if C is there, thus A and B are conditionally independent given C). 

and $P(B|A, C) = P(B|C)$ 

When dealing with datasets, or prob tables, A and B are conditionally independent given C if A and B are independent in the new data set created by filtering on C.
If A and B are independent in the original unfiltered data set, they are called *marginally independent*. 

Variables, like events, can also be dependent or independent of each other. Two variables X and Y are independent if for every value of x and y that X and Y can take, we have:
$$
P(X = x | Y = y) = P(X = x)
$$
As with dependence or independence of events, variable dependance/independance is also symmetrical. 

Since if for any pair of values of X and Y this equality does not hold (thus there's a case of dependance), then X and Y are said to be *dependent*. Thus in this sense, independence of variables can be understood as a set of independence of events. 


(from other spot in the book) To check if the outcomes of two coins are trulyu independendt, we should count the frequency at which both show up tails, and make sure that it equals the product of the frequencies at which each of the coins shows up tails. 


### 1.3.5 Probability distributions. 
A probability distribution for a variable X is the set of probabilities assigned to each possible value of X. 
The probabilities in a prob distribution must lie between 0 and 1 and sum to 1. An event with prob 0 is impossible, an event with prob 1 is certain. 

The prob distribution of a continuous variable X is represented by a function $f$, called *density function*. When $f$ is is plotted on a coordinate plane, the prob that the value of var X lies between values a and b is the area under the curve between a and b. In calculus, $\int_a^b\ f(x)\ dx$. The are under the entire curve $\int_{-\inf}^\inf f(x) dx$ must be equal to 1. 

The *joint distribution* is the prob distribution of a set of variables.
The joint distribution of a set of variables V is the set of probabilities of each possible combination of variable values in V. 
Probs in a joint distribution must sum to 1. 

### 1.3.6 The Law of Total Probability. 
For any two mutually exclusive events A and B (that is, A and B cannot co-occur), we have: 
$$
P(A or B) = P(A) + P(B)
$$
It follows that for any two events A and B, we have: 
$$
P(A) = P(A, B) + P(A, "\ not B\ ")
$$
($P(A, B)$ is equal to 0 because they are mutually exclusive events). 
The events "A and B" and "A and not B" are mutually exclusive, because B and 'not B' cannot co-occur. 


**Partition**: An exhaustive, mutually exclusive set,, ??such that exactly one of the events must be true?? check 

**Law of Total Probability**: For any set of events $B_1, B_2, ..., B_n$ such that exactly one of the events must be true (a partition), we have: 
$$
P(A) = P(A, B_1) + P(A, B_2) + ... + P(A, B_n)
$$
E.g., If we pull a random card from a standar deck, the prob that the card is a Jack will be equal to the probab that it's a Jack and a Space, plus the prob that it's a Jack and a heart, plus the prob that it's a Jack and a club, plus the prob that it's a Jack and  diamond. 

Other prob rule: 

$$
P(A, B) = P(A|B) P(B)
$$

Division rule 
$$
P(A|B) = P(A, B) / P(B)
$$
this formula is formally regarded as a definition of conditional probabilities and is justified by viewing conditioning as a filtering operation
When we condition on B, we remove from the table all events that conflict with B. The resulting subtable, like the original, represents a prob distribution (thus must sum to 1). Since the probabilities of the subtables rows in the original distribution summed to P(B) by definition (because all the rows that contain B, if u sum them, they must sum to P(B)), we can determine their probabilities in the new distribution by multiplying each by 1/P(B). 




**Marginalizing A over B** : Calculating the probability of an event A by summing up its probabilities over all $B_i$ is called marginalizing over B. And the resulting probability P(A) is called the *marginal probability of A*. 


**Bayes rule**
Using the rule $P(A, B) = P(A|B) P(B)$ and the division rule, together witht he symmetry $P(A, B) = P(B, A)$, we can obtain bayes rule

$$
P(A|B) = P(B|A)P(A)\ / P(B)
$$

Many times we can't asses P(A) directly, but It's easier to find P(A) using a weighted sum of condition probabilities (which is just a decomposition): 
$$
P(A) = P(A|B_1)P(B_1) +\ ...\ + P(A|B_k)P(B_k)
$$
**This law is sometimes called "the law of alternatives" or "extending the conversation"**


The reason is that finding a probability without a context e.g. $P(A)$ is very very hard, whereas probabilities that are tied to specific contexts (i.e., conditional probabilities $P(A|B_K)$)) are easier to find. 
Pearls book has an example on this, I ommited it


### 1.3.7 Using Bayes' Rule. 

In bayes rule, event A is usually referred as the "hypothesis" and event B as the "evidence". 

It's generally easier to asses the probability that a piece of evidence will occur if the hypothesis is correct $P(B|A)$. But it's way harder to figure out the probability of the hypothesis given the evidence P(A|B).  And this last one is the one that we actually are most interested in science or the real world in general: we want to update our belief in some hypothesis, P(A), after some evidence B has ocurred. 
To precisely use Bayes' rule in this manner, we must treat each hypothesis as an event and assign to all hypotheses for a given situation a probability distribution, called a *prior*. 
