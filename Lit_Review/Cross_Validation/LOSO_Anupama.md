Introduction 
* Schizophrenia – neurological disorder – symptoms include challenges in perception, delusions, lack of motivation 
* A multilayer perceptron (MLP) is used to show the importance of LOSO cross validation and how effective MLP is in feature extraction for disease classification 

Data EEG acquisition and preprocessing 
* Participants 
    * All data: 632 participants, 10 tasks 
    * A subset of 30(15+15) subjects’ data doing 2 tasks used for study 
* Data acquisition 
    * Quick cap and easy cap used, but data from quick cap later interpolated to match 10-20 standard 
    * Sampling rate 2000Hz, 500Hz low-pass filter 
    * Faraday cage used to minimise EM noise 
    * Two tasks: resting eyes-open (keep eyes open for 40s), maze (traverse maze using memorised pathway) 

* Artefact removal 
    * Data was resampled, detrended using the SIFT toolbox 
    * Time segment length = 0.33s, step size = 0.082s 
    * EEG then re-refererenced  
    * 3 methods to detect faulty channels probabilistic (threshold = 5), kurtosis (threshold = 5), and spectra (threshold = 2, 20 75 Hz) 
    * Probabilistic method – joint probability of each channel calculated -> normalised by subtracting mean and division by standard deviation -> if normalised value exceeds threshold, rejected 
    * Kurtosis method – same method but uses discrete kurtosis rather than joint probability 
    * Spectra method – spectral analysis using Welch’s modified periodogram 
    * Probabilistic method used to remove channels permanently 
    * Other two methods used for subsequent artefact reduction step as they are overly sensitive 
*Dataset for current study 
    * Eyes open task – 30 subjects – 5to8 5s epochs for each subject – total 207 data points 
    * 45 electrodes, 5 bands = 225 features 
    * Data set dimension (207,225) 
    * Similarly, maze dataset (1181,195) - 39 electrodes, 5 channels, 22 subjects 

Method 
* MLP  
    * Feed forward network, uses backpropagation to learn 
    * Input layer + hidden layers + Output layer 
    * Every node connected to every node of prev and next layers 
    * No intra layer connections 
    * Weights initialized randomly, learning = adjusting weights 
    * 4 layers – Input + 2 hidden (12 + 8 hidden units) + Output layer 
    * Activation function – ReLU for input, hidden, sigmoid for output 
    * Loss function – binary cross entropy 
    * Optimizer – adam 

* Machine learning method 
    * two parts: the first part was testing the effectiveness of MLP and the second part evaluating the necessity of LOSO cross validation 
    * maze for the first and eyes-open for the second part of the study 
    * EEG was standardised by removing the mean and scaling to unit variance 
    * 150 epochs and a batch size of 10 
    * To make sure model was learning the disease and not the subject, it was trained with corrupted label data – subject wise and sample wise mislabelled 
    * LOSO: one subject for testing, 29 for training. Accuracy averaged over 100 trials 
    * k-fold cross validation: 9:1 train test ratio. Accuracy averaged over 100 trials 

Results
* MLP performs better with mean accuracy of 85%
* Using K-fold seems to perform much better than LOSO with original data. However, data split during k-fold leaves data from the same subject in both training and test data.  This might mean that K-fold is learning the subject and not the disease condition. To verify, data was corrupted subjectwise. Corrupted datal gives high accuracy with k-fold and decrease in accuracy with LOSO. Hence, we conlude that the k-fold method was learning the subjects and LOSO was learning the disease condition.  