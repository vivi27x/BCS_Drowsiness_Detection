### Classification schemes:
*	Linear classifiers
    *	Linear discriminant analysis
    *	Support vector machines
*	NN classifiers
*	Non-Linear classifiers
*	Bayesian classifiers
*	Nearest neighbour classifiers
### Key points:
*	EEG signals are noisy – filters in the signal processing step
*	Choose best features for classification
*	Prioritise more important channels depending on intended application – reduces dimensions
### Basics of classification
*	Feature vector X obtained from EEG
*	Feature matrix formed
*	Classifier is then trained and tested
### Linear classifiers
*	LDA
    *	Binary classification
    *	Based on mean, covariance vectors
    *	Hyperplanes to separate classes
    *	Low computational power, good with simple datasets(unlike EEG)
*	SVM
    *	Simplest supervised learning algorithm
    *	Discriminant hyperplanes
    *	Process – Classifier margin(width the boundary could be increased by before hitting a data point) is defined -> line with maximum margin chosen
### Neural networks
*	Multilayer perceptrons are used – makes NNs sensitive to overfitting
*	Work great for data that requires non linear classification
*	Learning and adjusting weights to reduce cost function
*	Great for image classification
### Nonlinear Bayesian Classifiers
*	Two types:
    *	Bayes quadratic
        *	Assigns highest probability to feature vector for the class it belongs -> Bayes rule used to calculate posteriori probability -> MAP rule to determine class
    *	Hidden Markov Model
        *	Good for speech recognition, time series
        *	GMM, IOHMM usually used in BCI applications
### Nearest Neighbour Classifiers
*	Discriminative non-linear classifiers
*	Model assigns a feature vector to a class based on nearest neighbours
*	Main aim while using kNN – assign an unseen point in the dominant class within the training set
*	Drawback – dimensionality is high
### Combination of Classifiers
*	Boosting – Cascade of classifiers – powerful classifier can be formed using several weak ones
*	Voting – Several classifiers are used and the final class will be that of the majority – Most popular in BCI
*	Stacking – Several classifiers classify -> output fed into meta-classifier to make final decision
### Performance metrics
*	Evaluated using accuracy
*	Different metrics like sensitivity, specificity, Youden’s index discriminant power, and computation time / load can be used
*	Parameters of classifier can be optimized to increase accuracy




