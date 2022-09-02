Explain why we should add a test set. 


UNPROCESSED
"
The validation set is also known as the development set (which is used only for evaluation). 

If a model makes an accurate prediction for a data item, that should be because it has learned characteristics of that kind of item, and not because the model has been shaped by actually having seen that particular item. 


splitting off our validation data doesn't actually mean that our model never sees it in traning and thus it's completely untainted by it. The situation is more subtle. This is because in realistic scenarios we rarely build a model just by training its weight parameters once. Instead, we are likely to explore many versions of a model through various modeling choices regarding network architecture, learning rates, data augmentation strategies, and other factors (will be discussed in other chapters). Many of these choices can be described as choices of *hyperparameters*. This word repflects that they are parameters about parameters, since they are higher-level choices that govern the meaning of the weight parameters. 

The problem is that even though the ordinary training process is only looking at predictions on the training data when it learns values for the weight parameters, the same is not true of us. We, as modelers, are evaluating the model by looking at predictions on the validation data when we decide to explore new hyperparameter values. So subsequent versions of the model are, indirectly, shaped by us having seen the validation data. Just as the automatic training process is in danger of overfitting the training data, we are in danger of overfitting the validation data through human trial and error and exploration. 

The solution to this conundrum is to introduce another level of even more highly reserved data, the **test set**. Just as we hold back the validation data from the training process, we must hold back the test set data even from ourselves. It cannot be used to improve the model; it can only be used to evaluate the model at the very end of our efforts. In effect, we define a hierarchy of cuts of our data, based on how fully we want to hide it from training and modeling processes: 
- training data is fully exposed, 
- the validation data is less exposed, 
- and test data is totally hidden. 

This hierarchy parallels the different kinds of modeling and evaluation processes themselves -- the automatic traning process with back propagation, the more manual process of trying different hyper-parameters between training sessions, and the assesment of our final result. 

The test and validation sets should have enough data to ensure that you get a good estimate of your accuracy. If you're creating a cat detector, for instance, you generally want at least 30 cats in your validation set (m'where does this number come from? expertise intuition?). 


Having two levels of "reserved data" --a validation set and a test set, with one level representing data that you are virtually hiding from yourself -- may seem a bit extreme. But the reason it is often necessary is because models ten to gravitate toweard the simplest way to do good predictions (memorization), and we a fallible humans tend to gravitate toward fooling ourselves about how well our models are performing. The discipline of the test set helps us keep ourselves intellectually honest. That doesn't mean we always need a separate test set -- if you have very little data, you may need to just have a validation set -- but generally it's best to use one if at all possible. 


"
END UNPROCESSED




How to properly define a test set: [[Defining test sets]]

