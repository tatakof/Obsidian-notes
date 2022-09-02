fastai_resources[[fai_resources]]
some notes from each chapter. 

# 1
You should only use methods to avoid overfitting after you have confirmed that overfitting is actually ocurring (ie, you have actually observed the validation accuracy getting worse during training). We ogten see practitioners using over-fitting avoidance techniques even when they have enough data that they didn't need to do so, ending up with a model that may be less accurate than what they could have achieved. 


important: Validation Set: When you train a model, you must _always_ have both a training set and a validation set, and must measure the accuracy of your model only on the validation set. If you train for too long, with not enough data, you will see the accuracy of your model start to get worse; this is called _overfitting_. fastai defaults `valid_pct` to `0.2`, so even if you forget, fastai will create a validation set for you!



There are many different architectures in fastai, which we will introduce in this book (as well as discussing how to create your own). Most of the time, however, picking an architecture isn't a very important part of the deep learning process. It's something that academics love to talk about, but in practice it is unlikely to be something you need to spend much time on. There are some standard architectures that work most of the time, and in this case we're using one called _ResNet_ that we'll be talking a lot about during the book; it is both fast and accurate for many datasets and problems.

The `34` in `resnet34` refers to the number of layers in this variant of the architecture (other options are `18`, `50`, `101`, and `152`). Models using architectures with more layers take longer to train, and are more prone to overfitting (i.e. you can't train them for as many epochs before the accuracy on the validation set starts getting worse). On the other hand, when using more data, they can be quite a bit more accurate.

What is a metric? A _metric_ is a function that measures the quality of the model's predictions using the validation set, and will be printed at the end of each _epoch_. In this case, we're using `error_rate`, which is a function provided by fastai that does just what it says: tells you what percentage of images in the validation set are being classified incorrectly. Another common metric for classification is `accuracy` (which is just `1.0 - error_rate`). fastai provides many more, which will be discussed throughout this book.

The concept of a metric may remind you of loss, but there is an important distinction. The entire purpose of loss is to define a "measure of performance" that the training system can use to update weights automatically. In other words, a good choice for loss is a choice that is easy for stochastic gradient descent to use. But a metric is defined for human consumption, so a good metric is one that is easy for you to understand, and that hews as closely as possible to what you want the model to do. At times, you might decide that the loss function is a suitable metric, but that is not necessarily the case. 



'cnn_learner' also has a parameter 'pretrained', which defaults to True.

A model that has weights that have already been trained on some other dataset is called a 'pretrained model'. You should nearly always use a pretrained model, because it means that your model, before you've even shown it any of your data, is already very capable. And, as you'll see, in a deep learning model many of these capabilities are things you'll need, almost regardless of the details of your project. For instance, parts of pretrained models will handle edge, gradient, and color detection, which are needed for many tasks. 

When using a pretrained model, 'cnn_learner' will remove the last layer, since that is always specifically customized to the original training task (ie, ImageNet dataset classification in the case of resnet34), and replace it with one or more new layers with randomized weights, of an appropriate size for the dataset you are working with. This last part of the model is known as the 'head'.

Using pretrained models is the most important method we have to allows us to train more accurate models, more quickly, with less data, and less time and money... The importance of pretrained models is rarely considered in academic papers... Most people you speak to will probably greatly underestimate what you can do in deep learning with few resources, because they probably won't deeply understand how to use pretrained models. 

Using a pretrained model for a tast different to what it was originally trained for is known as *transfer learning*. Unfortunately, because transfer learning is so under-studied, few domains have pretrained models available. **For isntance, there are currently few pretrained models available in medicine, making transfer learning challenging to use in that domain. In addition, it is not yet well understood how to use transfer learning for tasks such as time series analysis.** 

The architecture only describes a template for a methematical function, it doesn't actually do anything until we provide values for the millions of parameters it contains.  

In order to fit a model, we have to provide at least one piece of information: how many times to look at each image (known as number of *epochs*). The number of epochs you select will largely depend on how much time you have available, and how long you find it takes in practice to fit your model. If you select a number that is too small, you can always train for more epochs later. 

Fine-tuning: A transfer learning technique where the parameters of a pretrained model are updated by training forfor additional epochs using a different task to that used to pretraining. 

But why did we use the method calle fine_tune, and not fit? fastai actually does have a method called fit, which does indeed fit a model (ie, look at images in the training set multiple times, each time updating the parameters to make predictions closer and closer to the target labels). But in this case, we've started with a pretrained model, and we don't want to throw away all those capabilities that it already has. As you'll learn in this book, there are some importante tricks to adapt a pretrained model for a new dataset -- a process called fine-tuning. 

when you see a fine_tune method, fastai will use these tricks for you. There are a few parameters you can set (discussed later), but in the default form shown here, it does two steps: 

1- Use one epoch to fit just those parts of the model necessary to get the new random head to work correctly with your dataset. 
2- Use the number of epochs requested when calling the method to fit the entire model, updating the weights of the later layer (especially the head) faster than the earlier layers (which, as we'll see, generally don't require many changed from the pretrained weights). 


An epoch is one complete training pass through the dataset. 
The head of a model is the part that is newly added to be specific to the new dataset. 

After calling fit, the results after each epoch are printed, shjowing the epoch number, the training and validation set losses (the "measure of performance" used for training the model), and any metrics you've requested (error rate, in this case)

Deep learning models are not "black box", there's a vast body of research showing how to deeply inspect deep learnin gmodels and get rich insihts from them.

When we fine-tuned our pretrained model earlier, we adapted what those last layers focus on (flowers, humans, animals) to specialize on the cats versus dogs problem. More generally, we could specialize such a pretrained model on many different tasks. 

# HERE ON NEED TO READ AND PASS TO OTHER NOTES. 

### Image Recognizers can tackle non-image tasks. 

An image recognizer can, as its name suggests, only recognize images. But a lot of things can be represented as images, which means that an image recognizer can learn to complete many tasks. 
For instance, a sound can be converted to a spectrogrgam, which is a chart that shows the amount of each frequency at each time in an audio file. fastai's show_batch clearly shows how each different sound has a quite distinctive spectrogram (see image)

A time series can easily be converted into an image by simply plotting the time series on a graph. However, it is often a good idea to try to represent your data in a way that makes it as easy as possible to pull out the most important components. In a time series, things like seasonality and anomalies are most likely to be of intereset. There are various transformations available for time series data, e.g., Gramian Angular Difference Field, that you can apply to the time series data before passing it to an image classification model. 

(a Gramian Agular Field is an image obtained from a time series, representing some temporal correlation between each time point. Two methods are available: Gramian Anular summation Field and Gramian Angular Difference Field)

... This suggests a good rule of thumb for converting a dataset into an image representation: if the human eye can recognize categories from the images, then a deep learning model should be able to do so too. 

In general, you'll find that a small number of general approaches in deep learning can go a long way, if you're a bit creative in how you represent your data. You shouldn't think of approaches like the ones described here as "hacky workarounds", becasue actually they often beat previously state-of-the-art results. These are the right ways to think about these problem domains. 

### Jargon recap

"

| Term | Meaning

|Label | The data that we're trying to predict, such as "dog" or "cat"

|Architecture | The _template_ of the model that we're trying to fit; the actual mathematical function that we're passing the input data and parameters to

|Model | The combination of the architecture with a particular set of parameters

|Parameters | The values in the model that change what task it can do, and are updated through model training

|Fit | Update the parameters of the model such that the predictions of the model using the input data match the target labels.

|Train | A synonym for _fit_

|Pretrained model | A model that has already been trained, generally using a large dataset, and will be fine-tuned

|Fine-tune | Update a pretrained model for a different task

|Epoch | One complete pass through the input data

|Loss | A measure of how good the model is, chosen to drive training via SGD

|Metric | A measurement of how good the model is, using the validation set, chosen for human consumption

|Validation set | A set of data held out from training, used only for measuring how good the model is

|Training set | The data used for fitting the model; does not include any data from the validation set

|Overfitting | Training a model in such a way that it _remembers_ specific features of the input data, rather than generalizing well to data not seen during training

|CNN | Convolutional neural network; a type of neural network that works particularly well for computer vision tasks

|=====



Machine learning is a discipline where we define a program not by writing it entirely ourselves, but by learning from data. Deep learning is a specialty within machine learning that uses neural networks with multiple layers. Image classification is a representative example (also known as image recognition). We start with labeled data, that is a set of images where we have assigned a label to each image indicating what it represents. Our goal is to produce a program, called a mode, which, given a new image, will make accurate prediction regarding what that new image represents. 

Every model starts with a choice of architecture, a general template for how that kind of model works internally. The process of training (or fitting) the model is the process of finding a set of parameter values (or weights) that specialize that general architecture into a model that works well for our particular kind of data. In order to define how well a model does on a single prediction, w4e need to define a loss function, which determines how we score a prediction as good or bad. 

To make the traning process go faster, we might start with pretrained model -- a model that has already been trained on someone else's data. We can then adapt it to our data by training it a bit more on our data, a process called finetuning. 

When we train a model, a key concern is to ensure that our model eneralizes, that is, that it learns general lessons from our data which also applyu to new items it will encounter, so that it can make good predictions on those items. The rist is that if we traing our model badly, insted of learning general lessons it effectively memorizes what is has already seen, and then it will make poor predictions about new imges. Such a failure is called overfittin. In order to avoid this, we always divide our data into two parts, the traning set and the validation set. We train the model by showing it only the training set and then we evaluate how well the model is doing by seeing how well it performs on items from the validation set. In this way, we check if the lessons the model learns from the traning set are lessons that generalize to the validation set. In order for a person to asses how well the model is doing on the validation set overall, we define a metric. dDuring the training processs, when the model has seen every item in the training set, we call that an epoch. 

All these concecpts apply to machine learning in general. That is, they apply to all sorts of schemes for defining a model by training it with data. What makes deep learning distinctive is a particular class of architectures, those based on neural networks. 




### Deep learning is not just for image classification. 

Segmentation: Creating a model that can recognize the content of every individual pixel in an image. 

...

'learn' is an object that contains a model and data for an image classification model (in this case). 



if you ever have any questions about a fastai method, you should use the function 'doc', passing it the method name: 

doc(learn.predict)

this will make a small window pop up with content

Tabular: Data that is in the form of a table, such as from a spreadsheet, database, or CSV file. A tabular model is a model that tries to predict one colum,n of a table based on information in other columns of the table. 

There is no pretrained model available for the tabular task. In general, pretrained models are not widely available for any tabular modeling tasks, although some organizations have created them for internal use), so we don't use 'fine_tune' in this case. **Instead we use 'fit_one_cicle', the most commonly used method for training fastai models from scratch (i.e., without transfer learning)**

