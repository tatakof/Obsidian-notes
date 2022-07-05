To properly define a validation and test sets, you should do somethimg more than randomly grab a fraction of your original dataset, because a key property of the validation and test sets is that they must be representative of the new data that you will see in the future. 

For example, if you have time-series data, you should use the last segment of the time-series as validation and test sets. 

A second common case is when you can easlily anticipate ways the data you will be making predictions for in production may be qualitatively different from the data you have to train your model with. E.g., if you want to classify different behaviours of drivers, you should leave as validation and test sets data from people whose images havent been used for training (instead of for example images of the same people but doing different behaviours)


Sometimes it may not be clear how your validation data will differ. For instance, for a problem using satellite imagery, you'd need to gather more information on whether the training set just contained certain geographic locations, or if it came from geographically scattered data. 
