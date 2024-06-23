# Classifying brain signals for Brain Computer Interfaces ![fe39816bb3e1714c56b2b4beb6b8ce10.png](../_resources/fe39816bb3e1714c56b2b4beb6b8ce10.png)
## Why? 
One of the important applications of EEG recordings is analyzing it to predict what the subject is thinking to do. For example- If we play a subway surfers using Brain computer Interface,BCI as control, so our aim will be to predict whether subject wants to go left or right or jump or duck.
* * *
## Some more examples 
· Word spellers: selecting 1 out of 26–29 letters
· Menu with options: selecting 1 out of N options
· Semi-autonomous robots: selecting 1 out of N high-level commands
![ef5de37c2caf280dff1ac478e35dd824.png](../_resources/ef5de37c2caf280dff1ac478e35dd824.png)
* * *
## How?
We have input data that contains **channels** and their corresponding eeg recording which is a time series data.  We transform this signal to something called a feature vector.![96a5cb500540657b1a636620b2909740.png](../_resources/96a5cb500540657b1a636620b2909740.png)Combining feature vector of all channels, we get a matrix now that stores our potential input to the classifier.
![564965b8bbb72ddba57fb1ab90ddce5d.png](../_resources/564965b8bbb72ddba57fb1ab90ddce5d.png)
* * *
## The five classifiers we will cover are:

- #### Linear classifiers 
 A linear functions is used to discriminate between classes.
 For example- SVMs(Support Vector Machines) and LDA(Linear Discriminant Analysis)
 LDA is based on the mean vectors and the covariance matrices of patterns for individual classes. LDA basically uses hyperplanes to separate the classes. A pro of using LDAs as a classifier for is that they require a very low computational processing power (load), which is suitable for online BCI systems.

 Suppose we have 2 classes in a given data and we aim to find a line that separates them. SVMs not only find the line but also finds the line with maximum margin.![f06ea58e3a69bcf8e3e52e53a875b62a.png](../_resources/f06ea58e3a69bcf8e3e52e53a875b62a.png)
 
- #### Neural network classifiers
These classifiers consist of multiple layers of neurons (also called multilayer perceptrons) connected in such a way that each neuron is activated using weighted values from the neurons in the previous layer and some activation functions. NNs work by ‘learning’ and adjusting a weight w that minimizes total squared output error (cost function) over all output units, which though backpropogation can change its own weight value.

- #### Nonlinear Bayesian classifiers

Produce nonlinear decision boundaries.
Generative models, enabling efficient rejection of uncertain samples, unlike discriminant classifiers.
Types:
1. Bayes Quadratic
2. Hidden Markov Model (HMM)

- ####  Nearest neighbor classifiers
These classifier plot the data points and then for classifying an unlabeled data point, they determine the distance from nearest data (neighbours)points.With sufficiently large k and enough training samples, kNN can approximate any function which enables to produce nonlinear decision boundaries.The reason for not being among the more popular classifiers in BCI systems, is the curse of dimensionality that follows with nearest neighbor systems.

- #### Combinations of the above
 There are different strategies to combine classifiers in BCI systems:
 **Boosting**: Using several classifiers in cascade
 **Voting**: Several classifiers that are being used with each of them assigning the input feature vector to a class
 **Stacking**: Several classifiers, with each of them classifying the input feature vector (level 0 classifiers)

* * *
![431811ed8f23e2f1942661f1c0130651.png](../_resources/431811ed8f23e2f1942661f1c0130651.png)
