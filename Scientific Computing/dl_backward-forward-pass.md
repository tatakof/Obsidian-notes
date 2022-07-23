### Backward pass and forward pass

The "backward" here refers to *backpropagation*, which is the name given to the process of calculating the derivative of each layer. We'll see how this is done exactly in chapter <<chapter_foundations>>, when we calculate the gradients of a deep neural net from scratch. This is called the "backward pass" of the network, as opposed to the "forward pass," which is where the activations are calculated. Life would probably be easier if `backward` was just called `calculate_grad`, but deep learning folks really do like to add jargon everywhere they can!



### Backward pass

Backward pass: Computing the gradients of the loss with respect to all model parameters.

The "backward" here refers to *backpropagation*, which is the name given to the process of calculating the derivative of each layer. We'll see how this is done exactly in chapter <<chapter_foundations>>, when we calculate the gradients of a deep neural net from scratch.
This is called the "backward pass" of the network, as opposed to the "forward pass," which is where the activations are calculated.
Life would probably be easier if `backward` was just called `calculate_grad`, but deep learning folks really do like to add jargon everywhere they can!


### Forward pass 
Forward pass: Applying the model to some input and computing the predictions.


... This is called the "backward pass" of the network, as opposed to the "forward pass," which is where the activations are calculated.