## FOUNDATIONS OF PROBABILITY THEORY

### Power set: 
the collection of all sets in a space X. The power set is massive; it contains the empty set, the entire space, all of the atomic sets, and more. 




### sigma-Algebra (over the space X): 
A well-behaved collection of subsets of X. A restricted collection of sets satisfying some closure properties, denoted with calligraphic font X. The reason we want a sigma algebra is that when dealing with sets we often want to consider not the enitre power set but rather a restriction of the power set that avoids any pathological sets (that feature some very odd properties) that might be hiding. We have to be careful to apply this restriction in a self-consistent manner. In particular, we want our restriction to be closed under the three natural set operations (intersetion, union and complement) so that we don't have to worry about straying outside of our carefully chosen restriction. E.g.,  if the sets A1 and A2 are in our restriction, we want their complement, union and intersection to be in our restriction as well.  
A given space with typically admit many sigma=algebras, although only a few will be of practical interest. 
An important benefit of these closure properties is that they ensure that any non-constructible sets that may be lurking within the power set dont persist into a sigma algebra. Consequently indentifying any sigma algebra removes many of the pathological behaviours that arise in uncountably-large spaces. 
Conveniently, many spaces are equipped with structures that define natural sigma algebras. In particular, all of the spaces that we typically deal with in practical problems, such as the integers and the real numbers, have natural sigma-algebras. Consequently, in practice we don't have to spend any time worrying about explicitly constructing  a sigma-algebra, and the technical need to restrict the power set to a sigma algebra has little impact on the practical use of sets. That said, because avoiding the pathologies of non-constructible sets is critical to a mathematically well-defined probability theory, sigma algebras will be a common occurance. 

### Functions
A function is a relation that associates elements in one space to elements in another space. 
A function also induces a mapping from sets in the input space, X, to sets in the output space, Y, by applying the function to each individual element in the input set. This induced map is also known as a pushforward map over sets. 
At the smae time we can also map sets form the output space, Y, to sets in the input space, X, by considering all of the points that map into a given set. This induced map is also known as a pullback map over sets. 
These induced maps will, in general, be between the power sets of the two spaces, but they need not respect any restriction of the power sets that we might be considering, in particular a choice sigma-algebras on the input and output spaces. When dealing with sigma algebras then, we often want to limit our consideration to only those special functions that induce maps between the sigm aalgebras themselves. 

### Mathematical logistics. 
Once the philosophy has been stripped aways, prob theory is simply the study of an object, a probability distribution that assigns values to sets, and the transformations of that object. To be fair this isn't particularly surprising as most of pure mathematics ultimately reduces to studying objects and their transformations. 

### Probability Distributions. 
From an abstract mathematical perspective, probability is surprisingly boring. Probability is simply a positive, conserved quantity that we want to distribute across a given space - in particular it does not necessarily refer to anything inherently random or uncertain. If we rescale this distribution in terms of the relative proportions of the total amount the regardless of the nature of this conserved quantity we can treat it as unit-less with total amounting to 1. 
A probability distribution defines a mathematically self-consistent allocation of this conserved quantity across X. If A is a subset of X then we write P_pi[A] as the probability assigned to A by the probability distribution pi. 
This allocation should be exhaustive such that all of it is distributed into X. In other words we require that the probability assigned to the full space is always the total probability available, P_pi[X] = 1
Moreover, any distribution of probability should be globally consistent over any disjoint decomposition of the total space. 
In particular, we can derive global consistency of probability distribution by recursively applying local consistency. 
More formally we want the allocation of probability to any collection of disjoint sets to be the same as the allocation to the union of those sets, so that no matter how we decompose the space X, or any subsets of X, we don't lose any probability.

Consistency over any finite collection of sets is known as finite additivity and this would be sufficient if there were only a finity number of subsets in X. Finite additivity, however, is insufficient for distributing probability across spaces which feature a countably infinite number of subsets. In particular consider computing the probability assigned to a circle using only rectangles, which is how distributions across the real numbers are more formally derived. No finite number of disjoint rectangles will exactly cover the circle and hence yield the desired probability, but the limit of a countably infinite number of them will. 

Consequently in general we need our probability distributions to be countably additive across any disjoint sets. (inifinite sum)

