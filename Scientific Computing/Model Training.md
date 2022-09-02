# Deep Learning


## Training concept
Training a model is the process of finding a set of parameters (of a given architecture) that can solve our particular task (i.e., specialize our architecture)



ALL UNPROCESSED
In order to fit a model, we have to provide at least one piece of information: how many times to look at each image (known as number of *epochs*). The number of epochs you select will largely depend on how much time you have available, and how long you find it takes in practice to fit your model. If you select a number that is too small, you can always train for more epochs later. 

In order to fit a model, we have to provide at least one piece of information: how many times to look at each image (known as number of *epochs*). The number of epochs you select will largely depend on how much time you have available, and how long you find it takes in practice to fit your model. If you select a number that is too small, you can always train for more epochs later. 

Fine-tuning: A transfer learning technique where the parameters of a pretrained model are updated by training forfor additional epochs using a different task to that used to pretraining. 

But why did we use the method calle fine_tune, and not fit? fastai actually does have a method called fit, which does indeed fit a model (ie, look at images in the training set multiple times, each time updating the parameters to make predictions closer and closer to the target labels). But in this case, we've started with a pretrained model, and we don't want to throw away all those capabilities that it already has. As you'll learn in this book, there are some importante tricks to adapt a pretrained model for a new dataset -- a process called fine-tuning. 

when you see a fine_tune method, fastai will use these tricks for you. There are a few parameters you can set (discussed later), but in the default form shown here, it does two steps: 

1- Use one epoch to fit just those parts of the model necessary to get the new random head to work correctly with your dataset. 
2- Use the number of epochs requested when calling the method to fit the entire model, updating the weights of the later layer (especially the head) faster than the earlier layers (which, as we'll see, generally don't require many changed from the pretrained weights). 

An epoch is one complete training pass through the dataset. 
The head of a model is the part that is newly added to be specific to the new dataset. 

After calling fit, the results after each epoch are printed, showing the epoch number, the training and validation set losses (the "measure of performance" used for training the model), and any metrics you've requested (error rate, in this case)

Deep learning models are not "black box", there's a vast body of research showing how to deeply inspect deep learnin gmodels and get rich insihts from them.

When we fine-tuned our pretrained model earlier, we adapted what those last layers focus on (flowers, humans, animals) to specialize on the cats versus dogs problem. More generally, we could specialize such a pretrained model on many different tasks. 











# Bayesian Models