Although we're not actually using a pretrained model (for the same reasons that we didn't for the tabular model), this exmaple shows that fastai lets us use 'fine_tune' anyway in this case (you'll learn how and why this works in <<chapter_pet_breeds>>). Sometimes it's best to experiment with 'fine_tune' versus 'fit_one_cycle' to see which works best for your dataset. 

we can use 'show_results' to view a few examples of input data and model predictions

learn.show_results()

Some of the most useful and important datasets are those that become important academic baselines: that is, datasets that are widely studied by researchers and used to compare algorithmic changes. Some of these become household names, such as MNIST, CIFAR-10, and ImageNet.

fast.ai has spent a lot of time creating cut-down versions of popular datasets that are specially designed to support rapid prototyping and experimentation, and to be easier to learn with. In this book we will often start by using one of the cut-down versions and later scale up to the full-size version (just as we're doing in this chapter!). In fact, this is how the world's top practitioners do their modeling in practice; they do most of their experimentation and prototyping with subsets of their data, and only use the full dataset when they have a good understanding of what they have to do. 

Each of the models we trained showed a traning and validation loss. Agood validation set is one of the most important pieces of the traning process. Let's see why and learn how to create one. 





### Validation sets and test sets. 

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


### Use judgment in defining test sets. 

To properly define a validation and test sets, you should do somethimg more than randomly grab a fraction of your original dataset, because a key property of the validation and test sets is that they must be representative of the new data that you will see in the future. 

For example, if you have time-series data, you should use the last segment of the time-series as validation and test sets. 

A second common case is when you can easlily anticipate ways the data you will be making predictions for in production may be qualitatively different from the data you have to train your model with. E.g., if you want to classify different behaviours of drivers, you should leave as validation and test sets data from people whose images havent been used for training (instead of for example images of the same people but doing different behaviours)


Sometimes it may not be clear how your validation data will differ. For instance, for a problem using satellite imagery, you'd need to gather more information on whether the training set just contained certain geographic locations, or if it came from geographically scattered data. 




# 2

### The practice of deep learning

Underestimating the constraints and overestimating the capabilities of deep learning may lead to frustratingly poor results, at least until you gain some experience and can solve the problems that arise. Conversely, overstimating the constrainsts and underestimating the capabilities of deep learning may mean you do not attempt a solvable problem because you talk yourself out of it. 

... This doesn't mean making any risky bets -- we will show you how you can gradually roll out models so that they don't create significant risks, and can even backtest them rprior to putting them in production. 

When selecting a project, the most important consideration is data availability. We have seen many students, researchers, and industry practitioners waste months or years while they attempt to find their perfect dataset. The goal is not to find the "perfect" dataset or project, but just to get started and iterate from there. 

If you take this approach, then you will be on your third iteration of learning and improving while the perfectionists are still in the planning stages. 

We also suggest that you iterate from end to end in your project; that is, don't spend months fine-tuning your model, or polishing the perfect GUI, or labelling the perfect dataset... Instead, complete every step as well as you can in a reasonable amount of time, all the way to the end. e.g., if your final goal is an application that runs on a mobile phone, then that should be what you have after each iteration.... By completing the project end to end, you will see where the trickiest bits are, and which bits make the biggest difference to the final result. 

... Maybe you can find some previous machine learning project, such as a Kaggle competition, that is related to your field of interest. 

Especially when you are starting out with deep learning, it's not a good idea to branch out into very different areas, to places that deep learning has not been applied to before. That's because if your model does not work at first, you will not know whether it is because you have made a mistake, or if the very problem you are trying to solve is simply not solvable with deep learning. And you won't know where to look to get help. Therefore, it is best at first yo start with something where you can find an example online where somebody has had good results with something that is at least somewhat similar to what you are trying to achieve, or where you can convert your data into a format similar to what someone else has used before (such as creating an image from your data).

### The state of Deep learning

#### Computer vision
There are many domains in which deep learning has not been used to analyze images yer, but those where it has been tried have nearly universally shown that computers can recognize what items are in a n image at least as well as people can. This is known as object recognition. Deep learning is also good at recognizing where objects in an image are, and can highlight their locations and name each found object. This is known as object detection (there is also a variant of this that we saw in <>, where every pixel is categorized based on what kind of object it is part of -- this is called segmentation). Deep learning algorithms are generally not good at recognizing images that are significantly different in structure or style to those used to train the model. For instance, if there were no black-and-0white images in the training data, the model may do poorly on black-and-white images... There is no general way to check what types of images are missing n your training set, but we will show in this chapter some ways to try to recognize when unexpected image types arise in the data when the model is being used in production (this is known as checking for out-of-domain data). 

One major challenge for object detection systems is that image labelling can be slow and expensive. There are a lot of work at the moment going into tools to try to make this labelling faster and easier, and to require fewer handcrafted labels to train accurate obejct detection models. One approach that is particularly helpful is to synthetically generate variations of input images, such as by rotating them or chaning their brightness and contrast; this is called *data augmentation* and **also works well for text and other types of models**. We will be discussing it in detail in this chapter. 

**Another point to consider is that although your problem might not look like a computer vision problem, it might be possible with a little imagination to turn it into one. For instance, if  what you are atrying to classify are sounds, you might try converting the sounds into images of their acoustic waveforms and then training a model on those images.**

#### Text
Computers are very good at classifying both short and long documents based on categories such as spam or not spam, sentiment, author, source website, and so forth. We are not aware of any rigorous work done in this area to compare them to humans, but anecdotally it seems to us that deep learning performance is similar to human performance on these tasks. Deep learning is also very good at generating context-appropriate text, such as replies to social media posts, and imitating a particular author's style. It's goos at making this content compelling to humans too -- in fact, even more compelling than human-generated text. However, deep learning is currently not good at generating correct responses! We don't currently have a reliable way to, for instance, combine a knowledge base of medical information with a deep learning model for generating medically correct natural language responses. This is very dangerours, because it is so easy to create content that appears to a layman to be compelling, but actually is entirely incorrect. 


... As a rule of thumb, text generation models will always be technologically a bit ahead of models recognizing automatically generated text. For instance, it is possible to use a model that can recognize artificially generated content to actually improve the generator that creates that content, until the classification model is no longer able to complete its task. 

Despite these issues, deep learning has many applications in NLP: it can be used to translate text from one language to another, summarize long documents into something that can be digested more quickly, find all mentions of a concept of interest, and more. Unfortunately, the translation or summary could well include completely incorrect information!

#### Combining text and images
The ability of deep learning to combine text and images into a single model is generally far better than most people intuitively expect. 

 For example, a deep learning model can be trained on input images with output captions written in English, and can learn to generate surprisingly appropriate captions automatically for new images! But again, we have the same warning that we discussed in the previous section: there is no guarantee that these captions will actually be correct.

Because of this serious issue, we generally recommend that deep learning be used not as an entirely automated process, but as part of a process in which the model and a human user interact closely. This can potentially make humans orders of magnitude more productive than they would be with entirely manual methods, and actually result in more accurate processes than using a human alone. For instance, an automatic system can be used to identify potential stroke victims directly from CT scans, and send a high-priority alert to have those scans looked at quickly. There is only a three-hour window to treat strokes, so this fast feedback loop could save lives. At the same time, however, all scans could continue to be sent to radiologists in the usual way, so there would be no reduction in human input. Other deep learning models could automatically measure items seen on the scans, and insert those measurements into reports, warning the radiologists about findings that they may have missed, and telling them about other cases that might be relevant.

#### Tabular data
For analyzing time series and tabular data, deep learning has recently been making great strides. However, deep learning is generally used as part of an ensemble of multiple types of model. If you already have a system that is using random forests or gradient boosting machines (popular tabular modeling tools that you will learn about soon), then switching to or adding deep learning may not result in any dramatic improvement. Deep learning does greatly increase the variety of columns that you can include—for example, columns containing natural language (book titles, reviews, etc.), and high-cardinality categorical columns (i.e., something that contains a large number of discrete choices, such as zip code or product ID). On the down side, deep learning models generally take longer to train than random forests or gradient boosting machines, although this is changing thanks to libraries such as [RAPIDS](https://rapids.ai/), which provides GPU acceleration for the whole modeling pipeline. We cover the pros and cons of all these methods in detail in <>.


#### Recommendation systems 

Recommendation systems are really just a special type of tabular data. In particular, they generally have a high-cardinality categorical variable representing users, and another one representing products (or something similar). A company like Amazon represents every purchase that has ever been made by its customers as a giant sparse matrix, with customers as the rows and products as the columns. Once they have the data in this format, data scientists apply some form of collaborative filtering to _fill in the matrix_. For example, if customer A buys products 1 and 10, and customer B buys products 1, 2, 4, and 10, the engine will recommend that A buy 2 and 4. Because deep learning models are good at handling high-cardinality categorical variables, they are quite good at handling recommendation systems. They particularly come into their own, just like for tabular data, when combining these variables with other kinds of data, such as natural language or images. They can also do a good job of combining all of these types of information with additional metadata represented as tables, such as user information, previous transactions, and so forth.

However, nearly all machine learning approaches have the downside that they only tell you what products a particular user might like, rather than what recommendations would be helpful for a user


#### Other data types

Often you will find that domain-specific data types fit very nicely into existing categories. For instance, protein chains look a lot like natural language documents, in that they are long sequences of discrete tokens with complex relationships and meaning throughout the sequence. And indeed, it does turn out that using NLP deep learning methods is the current state-of-the-art approach for many types of protein analysis. **As another example, sounds can be represented as spectrograms, which can be treated as images; standard deep learning approaches for images turn out to work really well on spectrograms.**


#### Drivetrain approach
https://www.oreilly.com/radar/drivetrain-approach-data-products/
The basic idea is to start with considering your objective, then think about what actions you can take to meet that objective and what data you have (or can acquire) that can help, and then build a model that you can use to determine the best actions to take to get the best results in terms of your objective. 

Our objective and available levers, what data we already have and what additional data we will need to collect, determine the models we can build. The models will take both the levers and any uncontrollable variables as their inputs; the outputs from the models can be combined to predict the final state for our objective. 

In practice often the practical implementation of your models will require a lot more than just training a model. You'll often need to run experiments to collect more data, and consider how to incorporate your models into the overall system you're developing. 

### Gathering your data

...
At the time of writing, Bing Image Search is the best option we know of for finding and downloading images. It's free for up to 1000 queries per month, and each query can download up to 150 images. 


### Getting help on Jupyter Notebooks


Here are some other features that are very useful in Jupyter notebooks:

-   At any point, if you don't remember the exact spelling of a function or argument name, you can press Tab to get autocompletion suggestions.
-   When inside the parentheses of a function, pressing Shift and Tab simultaneously will display a window with the signature of the function and a short description. Pressing these keys twice will expand the documentation, and pressing them three times will open a full window with the same information at the bottom of your screen.
-   In a cell, typing `?func_name` and executing will open a window with the signature of the function and a short description.
-   In a cell, typing `??func_name` and executing will open a window with the signature of the function, a short description, and the source code.
-   If you are using the fastai library, we added a `doc` function for you: executing `doc(func_name)` in a cell will open a window with the signature of the function, a short description and links to the source code on GitHub and the full documentation of the function in the [library docs](https://docs.fast.ai).
-   Unrelated to the documentation but still very useful: to get help at any point if you get an error, type `%debug` in the next cell and execute to open the [Python debugger](https://docs.python.org/3/library/pdb.html), which will let you inspect the content of every variable.



### From Data to DataLoaders
Once you have your data, you have to assemble it in a format suitable for model training. In fastai, that means creating an object called `DataLoader`

```
jargon: DataLoaders: A fastai class that stores multiple `DataLoader` objects you pass to it, normally a `train` and a `valid`, although it's possible to have as many as you like. The first two are made available as properties.
```

To turn our downloaded data into a `DataLoaders` object we need to tell fastai at least four things:

-   What kinds of data we are working with
-   How to get the list of items
-   How to label these items
-   How to create the validation set

```



	bears = DataBlock(
	    blocks=(ImageBlock, CategoryBlock), # tuple specifying what types we want
	    # independent and dependent variables. The dependent variable is our target
	    #  
	    get_items=get_image_files, # Recursively return images of a path
	    splitter=RandomSplitter(valid_pct=0.2, seed=42), # Split into training and validation
	    get_y=parent_label, # Define labels for target
	    item_tfms=Resize(128)
	) # Resize all images to the same size. 


```



DataBlocks arguments and what they do: 

- Blocks. Define a tuple with independent variable and dependent variable
- get_times. Define how to get the data. 
- splitter. Split training and validation sets.
- get_y. Define how to get target values. 





....




...



It's helpful to see where exactly our errors are occurring, to see whether they're due to a dataset problem (e.g., images that aren't bears at all, or are labeled incorrectly, etc.), or a model problem (perhaps it isn't handling images taken with unusual lighting, or from a different angle, etc.). To do this, we can sort our images by their _loss_.

The loss is a number that is higher if the model is incorrect (especially if it's also confident of its incorrect answer), or if it's correct, but not confident of its correct answer. In a couple of chapters we'll learn in depth how loss is calculated and used in the training process. For now, `plot_top_losses` shows us the images with the highest loss in our dataset. As the title of the output says, each image is labeled with four things: prediction, actual (target label), loss, and probability. The _probability_ here is the confidence level, from zero to one, that the model has assigned to its prediction:



