# The Necessity of Leave One Subject Out(LOSO) Cross Validation for EEG Disease Diagnosis

## Abstract:
- Scalp recorded EEG signal comes with High variability between individual subjects and recording sessions.
- This study primarily aimed to show how important is to have a leave-one-subject-out (LOSO) evaluation done for any scalp recorded EEG based machine learning.
-  This study also demonstrates effectiveness of a Multilayer Perceptron (MLP) in getting good LOSO accuracy from balanced, clean EEG data, without any pre-processing in comparison with traditional machine learning algorithms.
-  The study used data from participants diagnosed with schizophrenia, as well as a group of participants with no known neurological disorder.
-  Classification was done using traditional methods and MLP to classify the participants as belonging to disease or control subjects.
-   LOSO evaluation done with this proven MLP configuration using carefully and intentionally corrupted data clearly indicate that for disease diagnosis, the k-fold classification result is misleading. Therefore, evaluation of any scalp recorded EEG based disease classification method
must use a LOSO style cross-validation.

## 1 Introduction:
- Schizophrenia is a neurological disorder Symptoms include challenges in perception or perception of reality.
- In this study, we use a multilayer perceptron (MLP) to show importance of Leave-One-Subject-Out (LOSO) cross validation machine learning and how MLP is effective in making use of clean EEG data in mining out the features important for disease classification.

## 2 Data EEG Acquisition and Pre Processing
### 2.1 Participants:
- The study had 632 participants and each performed 10 different
tasks whilst recording EEG.
-  A subset of the data from 30 subjects were selected for the study described in this paper.

### 2.2 Data Acquisition:
- An EEG system with 128 channels and the Neuroscan ‘Quick cap’ or the Falk Minnow ‘Easy-cap’ were used to record the EEG data from participants at a sampling rate 2000 Hz with 500 Hz low-pass filter.
- The data from the Quick-cap were interpolated to match with the 10–20 positioning of the Easy-cap electrodes. This enabled the data from both caps to be analysed together.
-  To minimise electromagnetic noise, participants were seated in a Faraday cage.
-  A custom-built response panel was used to record participants’ manual responses.
-  EEG was recorded while subjects undertook mental tasks.The current study includes data from two mental tasks: resting eyes-open and maze. For eyes-open task, participants were looking at a black screen with a white cross positioned one metre in front of them with their eyes-open for 40 s
-  For the maze task, participants were asked to learn and memorise a hidden pathway embedded within a maze presented on a computer screen.

### 2.3 Artefact Removal:
- Faulty channels were determined using three different methods: probabilistic (threshold = 5), kurtosis (threshold = 5), and spectra (threshold = 2, 20 75 Hz).
- The probabilistic method uses joint probability on the data from each channel separately to calculate the entropy of the data. The joint probability values are then normalised via the subtraction of the mean, and the division of the standard deviation. If the resulting normalised joint probability values (one per channel) exceed a threshold, then the corresponding channels are labelled for rejection.
- The kurtosis method uses the same methodology as the probabilistic method,but uses discrete kurtosis rather than joint probability. The spectra method performs a spectral analysis using Welch’s modified periodogram.
- Artefact contaminated EEG data was then rejected by separating the data into epochs and flagging data as being artefactual, if two contiguous epochs exceeded a threshold (threshold = 10, Hamming taper).
- The data was then demeaned again to account for the artefact correction.This data is referred as “clean” data and used for this study.

### 2.4 Data-Set for Current Study:
- In eyes open task, there were 30 subjects. Each subject had 5 to 8 non overlapping, 5 s epochs making the total data points 207. The number epochs varied due to the rejection of epochs with bad data from the 40 s task. Importantly, each epoch was non-overlapping, that is each epoch was unique and there was no data leakage between each epoch.
- Data from 45 electrodes in 5 bands (delta: 1–4 Hz, theta: 4–8 Hz, alpha: 8–13 Hz, beta: 13–25 Hz and gamma: 25 Hz) was used and this results in 225 (45 × 5) features. This make the data-set dimension 207 × 225.
-  Similarly, maze task data is of shape 1181 × 195.
-  For the leave one subject out (LOSO) classification experiment, all data from all subjects was used for training except one, which was used for testing purposes. Where as for K-fold entire data set was split into 9:1 ration for each fold of training and testing.

