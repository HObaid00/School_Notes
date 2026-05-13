# K-fold Cross Validation
* Split your learning data into $\Large K$ folds (10-folds CV is common).
* Use $\Large K-1$ folds for training and the remaining for evaluation
* Average over all folds to get an estimate
	* of the error for a setting of your *hyper-parameter*
	* or the model for your model selection
* Try different settings for your hyper-parameters.
* Use all your training data and the best hyper-parameters for final training ( and testing) of your model

![[Pasted image 20260227092634.png]]

---
# LOOCV - The extreme Case

In leave-one-out-cross validation (LOOCV) we train on all but one
sample.

If we have N samples, this is the same as N -fold cross-validation.

LOOCV is interesting if we do not have a lot of data and we want to use as much of it for training as possible but still get a good estimate of model performance.

But it also means that we need to train our model N times...

If we have sufficiently large amounts of data and training our model is computationally expensive, we better stick to lower numbers of K or a single validation set.


$$\Large
\text{misclassification rate} = \frac{\text{\# wrong predictions}}{\text{total points}}
$$
---
# Links
[[Machine Learning]]
