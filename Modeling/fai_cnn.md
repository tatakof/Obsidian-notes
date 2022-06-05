
## Tasks a CNN can handle
A CNN is an image recognizer, but many things can be turned into images and thus be classified using a CNN. E.g.: 
- Sounds to Spectrograms (amount of frequency at each time)
- Time-series to simply plots. 
- Time-series to images with Gramian Angular Difference Field. (advantage of being able to capture seasonality and anomalies)
- Time-series to gray-level-images. 





## Size of images (mostly from fastbook)
We usually feed the model with several images at a time (called mini-batch). To do this, we group the images in a big array (or tensor), but the images have all to be of the same size. 

If your images are all of different sizes, you have to Resize them so that all have the same size. With fastai, you can use the `Resize` transform. 


## Resizing images
fastai `Resize` transform crops the images to fit a square of the size requested (using the full width or height). But this can result in losing some important details. You can also pad the images with zeros(black) or squish/stretch them. 
But all of these approaches are problematic or wasteful. 
Squishing and stretching deforms the image, making the model learn some features that are not actually real (and probably wont appear in your target), and thus lose some model accuracy. On the other hand, consistent cropping will maybe make an image lose its defining characteristic that allows the model to differentiate that image category from others. 
Lastly, padding simple wastes computation due to a lot of empty space and also results in lower resolution for the part of the image that we are interested in. 


What fastai recommends is cropping a random part of each image during each epoch. That will allow are model to focus on and recognize different features in our images. 
Btw, images of the same thing in the real world can be framed in slightly different ways, so this approach reflects how images are taken. 

Training an NN with variations of the same image (with objects in different places and with different sizes) helps the NN to understand the basic concept of what an object is and how it's represented in an image. 





## Standards of image classification

Image size: 224 pixels. 