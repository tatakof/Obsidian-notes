# Deep Learning

## Loss Function
DEFINE
"A loss function determines how we score a prediction as good or bad" (FastAI 01_)


"The loss is a number that is higher if the model is incorrect (especially if it's also confident of its incorrect answer), or if it's correct, but not confident of its correct answer. In a couple of chapters we'll learn in depth how loss is calculated and used in the training process. For now, `plot_top_losses` shows us the images with the highest loss in our dataset. "

"
Loss is the result of a bad prediction. A **loss** is a number indicating how bad the model's prediction was on a single example.

If the model's prediction is perfect, the loss is zero; otherwise, the loss is greater. The goal of training a model is to find a set of weights and biases that have low loss, on average, across all examples. Higher loss is the worse(bad prediction) for any model.

The loss is calculated on **training** and **validation** and its interpretation is how well the model is doing for these two sets. Unlike accuracy, a loss is not a percentage. It is a sum of the errors made for each example in training or validation sets.

In the following diagrams, there are two graphs representing the losses of two different models, the left graph has a high loss and the right graph has a low loss.
"


"
Usually with every epoch increasing, loss goes lower and accuracy goes higher. But with val_loss and val_acc, many cases can be possible:

1.  val_loss starts increasing, val_acc starts decreasing(means model is cramming values not learning)
    
2.  val_loss starts increasing, val_acc also increases.(could be case of overfitting or diverse probability values in cases softmax is used in output layer)
    
3.  val_loss starts decreasing, val_acc starts increasing(Correct, means model build is learning and working fine)
"(https://stackoverflow.com/questions/51704808/what-is-the-difference-between-loss-accuracy-validation-loss-validation-accur)


"
The lower the **loss,** the better a model (unless the model has over-fitted to the training data). The loss is calculated on **training** and **validation** and its interperation is how well the model is doing for these two sets. Unlike accuracy, loss is not a percentage. It is a summation of the errors made for each example in training or validation sets.

In the case of neural networks, the loss is usually [negative log-likelihood](https://en.wikipedia.org/wiki/Cross_entropy) and [residual sum of squares](https://en.wikipedia.org/wiki/Residual_sum_of_squares) for classification and regression respectively. Then naturally, the main objective in a learning model is to reduce (minimize) the loss function's value with respect to the model's parameters by changing the weight vector values through different optimization methods, such as backpropagation in neural networks.

Loss value implies how well or poorly a certain model behaves after each iteration of optimization. Ideally, one would expect the reduction of loss after each, or several, iteration(s).

The **accuracy** of a model is usually determined after the model parameters are learned and fixed and no learning is taking place. Then the test samples are fed to the model and the number of mistakes (zero-one loss) the model makes are recorded, after comparison to the true targets. Then the percentage of misclassification is calculated.

For example, if the number of test samples is 1000 and model classifies 952 of those correctly, then the model's accuracy is 95.2%.

[![enter image description here](https://i.stack.imgur.com/Vnf0p.png)](https://i.stack.imgur.com/Vnf0p.png)

There are also some subtleties while reducing the loss value. For instance, you may run into the problem of [over-fitting](https://en.wikipedia.org/wiki/Overfitting) in which the model "memorizes" the training examples and becomes kind of ineffective for the test set. Over-fitting also occurs in cases where you do not employ a [regularization](https://en.wikipedia.org/wiki/Regularization_%28mathematics%29), you have a very complex model (the number of free parameters `W` is large) or the number of data points `N` is very low.
"(https://stackoverflow.com/questions/34518656/how-to-interpret-loss-and-accuracy-for-a-machine-learning-model)
