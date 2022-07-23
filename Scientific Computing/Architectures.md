# Deep Learning Architectures 

- **Architecture**: The actual mathematical structure of our model. 

In the academic literature you will see a lot of different architectures, but in practice there are some standard architectures that work most of the time and you should first focus on those. 
ResNet is one example of a standard architecture that works pretty well. (called `resnet<number>`, where the number indicates the amount of layers) (@Fastbook)


- **Same architecture, different amount of layers**: 
Architectures with more layers tend to be used with bigger datasets. In the case of a big dataset, an architecture with more layers tend to give more accurate results. Also, the more layers you have, the longer it takes the model to train. BUT, have in mind that using a big amount of layers on a not so big data-set, overfitting tends to happen (you'll see that you can't train them for as many epochs before the accuracy on the validation set starts getting worse)


An architecture can be seen as a template for how that kind of model works internally and the process of training is what specialize that general architecture for our task. 





UNPROCESSED. 
The architecture only describes a template for a methematical function, it doesn't actually do anything until we provide values for the millions of parameters it contains.  




The basic idea is that by using more linear layers, we can have our model do more computation, and therefore model more complex functions. But there's no point just putting one linear layer directly after another one, because when we multiply things together and then add them up multiple times, that could be replaced by multiplying different things together and adding them up just once! That is to say, a series of any number of linear layers in a row can be replaced with a single linear layer with a different set of parameters.





### More layers
As you will learn, however, the deeper the model gets, the harder it is to optimize the parameters in practice.


We already know that a single nonlinearity with two linear layers is enough to approximate any function. So why would we use deeper models? The reason is performance. With a deeper model (that is, one with more layers) we do not need to use as many parameters; it turns out that we can use smaller matrices with more layers, and get better results than we would get with larger matrices, and few layers.


That means that we can train the model more quickly, and it will take up less memory. In the 1990s researchers were so focused on the universal approximation theorem that very few were experimenting with more than one nonlinearity. This theoretical but not practical foundation held back the field for years. Some researchers, however, did experiment with deep models, and eventually were able to show that these models could perform much better in practice. Eventually, theoretical results were developed which showed why this happens. Today, it is extremely unusual to find anybody using a neural network with just one nonlinearity.



### Meaning of layer nodes
... The key point about this is that `w1` has 30 output activations (which means that `w2` must have 30 input activations, so they match). That means that the first layer can construct 30 different features, each representing some different mix of pixels. You can change that `30` to anything you like, to make the model more or less complex.



## More layers or more nodes?




# Bayesian Modeling Architectures. 