#  Classifying brain signals for Brain-Computer Interfaces (a short introduction)

### Why do you need classification?
Many BCI applications require selecting 1 out of several options. So, by classifying brain signals we associate certain extracted features with certain commands. In its simplest case, classification techniques can classify a given brain signal into 1 of several classes, such as a binary classification (2 classes).

### Fundamentals
- Classification of biomedical signals (from brain oscillation recordings), is the process of categorizing the electrical activity measured by our recording device. In other words, it is the process of grouping values of a set based on a property that all values in that set share. 

- A classifier is the computational tool, used to obtain classification.

- It is not advised to use complex classifiers for a simple job. Using a deep neural network for a simple binary classification that could be solved with a linear discrimination, would be a waste of computational power, and make the BCI system slow and inefficient.
- The most important things are,
 1.  EEG signals are very noisy, i.e. noise reduction should be performed
2.  We should aim to choose the best features for classification
3.  Prioritising the most important channels for a given feature helps classification (dimensionality reduction) 

- To classify the brain signals, we transform the EEG signals to a feature vector, use some function to get a full matrix of feature vectors. This is feature extraction.

![image](https://github.com/aarsh-12/BCS_Drowsiness_Detection/assets/169232982/36047344-2e03-4070-9ddc-d3a95de4604f)

## Classification Algorithms for BCI systems 
### Linear classifiers
Linear Classifiers are algorithms that use linear functions to distinguish classes. Two examples are LDA and SVM.

#### Linear Discriminant Analysis
LDA is a popular binary classifier. It is based on the mean vectors and the covariance matrices of patterns for individual classes. LDA basically uses hyperplanes to separate the classes. It is a simple classifier and works well on simple datasets, however is not as as accurate on complex EEG data.

#### SVMs
SVMs are some of the simplest supervised machine learning models out there.
They help us find a line(or a hyperplane) with the highest margin which divides and classifies our data.
In order to find the best line, first we must define the classifier margin. The classifier margin of a linear classifier is the width that the boundary could be increased by, before hitting any data points. The maximum margin linear classifier is the linear classifier with the maximum margin. 

### Neural Networks
Neural Networks are deep learning models which are used for datasets which require non-linear classification. 
NNs learn by adjusting weights and biases, to minimize cost function and then using backpropagation to change its own weights. 
![image](https://github.com/aarsh-12/BCS_Drowsiness_Detection/assets/169232982/1e662c27-885e-4bd1-bf8b-f21016ddc40d)

## Nonlinear Bayesian Classifiers

Bayes quadratic and HMMs are the two non-linear bayesian classifiers used.

Bayesian Classification summarized in three points:  
i. Assigns the highest probability to the feature vector for the class it belongs  
ii. Bayes rule is used to calculate the posterior probability  
iii. Using the maximum A-posteriori (MAP) rule and the calculated probabilities, the class of the feature vector can be determined.

HMM are dynamic classifiers in speech recognition, they identify certain sequences of feature vectors to classify the time series data.

## Nearest Neighbour Classifiers

Its basic principle is assigning a feature vector to a class based on its nearest neighbor(s).
It uses kNNs and MD. MD-based classifiers are good but are rarely seen in BCI literature. In case of using kNN, the aim is to assign an unseen point in the dominant class among its kNN, within the training set. With sufficiently large k and enough training samples, kNN can approximate any function that enables the production of nonlinear decision boundaries. The major issue with this is it is poor at higher dimensions. 

## Combinations of the above
There are different strategies to combine classifiers in BCI systems:

**Boosting** : Using several classifiers in cascade

**Voting** : Several classifiers that are being used with each of them assigning the input feature vector to a class

**Stacking** : Several classifiers, with each of them classifying the input feature vector (level 0 classifiers)

## Performance Metrics

For a given algorithm, its performance metrics are evaluated through the classifier's accuracy. The classifier's performance can be optimized and improved in the post-processing stage.

![image](https://github.com/aarsh-12/BCS_Drowsiness_Detection/assets/169232982/182c2cdd-615d-454f-ba3a-00a23c416353)
 ---