## 3 Method
### 3.1 Multi-Layer Perceptron:
- It uses a supervised learning process called back propagation to train the model.
- a feed forward network consists of input layer, output layer and an arbitrary number of layers in between called hidden layers.
- Nodes of each hidden layer of an MLP are connected to every node in the previous and following layer.
- The weights carried by these connections represents the strength of the connection. These weights are typically initialized randomly. Learning is a process by which MLP network determines which network connection weights best reduce the difference between true and calculated outputs.
- A MLP with 4 layers was used in this study. An input layer, 2 hidden layers, with 12 and 8 hidden units respectively and an output layer were used for this study.
- The ReLU was used as the activation function for input and hidden layers. The sigmoid was the activation function used for the output layer. The Loss function used was the binary-cross entropy and Adam as the optimizer

### 3.2 Machine Learning Method:
- The study has two parts: the first part was testing the effectiveness of MLP and the second part evaluating the necessity of LOSO cross validation.
- The study used Random Forest (RF), Logical Regression (LR), Linear discriminant analysis (LDA), Support vector machine (SVM) with linear and RBF kernel to confirm the study findings.
- The first part of the study was to understand how effective MLP is in identifying people with Schizophrenia using the scalp recorded EEG. Primarily, the maze task data was used for this part as there were more samples for maze compared with eyes open data task.
- The same data-set was used for classification using the ensemble method Random Forest  and the results were compared with that of MLP.
- The second and main part of the study was to determine differences in performance of a classification algorithm when k-fold cross validation and LOSO cross validation were used.
- The eyes-open task was used for this part of the study. To begin with, data was used on MLP based disease classification where 10-fold cross validation was employed. Then the same data was used to train an MLP using LOSO cross validation.
- For leave one subject out (LOSO) cross validation experiment, all data from all subjects was used for training except one, which was used for testing purpose. The size of training and testing data-set is approximately 200:7.
- This process was repeated for each subject being kept aside for testing purposes constituting one round. To get an average measure of accuracy, 100 rounds of such training and testing were completed.
- For K-fold cross validation data samples were separated in 9:1 ratio where 90% samples (approx. 185) were used for training and 10% (approx. 20) were used for testing in each fold until every data is used for testing in one of the fold, this process repeated for 100 rounds for an average result.

## 4 Results
### 4.1 Effectiveness of MLP in Disease Classification:
- for this part “clean” data from the maze task was used.
- RF, LDA,SVM-L and SVM-RBF were used for comparing the result with an MLP. LOSO cross validation method was used for classification and 100 rounds of training were executed to get the mean accuracy and standard deviation.
- mean accuracy of MLP was better than others.
### 4.2 LOSO Versus K-Fold Cross-Validation:
- This part of the study was also performed using “clean” data from the eyes open task.
- Five classification experiments were done to show the need for of LOSO when evaluating disease classification algorithms.
- First, 10-fold cross validation was used to show the accuracy in which data from all subjects were used in training, such that even though the individual data instances were distinct, the same subject appears in both training AND testing data.
- The second exercise was done with LOSO cross-validation. In order to determine if the algorithm was learning from the disease features, rather than subject features, an experiment with corrupted class labels was undertaken.

## 5 Discussion
- The effectiveness of MLP in disease learning was evaluated in the first part of the study.
-  In this, clean schizophrenia maze data was processed using 4 layer MLP. The result shows that with clean data, the MLP classifier is able to discern the disease group subjects from the control group based on EEG.
-  From the t-test results, it can be seen that MLP is significantly better than RF and LDA, and comparable with LR, SVM-L and SVM-RBF results.
-  LOSO evaluation methodology was evaluated in the second part of the study.
-   Results from k-fold evaluation shows that if data from all subjects are used for training the model almost certainly (98%) can detect subjects with disease.
- In this case, training and testing data is not separated in terms of subjects, leaving data related to a subject in both places.
- A more realistic scenario, what is required is to classify a new unseen subject into one of the classes.
- With all other experimental aspects remaining the same, when the k-fold validation technique is changed to LOSO the accuracy decreased significantly to 70%. This likely means that in the case of k-fold where a subject data is in both training and testing partitions, the algorithm is learning the subject rather than the disease condition.
- These results clearly indicate that for disease diagnosis, the k-fold classification result is misleading. Therefore, evaluation of any scalp recorded EEG based disease classification method must use a LOSO style cross-validation.