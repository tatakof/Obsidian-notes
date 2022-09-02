### Gradient descent

Gradient: Computing the gradients of the loss with respect to all model parameters. this is an approximation of how the parameters need to change in order to minimize the loss function.

The gradients tell us how much we have to change each weight to make our model better. It is essentially a measure of how the loss function changes with changes of the weights of the model (the derivative).



Gradient descent: Taking a step in the directions opposite to the gradients to make the model parameters a little bit better.

... the *gradient*, which measures for each weight, how changing that weight would change the loss




... As we mentioned, we use calculus as a performance optimization; it allows us to more quickly calculate whether our loss will go up or down when we adjust our parameters up or down. In other words, the gradients will tell us how much we have to change each weight to make our model better.

You may remember from your high school calculus class that the *derivative* of a function tells you how much a change in its parameters will change its result.

The key point about a derivative is this: for any function, such as the quadratic function we saw in the previous section, we can calculate its derivative. The derivative is another function. It calculates the change, rather than the value. For instance, the derivative of the quadratic function at the value 3 tells us how rapidly the function changes at the value 3. More specifically, you may recall that gradient is defined as *rise/run*, that is, the change in the value of the function, divided by the change in the value of the parameter. When we know how our function will change, then we know what we need to do to make it smaller. This is the key to machine learning: having a way to change the parameters of a function to make it smaller. Calculus provides us with a computational shortcut, the derivative, which lets us directly calculate the gradients of our functions.



One important thing to be aware of is that our function has lots of weights that we need to adjust, so when we calculate the derivative we won't get back one number, but lots of them—a gradient for every weight. But there is nothing mathematically tricky here; you can calculate the derivative with respect to one weight, and treat all the other ones as constant, then repeat that for each other weight. This is how all of the gradients are calculated, for every weight.

We mentioned just now that you won't have to calculate any gradients yourself. How can that be? Amazingly enough, PyTorch is able to automatically compute the derivative of nearly any function! What's more, it does it very fast. Most of the time, it will be at least as fast as any derivative function that you can create by hand

> a: This (m'Pytorch') API might throw you off if you're coming from math or physics. In those contexts the "gradient" of a function is just another function (i.e., its derivative), so you might expect gradient-related APIs to give you a new function. But in deep learning, "gradients" usually means the _value_ of a function's derivative at a particular argument value. The PyTorch API also puts the focus on the argument, not the function you're actually computing the gradients of. It may feel backwards at first, but it's just a different perspective.


The gradients only tell us the slope of our function, they don't actually tell us exactly how far to adjust the parameters. But it gives us some idea of how far; if the slope is very large, then that may suggest that we have more adjustments to do, whereas if the slope is very small, that may suggest that we are close to the optimal value.





to calculate the gradients we do call `backward` on the `loss`. (that means doing backpropagation on the loss??) 




As we've seen, we need gradients in order to improve our model using SGD, and in order to calculate gradients we need some *loss function* that represents how good our model is. That is because the gradients are a measure of how that loss function changes with small tweaks to the weights.






### Stochastic Gradient Descent

The difference is that you do it on the whole batch??
see lecture of fastai course on chapter 4 for correct answer. 



SGD, or stochastic gradient descent, is an optimization algorithm. Specifically, SGD is an algorithm that will update the parameters of a model in order to minimize a given loss function that was evaluated on the predictions and target. The key idea behind SGD (and many optimization algorithms, for that matter) is that the gradient of the loss function provides an indication of how that loss function changes in the parameter space, which we can use to determine how best to update the parameters in order to minimize the loss function. This is what SGD does.

- Why does SGD use mini-batches?
We need to calculate our loss function (and our gradient) on one or more data points. We cannot calculate on the whole datasets due to compute limitations and time constraints. If we iterated through each data point, however, the gradient will be unstable and imprecise, and is not suitable for training. As a compromise, we calculate the average loss for a small subset of the dataset at a time. This subset is called a mini-batch. Using mini-batches are also more computationally efficient than single items on a GPU.


- What are the seven steps in SGD for machine learning?
Initialize the parameters – Random values often work best.

Calculate the predictions – This is done on the training set, one mini-batch at a time.

Calculate the loss – The average loss over the minibatch is calculated

Calculate the gradients – this is an approximation of how the parameters need to change in order to minimize the loss function

Step the weights – update the parameters based on the calculated weights

Repeat the process

Stop – In practice, this is either based on time constraints or usually based on when the training/validation losses and metrics stop improving.




Basic steps of SGD in python

```python
for x,y in dl:

pred = model(x)

loss = loss_func(pred, y)

loss.backward()

parameters -= parameters.grad * lr
```

