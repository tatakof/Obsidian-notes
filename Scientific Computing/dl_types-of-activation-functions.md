



### ReLU 
Function that returns 0 for negative numbers and doesn't change positive numbers.



### Sigmoid
23. Draw the sigmoid function. What is special about its shape?
Sigmoid function is a smooth curve that squishes all values into values between 0 and 1. Most loss functions assume that the model is outputting some form of a probability or confidence level between 0 and 1 so we use a sigmoid function at the end of the model in order to do this.


24. What is the difference between a loss function and a metric?

  

The key difference is that metrics drive human understanding and losses drive automated learning. In order for loss to be useful for training, it needs to have a meaningful derivative. Many metrics, like accuracy are not like that. Metrics instead are the numbers that humans care about, that reflect the performance of the model.