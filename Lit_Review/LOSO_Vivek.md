Schizophrenia is a neurological disorder with a strong hereditary component that
has been found to affect 1% of the population

**DATA ACQUISITION**
In this study, we use a multilayer perceptron (MLP) to show importance of Leave-One-Subject-Out (LOSO) cross validation machine learning and how MLP is effective in making use of clean EEG data in mining out the features important for disease classification

An EEG system with 128 channels were used to record
the EEG data from participants at a sampling rate 2000 Hz with 500 Hz low-pass
filter.

**Data Preprocessing and Artifact Detection**
The data was resampled and detrended using the SIFT toolbox. The time segment length was set to 0.33 seconds with a step size of 0.082 seconds. EEG data was then re-referenced.

Three methods were used to detect faulty channels:
**Probabilistic method** – joint probability of each channel calculated then normalised by subtracting mean and division by standard deviation then if normalised value exceeds threshold, rejected
**Kurtosis method** – same method but uses discrete kurtosis rather than joint probability
**Spectra method** – spectral analysis using Welch’s modified periodogram

The probabilistic method was used to remove channels permanently, while the kurtosis and spectra methods were used for subsequent artifact reduction due to their sensitivity.

**Dataset for Current Study**
- **Eyes Open Task**: 30 subjects, 5 to 8 epochs of 5 seconds each, totaling 207 data points. The data included 45 electrodes and 5 bands, resulting in 225 features. Dataset dimension: (207, 225).
- **Maze Dataset**: 22 subjects, 39 electrodes, and 5 bands, totaling 1181 data points. Dataset dimension: (1181, 195).


**MLP**
The MLP is a feed-forward network that uses backpropagation to learn. It consists of an input layer, two hidden layers (with 12 and 8 units), and an output layer. Each node is connected to every node in the previous and next layers, with no intra-layer connections. Weights are initialized randomly and adjusted during learning. The activation functions used are ReLU for the input and hidden layers, and sigmoid for the output layer. The loss function is binary cross-entropy, and the optimizer is Adam.

**STUDY**
The study was conducted in two parts. The first part tested the effectiveness of a Multi-Layer Perceptron (MLP), and the second part evaluated the necessity of Leave-One-Subject-Out (LOSO) cross-validation.
In the first part, a maze task was used, while in the second part, an eyes-open condition was employed. The EEG data was standardized by removing the mean and scaling to unit variance. The MLP was trained for 150 epochs with a batch size of 10.
To ensure the model was learning the disease and not the subject, it was trained with corrupted label data, where labels were mislabelled both subject-wise and sample-wise.
For the LOSO cross-validation, one subject was used for testing and 29 for training, with accuracy averaged over 100 trials. For k-fold cross-validation, a 9:1 train-test ratio was used, with accuracy also averaged over 100 trials.


**RESULTS**
The MLP achieved a mean accuracy of 85%. K-fold cross-validation performed better than LOSO with the original data, but since it splits data such that the same subject's data can appear in both training and test sets, it may learn subject-specific features rather than the disease condition. To verify this, the data was corrupted subject-wise. The k-fold method still showed high accuracy, while LOSO's accuracy decreased, indicating that k-fold was learning the subjects, whereas LOSO was learning the disease condition.