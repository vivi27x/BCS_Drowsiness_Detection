Signal classification is the 4th step in building a BCI. By classifying brain signals, we can equalize certain sets of extracted features to correspond to certain commands. 

<img src="../_resources/Screenshot%202024-06-11%20232847-1.png" width="200" >


### FUNDAMENTALS
- From the sample data we extract features based on which we use classification techniques to determine the actions corresponding to the signals.

<img src="../_resources/Screenshot%202024-06-11%20233244-1.png" width="300" >

- From the d- dimensional feature vector ***x<sub>n</sub>*** we find the the feature matrix ***X*** which is used in classification algorithms.







Here, we talk about the following classification techniques:
1. Linear classifiers
2. Neural network classifiers
3. Nonlinear Bayesian classifiers
4. Nearest neighbor classifiers
5. Combinations of the above

### LINEAR CLASSIFIERS:
Two examples are:
- Linear Discriminant Analysis (LDA, also known as Fischer’s LDA (FLDA))
- Support Vector Machines (SVM)
#### Linear Discriminant Analysis (LDA)
- LDA is a very popular binary classification method.
- LDA uses hyperplanes to separate the classes.
- They require a very low computational processing power
- It has the drawback that linearity provides poor results on complex EEG data sets.
- Here, the d-dimensional faeture vector ***x*** is projected down to **one dimensional scalar**  using the vector **w**

- The seperation of the mean of the respective classes is maximised and the variances are minimised.

<img src="../_resources/Screenshot%202024-06-12%20001531-1.png" width="300" >



#### SUPPORT VECTOR MACHINES (SVM):
- SVMs use discriminant hyperplanes to identify classes.
- The selected hyperplane(s) maximizes the margins
- It is possible to create nonlinear decision boundaries with SVMs by using a “kernel trick” with kernel functions (Gaussian and Radial Basis Functions (RBF)):

<img src="../_resources/af6f23db0e38851274684bf35570396c-1.png" width="200" >


- The hyper-parameters (the **regularization parameter** and **RBF widths**) need to be found manually.
- **Classifier margin:** width that the boundary could be increased by before hitting any data points
- The ***maximum margin linear classifier*** is the linear classifier with the maximum margin.
<img src="../_resources/3ff83d69d8a6c39d5bc0d6d05e3bfe42-1.png" width="300" >

It is generally used as it provides minimum error if the boundary is jolted in the perpendicular direction and is unaffected by the non-inclusion of non support vectors (**Leave-one-out cross validation**)




### NEURAL NETWORKS (NN):
- Neural networks make use of multilayer perceptrons
- Neural networks make use of multiple layers of neurons with varying activations
- Each neuron is connected to the neurons of other layers by **weights**
- The **weights** and **biases** are the inputs which determine the activation of the neurons of the next layer.
- Finally using backpropagation the **weights** and **biases** are modified to get optimum results.
<img src="../_resources/805ba9af4081064b4f94314081362411-1.png" width="300" >

###  NONLINEAR BAYESIAN CLASSIFIERS:
- Two types: **Bayes quadratic**, **Hidden Markov Model (HMM)**
- Produces nonlinear decision boundaries.
- Assigns highest probability to the feature of the class the instance belongs to according to **Bayes' Theorem**
- **HMMs** are popular dynamic classifiers in speech recognition.
- It is a type of probabilistic automaton that can provide the probability of observing a given sequence of feature vectors. Usually are **Gaussian mixture models ( GMM)** are used.
- Input-output HMM (IOHMM) is another type of HMM that is used in BCI applications.


### NEAREST NEIGHBOUR CLASSIFIERS:
- The models assign a feature vector to a class according to its nearest neighbor(s).
- In case of using kNN, the aim is to assign an unseen point in the dominant class among its kNN, within the training set (for BCI, the nearest neighbor are obtained using metric distances).
- However its inability to bypass the **curse of dimensionality**, it is not not among the popular classifiers for BCI

### COMBINATION OF CLASSIFIERS:
 Done to improve the performance of the BCI
1. **Boosting:** Using several classifiers in cascade
	 - Builds up a powerful classifier by putting together several weak ones.
	- Has a tendency of mislabeling.
	- Boosting has been tried with MLP
2. **Voting:**
	- The final class will be that of the majority
	- Most popular way
3. **Stacking:** Several classifiers, with each of them classifying the input feature vector (level 0 classifiers)
	- The output of each of these classifiers are then fed to the meta-classifier (level 1 classifier) to make the final decision (eg., HMM — SVM in BCI).
	- The combination of similar classifiers is likely to outperform on of classifiers on its own is an advantage.
	- The combination is known to reduce the variance and thus the classification error

### PERFORMANCE METRICS:
- The performance metric of a given algorithm or classification scheme is usually evaluated using the classifiers’ accuracy.
- A comparison of classifiers from different aspects can be done using different metrics (sensitivity, specificity, Youden’s index discriminant power, and computation time / load)