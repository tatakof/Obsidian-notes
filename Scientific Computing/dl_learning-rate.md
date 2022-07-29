### Definition

Learning rate: The size of the step we take when applying SGD to update the parameters of the model.



Deciding how to change our parameters based on the values of the gradients is an important part of the deep learning process. Nearly all approaches start with the basic idea of multiplying the gradient by some small number, called the *learning rate* (LR). The learning rate is often a number between 0.001 and 0.1, although it could be anything. Often, people select a learning rate just by trying a few, and finding which results in the best model after training (we'll show you a better approach later in this book, called the *learning rate finder*). Once you've picked a learning rate, you can adjust your parameters using this simple function:

```

w -= gradient(w) * lr

```

This is known as *stepping* your parameters, using an *optimizer step*.

  

If you pick a learning rate that's too low, it can mean having to do a lot of steps. <<descent_small>> illustrates that.

![[Pasted image 20220720065013.png]]




But picking a learning rate that's too high is even worse—it can actually result in the loss getting *worse*, as we see in!

![[Pasted image 20220720065111.png]]

If the learning rate is too high, it may also "bounce" around, rather than actually diverging; <<descent_bouncy>> shows how this has the result of taking many steps to train successfully.

![[Pasted image 20220720065201.png]]


- Why can't we always use a high learning rate?
The loss may “bounce” around (oscillate) or even diverge, as the optimizer is taking steps that are too large, and updating the parameters faster than it should be.





### Hands on 
One of the most important things we can do when training a model is to make sure that we have the right learning rate. If our learning rate is too low, it can take many, many epochs to train our model. Not only does this waste time, but it also means that we may have problems with overfitting, because every time we do a complete pass through the data, we give our model a chance to memorize it.



#### Learning rate finder

What do we do to find the perfect learning rate—not too high, and not too low? In 2015 the researcher Leslie Smith came up with a brilliant idea, called the *learning rate finder*. His idea was to start with a very, very small learning rate, something so small that we would never expect it to be too big to handle. We use that for one mini-batch, find what the losses are afterwards, and then increase the learning rate by some percentage (e.g., doubling it each time). Then we do another mini-batch, track the loss, and double the learning rate again. We keep doing this until the loss gets worse, instead of better. This is the point where we know we have gone too far. We then select a learning rate a bit lower than this point. Our advice is to pick either:

  

- One order of magnitude less than where the minimum loss was achieved (i.e., the minimum divided by 10)

- The last point where the loss was clearly decreasing

  

The learning rate finder computes those points on the curve to help you. Both these rules usually give around the same value

We can see on this plot that in the range 1e-6 to 1e-3, nothing really happens and the model doesn't train. Then the loss starts to decrease until it reaches a minimum, and then increases again. We don't want a learning rate greater than 1e-1 as it will give a training that diverges like the one before (you can try for yourself), but 1e-1 is already too high: at this stage we've left the period where the loss was decreasing steadily.

Even after we unfreeze, we still care a lot about the quality of those pretrained weights. We would not expect that the best learning rate for those pretrained parameters would be as high as for the randomly added parameters, even after we have tuned those randomly added parameters for a few epochs. Remember, the pretrained weights have been trained for hundreds of epochs, on millions of images.


UPDATE: https://forums.fast.ai/t/new-lr-finder-output/89236/3

Essentially before we had the two suggesters from the one-cycle paper, a global min and an estimated steepest slope (now called `steep` and `minimum`). We found that these tend to not give the best estimations for a good learning rate, and two other methods were created: the `valley` algorithm and the `slide` algorithm. They’re two other methods for getting a **much** better suggested learning rate to use OOTB without needing any graphical interpretation.

Valley and Slide can be used intermittently (or together as I’ll show in a moment!), but **in general** we found that: Valley > Slide > Steep > Minimum. Hence why the new default is `valley`.

Now let’s bring it back to the LR Finder. You can pass in **any or all** of those above methods to `lr_find`, and have _all_ of them plotted on the same graph! So then you can interpret for yourself which LR you want to go with.

To do so all you need to do is:

```
learn = Learner(...) # any cnn_, tabular_, etc will work
lrs = learn.lr_find(suggest_funcs=(minimum, steep, valley, slide))
```