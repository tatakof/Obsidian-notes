https://www.fast.ai/2017/11/13/validation-sets/

"_One of the most likely culprits for this disconnect between results in development vs results in production is a poorly chosen validation set (or even worse, no validation set at all). Depending on the nature of your data, choosing a validation set can be the most important step. Although sklearn offers a `train_test_split` method, this method takes a random subset of the data, which is a poor choice for many real-world problems._"



...


The underlying idea is that:

-   the training set is used to train a given model
-   the validation set is used to choose between models (for instance, does a random forest or a neural net work better for your problem? do you want a random forest with 40 trees or 50 trees?)
-   the test set tells you how you’ve done. If you’ve tried out a lot of different models, you may get one that does well on your validation set just by chance, and having a test set helps make sure that is not the case.


A key property of the validation and test sets is that they must be representative of the **new data you will see in the future**. This may sound like an impossible order! By definition, you haven’t seen this data yet. But there are still a few things you know about it.

## When is a random subset not good enough?

### Time series

If your data is a time series, choosing a random subset of the data will be both too easy (you can look at the data both before and after the dates your are trying to predict) and not representative of most business use cases (where you are using historical data to build a model for use in the future). If your data includes the date and you are building a model to use in the future, you will want to choose a continuous section with the latest dates as your validation set (for instance, the last two weeks or last month of the available data).

Suppose you want to split the time series data below into training and validation sets:

![Time series data](https://www.fast.ai/images/timeseries1.png)

A random subset is a poor choice (too easy to fill in the gaps, and not indicative of what you’ll need in production):

![a poor choice for your training set](https://www.fast.ai/images/timeseries2.png)

a poor choice for your training set

Use the earlier data as your training set (and the later data for the validation set):

![a better choice for your training set](https://www.fast.ai/images/timeseries3.png)

a better choice for your training set

Kaggle currently has a competition to [predict the sales in a chain of Ecuadorian grocery stores](https://www.kaggle.com/c/favorita-grocery-sales-forecasting). Kaggle’s “training data” runs from Jan 1 2013 to Aug 15 2017 and the test data spans Aug 16 2017 to Aug 31 2017. A good approach would be to use Aug 1 to Aug 15 2017 as your validation set, and all the earlier data as your training set.

### New people, new boats, new…

You also need to think about what ways the data you will be making predictions for in production may be _qualitatively different_ from the data you have to train your model with.

In the Kaggle [distracted driver competition](https://www.kaggle.com/c/state-farm-distracted-driver-detection), the independent data are pictures of drivers at the wheel of a car, and the dependent variable is a category such as texting, eating, or safely looking ahead. If you were the insurance company building a model from this data, note that you would be most interested in how the model performs on drivers you haven’t seen before (since you would likely have training data only for a small group of people). This is true of the Kaggle competition as well: the test data consists of people that weren’t used in the training set.

If you put one of the above images in your training set and one in the validation set, your model will seem to be performing better than it would on new people. Another perspective is that if you used all the people in training your model, your model may be overfitting to particularities of those specific people, and not just learning the states (texting, eating, etc).

A similar dynamic was at work in the [Kaggle fisheries competition](https://www.kaggle.com/c/the-nature-conservancy-fisheries-monitoring) to identify the species of fish caught by fishing boats in order to reduce illegal fishing of endangered populations. The test set consisted of boats that didn’t appear in the training data. This means that you’d want your validation set to include boats that are not in the training set.

Sometimes it may not be clear how your test data will differ. For instance, for a problem using satellite imagery, you’d need to gather more information on whether the training set just contained certain geographic locations, or if it came from geographically scattered data.

## The dangers of cross-validation

The reason that sklearn doesn’t have a `train_validation_test` split is that it is assumed you will often be using **cross-validation**, in which different subsets of the training set serve as the validation set. For example, for a 3-fold cross validation, the data is divided into 3 sets: A, B, and C. A model is first trained on A and B combined as the training set, and evaluated on the validation set C. Next, a model is trained on A and C combined as the training set, and evaluated on validation set B. And so on, with the model performance from the 3 folds being averaged in the end.

However, the problem with cross-validation is that it is rarely applicable to real world problems, for all the reasons describedin the above sections. Cross-validation only works in the same cases where you can randomly shuffle your data to choose a validation set.



from transformers tutorial by jeremy

...
The _test set_ is yet another dataset that's held out from training. But it's held out from reporting metrics too! The accuracy of your model on the test set is only ever checked after you've completed your entire training process, including trying different models, training methods, data processing, etc.

**You see, as you try all these different things, to see their impact on the metrics on the validation set, you might just accidentally find a few things that entirely coincidentally improve your validation set metrics, but aren't really better in practice. Given enough time and experiments, you'll find lots of these coincidental improvements. That means you're actually over-fitting to your validation set!**

That's why we keep a test set held back
