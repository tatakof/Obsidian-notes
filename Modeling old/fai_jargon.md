Some jargon is taken from FastAI's book with some "addings" from me. Other jargon have different sources (like ... ) or are written by me.   



### Label 
The data that we're trying to predict, such as "dog" or "cat"




### Architecture
The _template_ of the model that we're trying to fit; the actual mathematical function that we're passing the input data and parameters to





### Model
The combination of the architecture with a particular set of parameters. Also called a "mode"



### Parameters
The values in the model that change what task it can do, and are updated through model training



### Fit 
Update the parameters of the model such that the predictions of the model using the input data match the target labels.




### Train 
A synonym for _fit_. 'm also a synonym for learn?'



### Pre-trained model 
A model that has already been trained, generally using a large dataset, and will be fine-tuned



### Fine-tune 
Update a pretrained model for a different task. 

### Epoch 
One complete pass through the input data

### Loss 
A measure of how good the model is, chosen to drive training via SGD (Stochastic Gradient Descent)

### Metric 
A measurement of how good the model is, using the validation set, chosen for human consumption


### Validation set 
A set of data held out from training, used only for measuring how good the model is

### Training set
The data used for fitting the model; does not include any data from the validation set

### Overfitting 
Training a model in such a way that it _remembers_ specific features of the input data, rather than generalizing well to data not seen during training

### CNN 
Convolutional neural network; a type of neural network that works particularly well for computer vision tasks


- DataLoaders: A fastai class that stores multiple `DataLoader` objects you pass to it, normally a `train` and a `valid`, although it's possible to have as many as you like. The first two are made available as properties.


- Epoch: a complete pass through all training data during model training

