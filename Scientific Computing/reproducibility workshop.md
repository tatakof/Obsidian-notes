Mistakes that lead to over optimistic results


- Data augmentation of the whole dataset before data splitting. This is introduces two types of information leakeages: 
	- Artificial samples that are highly correlated with train samples are added to the test set and used for evaluation (with the extra problem of using artificial samples for testing, thus u should only augment the training set, not the test set)
	- Artificial samples that are highly correlated with the test samples are addedn to the training set

What to do 
![[Pasted image 20220801120158.png]]
partition, then only augment training data. 



- Cutting signals into sub-signals and then splitting the sub-signals into training and testing sets. These sub-signals are highly correlated and thus introduce a bias that leads to over optimistic results. 

TIPS
![[Pasted image 20220801121022.png]]