This sounds well and good, but it turns out that we cannot construct probability distributions that satisfy any kind of additivity for all subsets of every space. The problem? those non-constructible sets. It turns out that when a space features non constructible subsets we can combine a finite number of the, in a certain way, to achieve sub-additivity or super-additivity. In other words, theres no way that we can engineer a self-consistent distribution of probability across non constructible sets. Fortunately this pathological begavior isn't terminal because we already know how to avoind non-constructible sets in practice. All we have to do is limit our probability distributions to any well-defined sigma-algebra, calligraphic_X. 

This minimal properties needed to achieve the probability distribution behaviour that we're after are formalized in Kolmogorov's axioms:

- A probability distribution pi on a space X with sigma algebra calligaphic_X is a mapping from calligraphic_X to the real numbers [0, 1]. 
- This mapping defines a lossless allocation, P_pi [X] = 1
- This mapping defines a consistent allocation for any collection of disjoint sets in calligraphic_X. 

The more familiar rules of probability theory can all be derived from these axioms.

These rules can be used to construct explicit probability distributions when the sigma-algebra is small enough. 

A probability distribution defined by Kolmogorov's axioms is completely specified by the probability triplet (X, calligraphic_X, pi) whici is often denoted more compactly as x ~ pi. Here the point x E X simply denotes the space X, pi denotes the probability distribuytion, and a valid sigma-algebra is just assumed. 
Care must be taken to no t over interpret this notation - in particular it says nothing about individual points x E X but rather denotes a probability distribution over all sets in the assumed sigma-algebra. 



### Measureable Transformations. 
 Once we have defined a probability distribution on a space, X, and a well-behaved collection of subsets, $\mathcal{X}$, we can then consider how the probability distribution transforms when X transforms. In particular, let f : X -> Y be a transformation from X to another space Y. Can this transformation also transform our probability distribution on X onto a probability distribution on Y, and if so under what conditions?
...
In other words, if f is measureable then a self-consistent allocation of probability over X induces a self-consistent allocation of probability over Y. 


### Projections. 
Measurable transformations can be used to project a probability distribution over a space onto a probability distribution over a lower-dimensional subspace. 
Let $\varpi : X \rightarrow Y$  be a projection operator that maps points in a space X to points in the subspace $Y \subset X$. It turns out that in this case a sigma-algebra on X naturally defines a sigma algebra on Y and the projection operator is measurable with respect to this choice. Consequently any joint probability distribution on X will transform into a unique marginal probability distribution on Y. (marginal is lower dimensional than joint ???). More commonly we say that we marginalize out the complementary subspace, $Y^C$ . 

Marginalization is a bit more straightforward when we are dealing with a product space, $X \times Y$ , which is naturally equipped with the *component projection operators* $\varpi_{X} : X \times Y$ and $\varpi_{Y} : X \times Y$. In this case by pushing a distribution over ($X \times Y, \mathcal{X} \times \mathcal{Y}$ ) forwards along $\varpi_{X}$ we marginalize *out* Y to give a probability distribution over ($X, \mathcal{X}$ ). At the same time by pushing that same distribution forwards along the $\varpi_{Y}$ we can marginalize out X to give a probability distribution over ($Y, \mathcal{Y}$). 


Consider, for example, the three dimensiona space R3 where the coodinate functions serve as projection operators onto the trhee axes X Y Z. Marginalizing out X transforms a probability distribution over X x Y x Z to give a probability distribution over the two dimensional space Y x Z = R2. Marginalizing out Y then givens a probability distribution over the one-dimensiona space, Z = R. 

### Reparametrizations. 
Another important class of measurable functions are those one-to-one maps for which f(A) $\in$ $\mathcal{Y}$  for any $A \in \mathcal{X}$  in addition to $f_{-1} (B) \in \mathcal{X}$ for any $B \in \mathcal{Y}$. In this case f not only transforms a probability distribution on X into a probability distribution on Y but also transforms a probability distribution on Y intro a probabiltiy distribution on X. Moreover, transforming a distribution on X to one on Y and back perfectly restores the original distribution - **unlike projections these reparameterizations preserve all information encoded in a  probability distribution**. 
In this case ($X, \mathcal{X}, \pi$ ) and ($Y, \mathcal{Y}, \pi$) are really just two different manifestations, or *parametrizations*, of the same abstract probability system. The two parameterizations, for example, might correspond to different choices of coordinate system, different choices of units, or different choices of language dialect capable of the same descriptions. The reparameterizations the translate from one wequivalent manifestation to anohter. 

For discrete spaces all reparameterizations can be reduced to permutations that simply rearrange the individual elements of the space. This simple inuition, however, doesn't carry over to continuous spaces for which reparameterizations can be significantly more subtle. 

## Great expectations. 
Conveniently the distribution of probability acrros a space also provides a supplementary function: it allows us to summarize hjow functions of the form f: X -> R behave. 
Without probability the only way that we can summarize the behavior of such a function is through topological information such as minima and maxima. The introduction of a probability distribution, however, allows us to *average* the behavior of a function across it's input domain.

If A1 and A2 are two sets and $P_\pi [A] > P_\pi [A2]$ then the behavoir of f within A1 is more relevant to an average. 

Expectation values, $E_\pi [f]$ (is this the expectation of the function f using pi as the function that assigns the probability to each interval?) , reduce a function to a single real number by weighting the function output at every point by the probability distributed around that point.


## 3.2 Useful expectations

Expectation values serve two powerful purposes. They can be used to summarize the beahior of a function f: X -> R in the context of a given probability distribution. We can also invert this perspective, however, and use the expectation value of certain functions to characterize the given probability distribution itself. **In this section i'll introduce certain functions whose expectations are particularly useful in interrogating the properties of probability distributions defined on certain spaces. **

First, however, a word of caution. **The structure of these special functions, and hence the interpretation of these expectation values, is specific to the context of a given space and will not, in general, push forward along a transformation to another space. In particular, the interpretation is unique to a given parameterization and will change under reparameterizations even though the abstract probabilistic system does not. **

**If desired we can preserve the value of an expectation value if we first push the special function forward along the transformation and only then perform an expectation. Expectation and transformation do not, in general, commute!**

### 3.2.1 This distribution and I are having a moment. 

When our target space is a subset of the real line, X $\subseteq$ R, there is a natural embedding of X into R,   

$$
\iota : X \rightarrow R 
$$
$$
x \rightarrow x
$$

(in mathematics, the inclusion map of one space into another is sometimes denoted by the lower case iota.)


If our target space is itself the real line then the identity function serves as an appropriate embedding. 
$$
\iota : R \rightarrow R
$$





(remember that in 3.2: "In this section ill introduce certain functions whose expectations are particularly usefuil in interrogatin the properties of probability distributions defined on certain spaces". Thus this identity function maybe is one of those functions whose expectations are particularly usefull in interrogatin the properties of probability distributions defined on certain spaces. )


**The expectation value of this embedding function (the identity function), and simple transformations of the embedding function, are extremely useful in characterizing certain properties of probability distributions. *Moments* are expectations of powers of the embedding function,**

$$
m_{\pi ,n} \equiv E_{\pi} [\iota^n]
$$ 
Central moments center the embedding function around the  first moment, 
$$
\mathbb{c}_{\pi, n} 
\equiv 
\mathbb{E}_{\pi} [ (\iota - \mathbb{m}_{\pi, 1})^{n} ].
$$

The mean of a probability distribution is the corresponding first moment, 

$$
\mathbb{m}_{\pi} = \mathbb{m}_{\pi, 1} = \mathbb{E}_{\pi} [ \iota ],
$$


(m_pi equals the mean of the probability distribution pi?)


 which quantifies a sense of *where* in the target space the probability distribution is concentrating its allocation. 


At the same time the variance of a probability distribution is the second central moment, 

$$
\mathbb{V}_{\pi} 
= \mathbb{c}_{\pi, 2} 
= \mathbb{E}_{\pi} [ (\iota - \mathbb{m}_{\pi})^{2}],
$$

which quantifies a sense of the *breath* of the probability allocation around the mean. In practice the *standard deviation*, 

$$
\mathbb{s}_{\pi} = \sqrt{ \mathbb{V}_{\pi} }
$$

is often more interpretable than the variance. 

Higher-order central moments go on to quantify more intricate properties of a given probability distribution. for example, the thrid central moment quantifies how *asymetrically* probability is distributed around the mean. 

While we can always define expectation values of a given function f : X -> R, a probability distribution will not always have well-defined moments. On one hand the corresponding expectation values may be infinite or simply ill-posed. On the other hand the embedding function itself may no be well-defined. 

For example, if our space is a subset of the real numbers in more than one dimension, $X \subseteq \mathbb{R}^{N}, \, N > 1$, then there is no unique embedding function and hence no well-defined moments. We can, however, define component moments as expectations of the coordinate functions, $\hat{x}_{n}: X \rightarrow \mathbb{R}$, that project a point x E X onto each of the component real lines. These component means and variances then provide some quantification of how probability is allocated along each axis. 


Unfortunately it's also common for the mean of a function to refer to its expectation value,
$$
\mathbb{m}_{\pi} [f] = \mathbb{E}_{\pi} [ f ].
$$

and the variance of a function to refer to the expectation

$$
\mathbb{V}_{\pi} [f] = \mathbb{E}_{\pi} [ (f - \mathbb{E}_{\pi}[f])^{2}]
$$

(don't really get why this isn't propper. Maybe you can't get the mean of a function that is not a prob distribution but you can always get the expectation?)

In order to avoid confusion with the mean and variance of a probability distribution, I will always specify the argument [f] when these alternative notations are being used.

**Finally, keep in mind that moments are defined within the context of a particular parameterization!. Reparameterizing to another space introduces a *different* embedding function which defines *different* moments that quantify *different* properties of the abstract probability system.** 


### 3.2.2 Cumulative Distribution Functions and Quantiles

The target space is *ordered* when we can **uniquely** define an ordering of each point. For example the one-dimensional real line is ordered because each point is placed above or below all others, but the two-dimensional real plane is not ordered because, for example, there is *no unique way* to define whether the point (1, 0) is greater than or less than the point (0, 1). Similarly, there's no self-consistent way to order a circle.

When the target space is ordered we can define *one-sided* interval sets
$$
I(x) = \left\{ x \in X \mid x_{\mathrm{min}} \le x \right\}
$$

where $x_{min}$ is the *unique* smallest value in X, as well as *two-sided interval sets*

$$
I(x_{1}, x_{2}) = \left\{ x \in X \mid x_{1} < x \le x_{2} \right\}
$$

The *cumulative distribution function* is constructed from the expectation values of all of the indicator functions corresponding to one-sided interval sets,
$$
\Pi(x) 
= \mathbb{E}_{\pi} [ \mathbb{I}_{I(x)} ]
= \mathbb{P}_{\pi} [ I(x) ].
$$
Cumulative distribution functions not only give the probability of one-sided intervals, the difference between cumulative distribution functions also gives the probability of two-sided intervals. 

EQs
EQs

$$
\begin{align*}
\mathbb{P}_{\pi} [ I(x_{1}, x_{2}) ] 
&=
\mathbb{P}_{\pi} [ I(x_{2}) ] - \mathbb{P}_{\pi} [ I(x_{1}) ]
\\
&=
\Pi(x_{2}) - \Pi(x_{1}).
\end{align*}
$$


*Quantiles* are inverses of the cumulative distribution function for a gien target probability,
$$
x_{p} = \Pi^{-1} (p).
$$

More descriptively, a p-quantile is the point in the target space where we've accumulated p probability. The most common quantile is x_{0.5}, or the median, which quantifies the point in the target space that splits the total probability distribution below and above. This quantifies a different sense of where a porbability distribution concentrates other than the mean. *Tail quantiles*, such as x_0.05 and x_0.95, quantify a different sense of the breath of a probability distribution than the variance. 

**Because a reparameterization can arbitratily reorder a space**, a cumulative distribution function is defined only within the context of a given parameterization. As with moments, quantiles in different parameterizations isolate different properties of the abstract probability system!. 

### 3.2.3 Histograms
a histogram is the collection of probabilities over a sequence of disjoint intervals, $\{B_1, ..., B_N\}$ 
$$
\left\{ 
\mathbb{P}_{\pi} [ B_{1} ], 
\ldots, 
\mathbb{P}_{\pi} [ B_{N} ] 
\right\},
$$
or, equivalently, the expectation values of the corresponding indicator functions, 


$$
\left\{ 
\mathbb{E}_{\pi} [ \mathbb{I}_{B_{1}} ],
\ldots,
\mathbb{E}_{\pi} [ \mathbb{I}_{B_{N}} ]
\right\}.
$$


For one-dimensional, and occasionally two-dimensional target spaces, histograms are useful ways of visualizing the *overall behavior* of a probability distribution. 

## Representing probability distributions with densities

