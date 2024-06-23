# BCI Classification
Classification of biomedical signals is crucial for distinguishing between different mental actions in building Brain-Computer Interfaces.

Classification is the fourth step after obtaining, preprocessing the signals and then extracting features.

## Classification Schemes
Basically, we look at the electrical activity adn group them into sets on basis of the common properties they share
##### Important Note: Aim to choose the best features and prioritise the important channels
## Classification Algos
1. ### Linear Classifiers :
     ##### LDA :
             It separate classes based on the mean vectors and covariance matrices of patterns for individual classes.
             It uses hyperplanes to distinguish between classes in a linear manner. LDA requires low computational processing power, making it suitable for online BCI systems.
              Projection: The d-dimensional feature vector x is projected onto a lower dimension (scalar) to ensure that the means of the classes are well-separated while keeping the spread of the data small.
              Optimization: optimizes a cost function related to within-class covariance matrix (S_w) and between-class covariance matrix (S_b).
              Classification: optimal threshold z_0 is chosen, and any feature vector x can be classified based on this threshold.
                
              As far as I could understand, the goal of LDA is to find a linear boundary that maximizes the separation between classes while minimizing the spread within each class.
     ##### SVM : 
             Feels much simpler to visualize
             Uses selected hyperplanes that maximizes the margins i.e. basically just the distance between the mean line and the points closest to it.
2. ### Neural Network Classifiers :
     We know the basics and stuff.
     ##### New stuff :
             Approach for prosthetic arm and a flowchart that would help with implementation I suppose
3. ### Non-linear Bayesian Classifiers :
     I didn't really get why we introduce HMMs here because as far as I remembered, HMMs were when we can define all the states, transition probabilities etc. and also HMMs were mainly speech recognition and a bit good at time series stuff like weather forecast. Time series feels useful but when I tried it earlier on weather data, the result wasn't good ( too much deviation, sometimes opposite predictions ) 
4. ### Nearest Neighbour Classifiers :
     The models assign a feature vector to a class according to its nearest neighbor(s). The neighbor can be a feature vector from the training set as in the case of k-nearest neighbors (k-NN). In case of using kNN, the aim is to assign an unknown data point in the dominating class among its k-NN, with in the training set. In BCI the nearest nieghbour are obtained by metric distance(MD).

5. ### Combination of above :
     We have pros given that were expected.
