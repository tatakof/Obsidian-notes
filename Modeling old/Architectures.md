# Deep Learning Architectures 

- **Architecture**: The actual mathematical structure of our model. 

In the academic literature you will see a lot of different architectures, but in practice there are some standard architectures that work most of the time and you should first focus on those. 
ResNet is one example of a standard architecture that works pretty well. (called `resnet<number>`, where the number indicates the amount of layers) (@Fastbook)


- **Same architecture, different amount of layers**: 
Architectures with more layers tend to be used with bigger datasets. In the case of a big dataset, an architecture with more layers tend to give more accurate results. Also, the more layers you have, the longer it takes the model to train. BUT, have in mind that using a big amount of layers on a not so big data-set, overfitting tends to happen (you'll see that you can't train them for as many epochs before the accuracy on the validation set starts getting worse)


An architecture can be seen as a template for how that kind of model works internally and the process of training is what specialize that general architecture for our task. 





UNPROCESSED. 
The architecture only describes a template for a methematical function, it doesn't actually do anything until we provide values for the millions of parameters it contains.  




## More layers or more nodes?




# Bayesian Modeling Architectures. 