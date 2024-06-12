BCI (Brain Computer Interference)

Classification - Classification of biomedical signals is essential in
building Brain-Computer Interfaces (BCIs) to distinguish between
different mental actions.

As we are building BCI we need to classify our signals.
<span class="mark">By classifying brain signals, we can equalise certain
sets of extracted features to correspond to certain commands.</span>

<span class="mark">LDA (Linear Discriminant Analysis): this is a
classification technique in which we divide the data into two different
groups and make a boundary between both the classes. this is also a sort
of binary classifier.</span>

<span class="mark"></span>

<span class="mark">A classification scheme is the descriptive
information for an arrangement or division of objects into groups based
on characteristics, which the objects have in common, obtained by using
a classifier.</span>

<span class="mark">For the classification, We need to transform each EEG
signal into a feature vector.</span>

<span class="mark">Once data is ready for classification now we have 5
types of algorithms for classifying the data. It goes as…</span>

1.  <span class="mark">**Linear classifiers:** Linear classifiers are
    > discriminant algorithms that use linear functions to distinguish
    > classes.</span>

> <span class="mark">In linear classification, we have two
> technique</span>

- <span class="mark">LDA: It uses a hyperplane to separate the classes.
  > A pro of using LDAs as a classifier for is that they require a very
  > low computational processing power (load).</span>

- <span class="mark">SVM(Support vector machine): S</span>VM uses
  > discriminant hyperplanes to identify classes<span class="mark">. We
  > found the hyper-parameters for the boundary line bn two classes but
  > is it not the best line, to find the best line we make a
  > margin(width) in the line.</span>

> <span class="mark">Now, we have a more efficient line to classify the
> classes, if we make a little error in input data it still classifies
> the correct class.</span>

2.  <span class="mark">**Neural Network:** Neural networks make use of
    > multilayer perceptrons (MLPs), which make universal
    > approximators.</span>

> <span class="mark">NNs work by ‘learning’ and adjusting a *weight w*
> that minimizes total squared output error (cost function) overall
> output units, which though backpropagation can change its own *weight*
> value. By this it produce a best fit line to distinguish bn classes.
> We learn CNN we generally CNN technique for classification of
> data.</span>

3.  <span class="mark">**Nonlinear Bayesian Classifiers:**There are
    > basically two types of nonliear Bayesian classifiers in use for
    > BCI systems.</span>

> <span class="mark">1. Bayes quadraric:</span>
>
> <span class="mark">They work by producing no-linear boundaries. It
> work using probability calculation for each class and assigns the
> higher probability to the feature map from where it belongs.</span>
>
> <span class="mark">2. Hidden markov model:</span>
>
> <span class="mark">They have shown to be good classifiers when using
> time series (making them suitable for EEG based BCIs).</span>
>
> <span class="mark">HMM can be seen as a kind of probabilistic
> automaton that can provide the probability of observing a given
> sequence of feature vectors.</span>

4.  <span class="mark">**Nearest Neighbor Classifiers:**The models
    > assign a feature vector to a class according to its nearest
    > neighbor(s). The neighbor can be a feature vector from the
    > training set as in the case of k-nearest neighbors (k-NN).</span>

> <span class="mark">In case of using kNN, the aim is to assign an
> unknown data point in the dominating class among its k-NN, with in the
> training set.</span>
>
> <span class="mark">In BCI the nearest nieghbour are obtained by metric
> distance(MD).</span>
