# LOSO Cross-Validation For EEG Disease Diagnosis

## Introduction
- Most neurological disorder classification studies uses traditional machine learning algorithms like Support Vector Machine (SVM), Bayesian Gaussian-process logistic regression, and discriminant analysis.
- This study uses a multilayer perceptron (MLP) to show the importance of Leave-One-Subject-Out (LOSO) cross-validation and demonstrates how MLP effectively uses clean EEG data for disease classification.

## Data EEG Acquisition and Pre Processing

### Participants

- Data for this study were collected at Flinders Medical Centre (2003-2006) with 632 participants, each performing 10 EEG tasks. The Flinders Clinical Research Ethics Committee approved the reanalysis. - This study used data from 30 subjects (15 with schizophrenia and 15 controls), focusing on eyes-closed and maze tasks.

###  Data Acquisition

- An EEG system with 128 channels recorded data from participants at 2000 Hz with a 500 Hz low-pass filter.
- Participants were seated in a Faraday cage to reduce electromagnetic noise. Visual and auditory instructions were given via a computer, and responses were recorded with a custom-built response panel.
- This study used data from two tasks: resting eyes-open and maze. 
- For the eyes-open task, participants looked at a black screen with a white cross for 40 seconds.
- For the maze task, participants learned and memorized a hidden path in a maze on a computer screen, using directional buttons to move the cursor.

### Artefact Removal

- To remove the artefacts, they found the faulty channels using three different methods :
probbilistic, kurtosis, spectra.
- Then the data was epoched, and the faulty channel's data was marked as artefactual. The data was then 'demeaned' again to make it clean.

### Data-Set for Current Study
![image](https://github.com/aarsh-12/BCS_Drowsiness_Detection/assets/169232982/6c4d3d0f-8448-426b-80e2-70ef5fdacf50)

## Method

### MLP
- A Multi-Layer Perceptron (MLP) is a deep learning model with an input layer, output layer, and hidden layers. It uses backpropagation for training. Each layer's nodes connect to nodes in the previous and next layers.
- This study used an MLP with four layers: an input layer, two hidden layers (12 and 8 units), and an output layer. The ReLU activation function was used for the hidden layers, and the sigmoid function for the output layer. Binary cross-entropy was the loss function, and Adam was the optimizer. 
- Experiments with different layers, units, and activation functions like softmax, tanh, and Leaky ReLU showed no improvement over ReLU and sigmoid.

### Machine Learning Method
- The study aimed to check how efficient each method was to identify Schizophrenia. It had two parts: testing the effectiveness of MLP and evaluating the necessity of LOSO cross-validation.
- It had two tasks : maze and eyes-open
- It used the following algorithms : MLP, Random Forest (RF), Logical Regression (LR), Linear Discriminant Analysis (LDA), Support Vector Machine (SVM) with linear and RBF kernels.
- For data processing it cleaned and standardized EEG data, randomized training set, set no seed for random weight initialization.
- The MLP model had best performance with 2 hidden layers (12 and 8 units), Adam optimizer, ReLU for hidden layers, sigmoid for output layer, 150 epochs, and batch size of 10.
- The first part of the study was to understand how good was MLP to identify SChizophrenia from EEG, the maze task was used primarily for this study.
- The second and main part of the study was to determine differences in performance of a classification algorithm when k-fold cross validation and LOSO cross validation were used. The eyes-open task was used for this study.
- Model was also tested with corrupted label-data to ensure the model learned disease condition.
- For LOSO it Trained on all subjects except one, and this was repeated for each subject.
- For K-fold cross validation data samples were separated in 9:1 ratio where 90% samples
were used for training and 10% were used for testing.

## Results

![image](https://github.com/aarsh-12/BCS_Drowsiness_Detection/assets/169232982/3dd9dc46-67e0-4700-b82d-7156bd061ebb)

![image](https://github.com/aarsh-12/BCS_Drowsiness_Detection/assets/169232982/25da6113-fa1d-42b6-85fe-031a034d10a2)

## Discussion

### MLP
- Clean schizophrenia maze data was processed using a 4-layer MLP.
- Results showed MLP could distinguish disease subjects from controls based on EEG.
- Despite a small dataset (20 subjects, 195 features, 1181 samples), MLP showed promising results.

### LOSO and k-fold cross validation
- *K-Fold Results*: Showed 98% accuracy but included the same subject in both training and testing, leading to high accuracy due to learning subject-specific features.
- *LOSO Results*: Showed a realistic scenario where new, unseen subjects were classified, with accuracy dropping to 70%.
- *Corrupted Data Tests*: Confirmed that K-fold learned subject-specific features, not disease features. Corrupted subject-wise data gave 98% accuracy in K-fold but only 30% in LOSO, indicating K-fold's misleading high accuracy.

### Conclusion
- K-fold cross-validation can be misleading for disease diagnosis.
- For EEG-based disease classification, LOSO cross-validation is necessary to ensure realistic and reliable results.







