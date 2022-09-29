Some jargon is taken from FastAI's book with some "addings" from me. Other jargon have different sources (like ... ) or are written by me.   



### Label 
The data that we're trying to predict, such as "dog" or "cat"




### Architecture
The _template_ of the model that we're trying to fit; the actual mathematical function that we're passing the input data and parameters to





### Model
The combination of the architecture with a particular set of parameters. Also called a "mode"



### Parameters
The values in the model that change what task it can do, and are updated through model training
Numbers that are randomly initialized, and then optimized (they are the numbers that define the model)

### Activations
Numbers that are calculated (both by linear and nonlinear layers)


### Fit 
Update the parameters of the model such that the predictions of the model using the input data match the target labels.




### Train 
A synonym for _fit_. 'm also a synonym for learn?'



### Pre-trained model 
A model that has already been trained, generally using a large dataset, and will be fine-tuned



### Fine-tune 
Update a pretrained model for a different task. 

### Freezing
Our challenge when fine-tuning is to replace the random weights in our added linear layers with weights that correctly achieve our desired task (classifying pet breeds) without breaking the carefully pretrained weights and the other layers. There is actually a very simple trick to allow this to happen: tell the optimizer to only update the weights in those randomly added final layers. Don't change the weights in the rest of the neural network at all. This is called *freezing* those pretrained layers.


### Epoch 
One complete pass through the input data
An epoch is one complete pass through all of the images in the data

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


### ReLU 
Function that returns 0 for negative numbers and doesn't change positive numbers.

### Mini-batch 
A small group of inputs and labels gathered together in two arrays. A gradient descent step is updated on this batch (rather than a whole epoch).

### Forward pass 
Applying the model to some input and computing the predictions.

### Loss 
A value that represents how well (or badly) our model is doing.

### Gradient 
The derivative of the loss with respect to some parameter of the model.

### Backward pass 
Computing the gradients of the loss with respect to all model parameters.

### Gradient descent 
Taking a step in the directions opposite to the gradients to make the model parameters a little bit better.

### Learning rate 
The size of the step we take when applying SGD to update the parameters of the model.


### Test Time Augmentation (TTA)
jargon: test time augmentation (TTA): During inference or validation, creating multiple versions of each image, using data augmentation, and then taking the average or maximum of the predictions for each augmented version of the image.


### Dot product
jargon: dot product: The mathematical operation of multiplying the elements of two vectors together, and then summing up the result.


### Embedding 
jargon: Embedding: Multiplying by a one-hot-encoded matrix, using the computational shortcut that it can be implemented by simply indexing directly. This is quite a fancy word for a very simple concept. The thing that you multiply the one-hot-encoded matrix by (or, using the computational shortcut, index into directly) is called the _embedding matrix_.


### Token
jargon: token: One element of a list created by the tokenization process. It could be a word, part of a word (a _subword_), or a single character.

### Word Tokenization with fastai

Rather than providing its own tokenizers, fastai instead provides a consistent interface to a range of tokenizers in external libraries. Tokenization is an active field of research, and new and improved tokenizers are coming out all the time, so the defaults that fastai uses change too. However, the API and options shouldn't change too much, since fastai tries to maintain a consistent API even as the underlying technology changes.

### Numericalization
_Numericalization_ is the process of mapping tokens to integers. The steps are basically identical to those necessary to create a `Category` variable, such as the dependent variable of digits in MNIST:

1.  Make a list of all possible levels of that categorical variable (the vocab).
2.  Replace each level with its index in the vocab.