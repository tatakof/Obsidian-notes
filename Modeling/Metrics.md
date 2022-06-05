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
























# Bayesian Metrics
