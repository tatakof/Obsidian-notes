## Fine Tuning
We can achieve a higher model performance and faster training by using a pretrained model (practice often called Transfer Learning), which is a model that has been trained on some other data-set. 
Once we have this pre-trained model, we can *fine-tune it* to our task by training the model a little bit more with our data. This process is what is called *Finetuning*. 
'm CHECK usually when we do a fine tuning what we do is remove the last layers of a model and add new ones that we train with our data'.

UNPROCESSED
But why did we use the method calle fine_tune, and not fit? fastai actually does have a method called fit, which does indeed fit a model (ie, look at images in the training set multiple times, each time updating the parameters to make predictions closer and closer to the target labels). But in this case, we've started with a pretrained model, and we don't want to throw away all those capabilities that it already has. As you'll learn in this book, there are some importante tricks to adapt a pretrained model for a new dataset -- a process called fine-tuning. 

when you see a fine_tune method, fastai will use these tricks for you. There are a few parameters you can set (discussed later), but in the default form shown here, it does two steps: 

1- Use one epoch to fit just those parts of the model necessary to get the new random head to work correctly with your dataset. 
2- Use the number of epochs requested when calling the method to fit the entire model, updating the weights of the later layer (especially the head) faster than the earlier layers (which, as we'll see, generally don't require many changed from the pretrained weights). 
END UNPROCESSED

## Transfer learning



ALL UNPROCESSED
'cnn_learner' also has a parameter 'pretrained', which defaults to True.

A model that has weights that have already been trained on some other dataset is called a 'pretrained model'. You should nearly always use a pretrained model, because it means that your model, before you've even shown it any of your data, is already very capable. And, as you'll see, in a deep learning model many of these capabilities are things you'll need, almost regardless of the details of your project. For instance, parts of pretrained models will handle edge, gradient, and color detection, which are needed for many tasks. 

When using a pretrained model, 'cnn_learner' will remove the last layer, since that is always specifically customized to the original training task (ie, ImageNet dataset classification in the case of resnet34), and replace it with one or more new layers with randomized weights, of an appropriate size for the dataset you are working with. This last part of the model is known as the 'head'.

Using pretrained models is the most important method we have to allows us to train more accurate models, more quickly, with less data, and less time and money... The importance of pretrained models is rarely considered in academic papers... Most people you speak to will probably greatly underestimate what you can do in deep learning with few resources, because they probably won't deeply understand how to use pretrained models. 

Using a pretrained model for a tast different to what it was originally trained for is known as *transfer learning*. Unfortunately, because transfer learning is so under-studied, few domains have pretrained models available. **For isntance, there are currently few pretrained models available in medicine, making transfer learning challenging to use in that domain. In addition, it is not yet well understood how to use transfer learning for tasks such as time series analysis.** 
END UNPROCESSED CHUNK 




This final linear layer ((of a pretrained model)) is unlikely to be of any use for us when we are fine-tuning in a transfer learning setting, because it is specifically designed to classify the categories in the original pretraining dataset. So when we do transfer learning we remove it, throw it away, and replace it with a new linear layer with the correct number of outputs for our desired task (in this case, there would be 37 activations).





### Freezing
Our challenge when fine-tuning is to replace the random weights in our added linear layers with weights that correctly achieve our desired task (classifying pet breeds) without breaking the carefully pretrained weights and the other layers. There is actually a very simple trick to allow this to happen: tell the optimizer to only update the weights in those randomly added final layers. Don't change the weights in the rest of the neural network at all. This is called *freezing* those pretrained layers.



### Types of tasks and availability of pretrained models. 
- Image: Lots
- Tabular: no pretrained model available