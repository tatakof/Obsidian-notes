from https://www.analyticsvidhya.com/blog/2020/04/feature-scaling-machine-learning-normalization-standardization/

# Feature scaling 
Some ML/DL algorithms are highly sensitive to features with varying degrees of magnitude, range, and units; whereas some algorithms are virtually invariant to it. Thus in some cases we need to perform feature scaling to avoid problems or performance loss. 



## Algorithms

### Gradient descent Based Algorithms
ML algorithms like Linear regression, Logistic regression, Neural Network, etc. that use gradient descent as an optimization technique require data to be scaled. 
This is due to how gradient descent works:
$$
\theta_j := \theta_j - \alpha \frac{1}{m} \sum_{i=1}^m (h_\theta (x^{(i)}) - y^{(i)}) x_j^{(i)}

$$
The presence of feature value X in the formula will affect the step size of the gradient descent. The difference in ranges of features will cause different step sizes for each feature. 
To ensure that the gradient descent moves smoothly towards the minima and that the steps for gradient descent are updated at the same rate for all the features, we have to scale the data before feeding it to the model. 

Having features on a similar scale can help the gradient descent converge more quickly towards the minima. 


---
Note 
'$:=$'  means 'is defined by'

---


### Distance-based algorithms
Distance algorithms like KNN, K-means, and SVM are most affected by the range of features, because the algorithm uses distances between data points to determine their similarity. 
Having features with different scales gives some chance that higher weightage is given to features with higher magnitude. Thus biasing our algorithm towards a given feature. 



### Tree-Based algorithms
Tree-based algorithms, on the other hand, are fairly insensitive to the scale of the features, since the decision tree is only splitting a node based on a single feature, thus the  split on a feature is not influenced by other features. This makes tree-based algorithms invariant to the scale of the features. 


## Normalization
Normalization is a scaling technique in which values are shifted and rescaled so that they end up ranging between 0 and 1. It is also known as **Min-Max scaling**.
$$
X' = \frac{X- X_{min}}{X_{max} - X_{min}}

$$
Note that if you subtract X_min from every X value, then the minimum value of the X variable is going to be 0 (because the numerator is equal to 0) and the max value is going to be equal to X_max - X_min. Then, by dividing (or scaling) every value of X by X_max - X_min, then the max value is going to be 1 (because now the numerator is equal to the denominator) and every value of X will be between 0 and 1. 

## Standarization 
Standarization is another scaling technique where the values are centered around the mean with a unit standard deviation. This means that the mean of the attribute becomes zero and the resultant distribution has a unit standard deviation. 
$$
X' = \frac{X - \mu}{\sigma}
$$


## When to Normalize and when to Standarize?
There's no hard and fast rule to tell you when to normalize or standarize your data (you can always test both and check performance). But here a few things to keep in mind. 

- **Normalization** is good to use when u know that the distribution of ur data does NOT follow a Gaussian distribution. This can be useful in algorithms that do not assume any distribution of the data like KNN or Neural Nets. 
- **Standarization**, on the other hand, can be helpful in cases where the data follows a Gaussian distribution. However, this does not have to be necessarily true. Also, unlike normalization, standarization does not have a bounding range. So, even if you have outliers in your data, they will not be affected by standarization. An important thing to note is that by standarizing a variable you are assuming that variable follows a given distribution, since for standarization you need a mean and a standard deviation (and they are computed differently for different distributions?)

!!!
It's a good practice to fit the scaler on the training data and then use it to transform the testing data. This would avoid any data leakage during the model testing process. Also, the scaling of target values is generally not required. 
(m' I think what the author means is that you should perform the feature scaling separately, first on the training data and then in the testing data, cuz if you perform the scaling in the whole data set and then split it into training and test data, you will have information leakage. Also the author mentions that the scaling of the testing values is generally not required, I think because the model makes predictions that are unscaled)

Note that in the case of Standarization, the values of X' are not restricter to a particular range.


Also note that that standarization should only be applied to numerical variables and not the one-hot encoded features (dummy variables). **Standarizing the One-Hot encoded features would mean assigning a distribution to categorical features**

## Comparing unscaled, normalized and standarized data 

![Feature scaling: Normalization vs Standardization](https://cdn.analyticsvidhya.com/wp-content/uploads/2020/03/NormVsStand_box_plots-1.png)



