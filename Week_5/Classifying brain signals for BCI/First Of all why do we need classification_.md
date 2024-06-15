First Of all why do we need classification?
> Classification of biomedical signals is essential in building Brain-Computer Interfaces (BCIs) to distinguish between different mental actions.
> A higher resolution of signal classification is proportional to the number of mental commands a single BCI system can manage.
> Classification techniques can help to classify brain signals into several classes one such example is binary classificaton.

Components of a Brain-Computer Interface is shown in the **image**:



![Screenshot 2024-06-12 105539.png](./Screenshot%202024-06-12%20105539.png)


## Classification Schemes:
In this article we are given with 5 categories of commonly used classification schemes: Linear Classifiers, Neural Network (NN) Classifiers, Non-linear Bayesian Classifiers, Nearest Neighbour Classifiers, and Classifier Combinations.
## Fundamentals:
- Classification is basically categorization of the electrical activity measured by our recording device.
- It is the process of grouping values of a set based on a property that all values in that set share
example is shown in the **image**:





![Screenshot 2024-06-12 105553.png](./Screenshot%202024-06-12%20105553.png)





- A classifier is the computational tool, used to obtain classification.

Three key points:
> - EEG signals are very noisy, i.e. noise reduction should be performed.
> - We should aim to choose the best features for classification.
> - Prioritising the most important channels for a given feature helps    classification.

## Basics Of Classification:
**image**:

![Screenshot 2024-06-12 105606.png](./Screenshot%202024-06-12%20105606.png)


- In order to classify EEG signals, we have to transform each EEG signal to a feature vector. Let’s call that feature vector for x.

With the above function, we can then derive the **following**:

![Screenshot 2024-06-12 110554.png](./Screenshot%202024-06-12%20110554.png)


- This in turn, allows us to obtain a set of feature vectors as a matrix given the **following**:

![Screenshot 2024-06-12 110605.png](./Screenshot%202024-06-12%20110605.png)


- Once feature extraction is done, the classification can be **performed**:

![Screenshot 2024-06-12 110622.png](./Screenshot%202024-06-12%20110622.png)



# Classification Algorithms for BCI systems:
## 1. Linear classifiers:
Two examples are:
- Linear Discriminant Analysis (LDA)
- Support Vector Machines (SVM)

### Linear Discriminant Analysis (LDA):
- it is a method of binary classification.
- It is based on the mean vectors and the covariance matrices of patterns for individual classes.maximize the distance between means and minimizing the variatiion within each category.
- The d-dimensional feature vector x is projected onto a lower **dimension**

![Screenshot 2024-06-12 121146.png](./Screenshot%202024-06-12%20121146.png)


- this can be realized by optimizing a cost function related to within-class covariance matrix (S_w) and between-class **covariance matrix (S_b**):


![Screenshot 2024-06-12 121408.png](./Screenshot%202024-06-12%20121408.png)



### Support Vector Machines (SVM):
- SVMs use discriminant hyperplanes to identify classes.
- The selected hyperplane(s) maximizes the margins
- It maps the data to higher dimensions using kernel functions
- In order to find the best line, first we must define the classifier margin. The classifier margin of a linear classifier is the width that the boundary could be increased by before hitting any data points. 
- The maximum margin linear classifier is the linear classifier with the maximum margin.
- **Visualisation**:

![Screenshot 2024-06-12 123217.png](./Screenshot%202024-06-12%20123217.png)


## 2. Neural Networks:
- Neural networks make use of multilayer perceptrons (MLPs)
- NNs are great for data sets that require non-linear classifications.
- NNs work by ‘learning’ and adjusting a weight w that minimizes total squared output error (cost function) over all output units, which though backpropogation can change its own weight value.
**Visualisation**:

![Screenshot 2024-06-12 123515.png](./Screenshot%202024-06-12%20123515.png)


## Nonlinear Bayesian classifiers:
Two types:
- Bayes quadratic
- Hidden Markov Model (HMM)

### Bayes Quadratic:
i. Assigns the highest probability to the feature vector for the class it belongs
ii. Bayes rule is used to calculate the posteriori probability
iii. Using the maximum A-posteriori (MAP) rule and the calculated probabilities, the class of the feature vector can be determined.

### HMM:
- are popular dynamic classifiers in speech recognition.
- HMM can be seen as a kind of probabilistic automaton that can provide the probability of observing a given sequence of feature vectors.
- For BCI related uses, these probabilities usually are Gaussian mixture models

## Nearest Neighbor Classifiers:
- The models assign a feature vector to a class according to its nearest neighbor(s).
- The neighbor can be a feature vector from the training set as in the case of k-nearest neighbors (kNN) or a class prototype as in Mahalanobis distance (MD).
## Combination of classifiers:
- To enhance the efficiency of the model we use combinations of classifiers.
### Boosting:
- It uses several classifiers in cascade
- This can build up a powerful classifier by putting together several weak ones.
### Voting: 
- Several classifiers that are being used with each of them assigning the input feature vector to a class
- The final class will be that of the majority
- Voting is the most popular way of combining classifiers in BCI research.
### Stacking: 
- Several classifiers, with each of them classifying the input feature vector 
- The output of each of these classifiers are then fed to the meta-classifier  to make the final decision (eg., HMM — SVM in BCI).
