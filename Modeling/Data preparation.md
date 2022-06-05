# General 
Things to keep in mind: 
- You always must have a training set and a validation set, and if possible a test set. 







## CNNs

We usually feed our cnn with several images at a time (called a mini batch), to do this, we need to group them in a big array (called tensor). This big array need all images to be of the same size, and thus we have to make sure we resize all of our images (see [[fai_methods]])

See also [[fai_cnn]] content and maybe add it here. 



### Encoding Time-series as images

"A good rule of thumb for converting a dataset into an image representation: if the human eye can recognize categories from the images, then a dl model should be able to do so too" (fastai 01)
'm But at the same time there are examples where a human eye couldn't recognize categories (like that example of turning security of a computer behaviour into a bit map) but it still worked. So maybe we could do the same'. 

https://www.kaggle.com/code/tigurius/recuplots-and-cnns-for-time-series-classification/notebook

https://arxiv.org/pdf/1710.00886.pdf



https://pdfs.semanticscholar.org/9bd2/f60e9d37a1c37da659ada8583d3cb84e41a6.pdf

https://medium.com/analytics-vidhya/encoding-time-series-as-images-b043becbdbf3

https://pyts.readthedocs.io/en/0.10.0/auto_examples/image/plot_gaf.html

https://pyts.readthedocs.io/en/0.10.0/auto_examples/index.html#multivariate-time-series


https://pyts.readthedocs.io/en/0.10.0/auto_examples/multivariate/plot_joint_rp.html#sphx-glr-auto-examples-multivariate-plot-joint-rp-py

https://pyts.readthedocs.io/en/0.10.0/auto_examples/multivariate/plot_weasel_muse.html#sphx-glr-auto-examples-multivariate-plot-weasel-muse-py


Different types of encoding. Advantages and Disadvantages. 

"A typical approach is to convert the time-series to a spectrogram. This is disadvantageous since in a spectrogram it matters where an effect appears in contrast to CNNs where it is assumed that a feature is of the same kind, no matter where in the picture it is. The usage of recurrence plots as visualization of the recurrence structure of a time-series is hence advantageous." (https://www.kaggle.com/code/tigurius/recuplots-and-cnns-for-time-series-classification/notebook)



- Gramian Angular Field: 
	An image obtained from a time series that rperesents some temporal correlation between each time point. There are 2 different methods
	- Gramian Angular Summation Field
	- Gramian Angular Difference Field