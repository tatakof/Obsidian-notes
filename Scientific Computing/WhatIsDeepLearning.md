### Machine Learning

Arthur Samuel: "Suppose we arrange for some automatic means of testing the effectiveness of any current weight assignment in terms of actual performance and provide a mechanism for altering the weight assignment so as to maximize the performance. We need not go into the details of such a procedure to see that it could be made entirely automatic and to see that a machine so programmed would "learn" from its experience."


#### Steps of a machine learning model 
  

1. *Initialize* the weights.
1. For each image, use these weights to *predict* whether it appears to be a 3 or a 7.
1. Based on these predictions, calculate how good the model is (its *loss*).
1. Calculate the *gradient*, which measures for each weight, how changing that weight would change the loss
1. *Step* (that is, change) all the weights based on that calculation.
1. Go back to the step 2, and *repeat* the process.
1. Iterate until you decide to *stop* the training process (for instance, because the model is good enough or you don't want to wait any longer).


### Deep learning
FROM https://julialang.org/blog/2019/01/fluxdiffeq/ 

One way to address this is to use machine learning. In a typical machine learning problem, you are given some input xxx and you want to predict an output yyy. This generation of a prediction yyy from xxx is a machine learning model (let's call it MLMLML). During training, we attempt to adjust the parameters of MLMLML so that it generates accurate predictions. We can then use MLMLML for inference (i.e., produce yyys for novel inputs xxx). This is just a nonlinear transformation y=ML(x)y=ML(x)y=ML(x). The reason MLMLML is interesting is because its form is basic but adapts to the data itself. For example, a simple neural network (in design matrix form) with sigmoid activation functions is simply matrix multiplications followed by application of sigmoid functions. Specifically,
ML(x)=σ(W3⋅σ(W2⋅σ(W1⋅x)))ML(x)=\sigma(W_{3}\cdot\sigma(W_{2}\cdot\sigma(W_{1}\cdot x)))ML(x)=σ(W3​⋅σ(W2​⋅σ(W1​⋅x)))

is a three-layer deep neural network, where W=(W1,W2,W3)W=(W_1,W_2,W_3)W=(W1​,W2​,W3​) are learnable parameters. You then choose WWW such that ML(x)=yML(x)=yML(x)=y reasonably fits the function you wanted it to fit. The theory and practice of machine learning confirms that this is a good way to learn nonlinearities. For example, the Universal Approximation Theorem states that, for enough layers or enough parameters (i.e. sufficiently large WiW_{i}Wi​ matrices), ML(x)ML(x)ML(x) can approximate any nonlinear function sufficiently close (subject to common constraints).

So great, this always works! But it has some caveats, the main being that it has to learn everything about the nonlinear transform directly from the data.