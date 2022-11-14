
The network that transforms input data into output is not the only thing we need or training. We need to dene our learning objective, which is to have a unction that accepts two arguments—the network's output and the desired output. Its responsibility is to return to us a single number—how close the network's prediction
is from the desired result. This function is called the loss function, and its output is the loss value. Using the loss value, we calculate gradients of network parameters and adjust them to decrease this loss value, which pushes our model to better results in the future. Both the loss function and the method of tweaking a network's
parameters by gradient are so common and exist in so many forms that both of them orm a signicant part o the PyTorch library. Let's start with loss unctions.





Loss: A value that represents how well (or badly) our model is doing.

The loss function will return a value based on the given predictions and targets, where lower values correspond to better model predictions.


when we do SGD, the average loss over the minibatch is calculated


... Based on these predictions, calculate how good the model is (its *loss*) ...



- Loss:: This is what Samuel referred to when he spoke of *testing the effectiveness of any current weight assignment in terms of actual performance*. We need some function that will return a number that is small if the performance of the model is good (the standard approach is to treat a small loss as good, and a large loss as bad, although this is just a convention).



the loss function returns a value based on a prediction and a target



We need to define first what we mean by "best (parameters)." We define this precisely by choosing a *loss function*, which will return a value based on a prediction and a target, where lower values of the function correspond to "better" predictions. For continuous data, it's common to use *mean squared error*:

```python 
def mse(preds, targets): return ((preds-targets)**2).mean().sqrt()
```






So, we need to choose a loss function. The obvious approach would be to use accuracy, which is our metric, as our loss function as well. In this case, we would calculate our prediction for each image, collect these values to calculate an overall accuracy, and then calculate the gradients of each weight with respect to that overall accuracy.

Unfortunately, we have a significant technical problem here. The gradient of a function is its *slope*, or its steepness, which can be defined as *rise over run*—that is, how much the value of the function goes up or down, divided by how much we changed the input. We can write this in mathematically as: `(y_new - y_old) / (x_new - x_old)`. This gives us a good approximation of the gradient when `x_new` is very similar to `x_old`, meaning that their difference is very small. But accuracy only changes at all when a prediction changes from a 3 to a 7, or vice versa. The problem is that a small change in weights from `x_old` to `x_new` isn't likely to cause any prediction to change, so `(y_new - y_old)` will almost always be 0. In other words, the gradient is 0 almost everywhere.(m'and if gradient is 0 we can't step our model?')

A very small change in the value of a weight will often not actually change the accuracy at all. This means it is not useful to use accuracy as a loss function—if we do, most of the time our gradients will actually be 0, and the model will not be able to learn from that number.

> S: In mathematical terms, accuracy (m'every accuracy function? or is there only one?') is a function that is constant almost everywhere (except at the threshold, 0.5), so its derivative is nil almost everywhere (and infinity at the threshold). This then gives gradients that are 0 or infinite, which are useless for updating the model.

Instead, we need a loss function which, when our weights result in slightly better predictions, gives us a slightly better loss. So what does a "slightly better prediction" look like, exactly? Well, in this case, it means that if the correct answer is a 3 the score is a little higher, or if the correct answer is a 7 the score is a little lower.

The loss function receives not the images themselves, but the predictions from the model.

The purpose of the loss function is to measure the difference between predicted values and the true values — that is, the targets (aka labels).


You can see that this function returns a lower number when predictions are more accurate, when accurate predictions are more confident (higher absolute values), and when inaccurate predictions are less confident. In PyTorch, we always assume that a lower value of a loss function is better.


In PyTorch, we always assume that a lower value of a loss function is better.



Remember that _loss_ is whatever function we've decided to use to optimize the parameters of our model. But we haven't actually told fastai what loss function we want to use. So what is it doing? fastai will generally try to select an appropriate loss function based on what kind of data and model you are using. In this case we have image data and a categorical outcome, so fastai will default to using _cross-entropy loss_.



### Types of loss functions used

Sigmod?? see chapter 4 of fastbook. 




#### Cross Entropy loss
_Cross-entropy loss_ is a loss function that is similar to the one we used in the previous chapter, but (as we'll see) has two benefits:

-   It works even when our dependent variable has more than two categories.
-   It results in faster and more reliable training.


When we first take the softmax, and then the log likelihood of that, that combination is called *cross-entropy loss*. In PyTorch, this is available as `nn.CrossEntropyLoss` (which, in practice, actually does `log_softmax` and then `nll_loss`):

> s: An interesting feature about cross-entropy loss appears when we consider its gradient. The gradient of `cross_entropy(a,b)` is just `softmax(a)-b`. Since `softmax(a)` is just the final activation of the model, that means that the gradient is proportional to the difference between the prediction and the target. This is the same as mean squared error in regression (assuming there's no final activation function such as that added by `y_range`), since the gradient of `(a-b)**2` is `2*(a-b)`. Because the gradient is linear, that means we won't see sudden jumps or exponential increases in gradients, which should lead to smoother training of models.






















gradient of cross-entropy loss is proportional to the difference between the activation and the target, so SGD always gets a nicely scaled step for the weights