Things I quite don't understand now or know


- In CNNs, how do channels work? in my aar, why am i making images with the 3 timeseries together instead of with 3 separate channels? Does this have something to do with the terms "1D CNN" or "2D CNN", does the dimension mean the amount of channels?


- Relation of layer length (amount of nodes in a given layer) with capacities of a NN. I remember alfredo canziani saying something that the amount of nodes in a layer determines the amount of dimensions of the space after that layer (which is just a transformation). Are there some hard and fast rules in terms of layer length? 

- Amount of layers, is there a hard and fast rule? 



- Why valid loss and training loss can keep going down as the epochs pass but the error rate is the same. 



- Loss vs Probability. 

The _probability_ here is the confidence level, from zero to one, that the model has assigned to its prediction.

And the loss is [[Math Functions#Deep Learning#Loss Function]]


- Fastai what is a Learner object?
It's a fastai's class that group together a `model`, some `dls` and a `loss_func` to handle training

- Why val_loss and train_loss can be numbers bigger than 1



- More layers vs more nodes trade-off (check alfredo canziani and yan lecun lectures, fastbook has some things as well). [[Architectures#More layers or more nodes]]

