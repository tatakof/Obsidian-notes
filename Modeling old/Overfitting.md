# Overfitting in Deep Learning

Overfitting is the case when the model "memorizes" our training data instead of extracting meaninful features that will generalize to other datasets of the same task. What we mean by "memorization" is that in the training process, the model arrives to really specific parameters that can only explain/predict the data that it has seen, losing its ability to generalize to other datasets.
Overfitting can happen if we train our model badly, that is, we don't split our data into training and validation sets, or training, validation and test sets. 
The reason of why we should include a test set if the amount of data allows it is: [[Training, Validation and Test sets]]
By doing this data splitting into sets, we can check if the training generalizes at least to the validation set. 

Models should learn *characteristics* of kinds of items in data, not learn the items themselves (which would end up in memorization of items and overfitting)
 

- Overfitting can be seen when the validation accuracy is getting worse during training. Overfitting can be seen when your accuracy is getting better than your validation accuracy.


- When overfitting **happens**:
	- When you train your model for too long without enough data. 


- When to use **overfitting-avoidance techniques**:
	- Only use them when you have confirmed that overfitting is actually ocurring. Otherwise this could lead to performance loss. 






























# Overfitting in Bayesian modeling. 