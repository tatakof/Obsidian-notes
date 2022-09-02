# Deep Learning Metrics
## Intro
Since we are specializing a given architecture to solve our particular task by training (or learning), which is the process of finding the set of parameters of our architecture that best solve our task, we need a way to determine how well a given set of parameters solves that task. 
Once we have our architecture with a given set of parameters (either random or set by training), we have a *model* (Thus a model is a combination of n architecture with a given set of parameters). 
In order to check how well our model is performing on our task, that is, how well it is predicting, we need to define a way to measure how well the prediction is. For that we define a metric (i.e. a standard of measurement) that tells us how well our model is making a prediction. We need to define a "loss function" [[Math Functions#Deep Learning#Loss Function]], which determines how we score a prediction as good or bad. 


## What's a Metric?

First of all, a metric is a function, and we have to choose which function to use.  
This function measures how well the model is making a predictions (and evaluated on the validation set). 
When training a DL model, the chosen metric will be printed at the end of each epoch [[fai_jargon]] 
**To be continued**


UNPROCESSED
What is a metric? A _metric_ is a function that measures the quality of the model's predictions using the validation set, and will be printed at the end of each _epoch_. In this case, we're using `error_rate`, which is a function provided by fastai that does just what it says: tells you what percentage of images in the validation set are being classified incorrectly. Another common metric for classification is `accuracy` (which is just `1.0 - error_rate`). fastai provides many more, which will be discussed throughout this book.
 
The concept of a metric may remind you of loss, but there is an important distinction. The entire purpose of loss is to define a "measure of performance" that the training system can use to update weights automatically. In other words, a good choice for loss is a choice that is easy for stochastic gradient descent to use. But a metric is defined for human consumption, so a good metric is one that is easy for you to understand, and that hews as closely as possible to what you want the model to do. At times, you might decide that the loss function is a suitable metric, but that is not necessarily the case. 
END UNPROCESSED





Recall that a metric is a number that is calculated based on the predictions of our model, and the correct labels in our dataset, in order to tell us how good our model is. For instance, we could use either of the functions we saw in the previous section, mean squared error, or mean absolute error, and take the average of them over the whole dataset. However, neither of these are numbers that are very understandable to most people; in practice, we normally use *accuracy* as the metric for classification models.

As we've discussed, we want to calculate our metric over a *validation set*. This is so that we don't inadvertently overfit—that is, train a model to work well only on our training data.





- Are metrics generally calculated using the training set, or the validation set? Why?
Metrics are generally calculated on a validation set. As the validation set is unseen data for the model, evaluating the metrics on the validation set is better in order to determine if there is any overfitting and how well the model might generalize if given similar data.




### L1 and L2 Norms

- Take the mean of the *absolute value* of differences (absolute value is the function that replaces negative values with positive values). This is called the *mean absolute difference* or *L1 norm*
- Take the mean of the *square* of differences (which makes everything positive) and then take the *square root* (which undoes the squaring). This is called the *root mean squared error* (RMSE) or *L2 norm*.



Root mean square error (RMSE), also called the L2 norm, and mean absolute difference (MAE), also called the L1 norm, are two commonly used methods of measuring “distance”. Simple differences do not work because some difference are positive and others are negative, canceling each other out. Therefore, a function that focuses on the magnitudes of the differences is needed to properly measure distances. The simplest would be to add the absolute values of the differences, which is what MAE is. RMSE takes the mean of the square (makes everything positive) and then takes the square root (undoes squaring).



#### Difference between L1 and L2 norms
> S: Intuitively, the difference between L1 norm and mean squared error (MSE) is that the latter will penalize bigger mistakes more heavily than the former (and be more lenient with small mistakes).





### The problem with metrics in AI
[[dl_the-problem-with-metrics]]







