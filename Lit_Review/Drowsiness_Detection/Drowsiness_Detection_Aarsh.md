# EEG-based Cross-Subject Driver Drowsiness Recognition with an Interpretable CNN 
### Introduction 

- Driver's drowsiness has been a major issue leading to car accidents. This shows the need for a system to detect drowsiness levels in a person. 
- EEG is a practical method for detecting drowsiness due to its high resolution and low cost, but variability in signals across different people makes it challenging. 
- Traditional methods use hand-crafted features, which may miss important information. Deep learning, especially CNNs, can learn directly from raw data but the details on their exact working in EEG based models is still a bit underexplored.
- In this paper, they have talked about implementing a novel Convolutional Neural
Network (CNN) named “InterpretableCNN” for the task.

### Existing models

- The existing models in some cars detect a drivers drowsiness through camera-based, driver behaviour based and physiological signal-based methods.

- But EEG based model would be able to detect it before the driver starts showing the drowsy behaviuors.

### EEG-Based model

- Research shows a link between drowsiness and EEG patterns, such as increased Theta (4-7.9 Hz) and Alpha (8-11.9 Hz) band power during drowsiness.
- They further concluded that the increase in lower Alpha power occurs only when subjects
are struggling not to sleep, while the Alpha power will decrease when subjects fall asleep.

## MATERIALS AND METHODS

### Data Preparation

- They used a public EEG dataset from 27 subjects aged 22-28 during a virtual reality driving task, where they responded to lane-departure events.
- Each sample was labeled based on reaction times (RT) to the events: "alert" if RTs were short and "drowsy" if RTs were long. Sessions with fewer than 50 samples per class were discarded, resulting in 2952 samples from 11 subjects.
- To create a balanced dataset for training, we selected representative samples from each class, ensuring fair training conditions.

### Netork Design

#### Core Idea

- EEG data we recieve is often contaminated with several artifacts. To enhance data quality for accurate recognition, spatial filtering techniques are employed. These techniques extract new signals from raw EEG recordings with minimal contamination and redundancy.
- $$s_j = \sum_{i=1}^{m} w_{i,j} x_i + b_j$$
- We use the above equation to transform our EEG signals from m electrodes to N1 new signals, where the w matrix is the set of spatial filters.
- One such technique is Independent Component Analysis (ICA), which derives spatial filters based on the statistical independence of source signals. 
- From this cleaned data, we extract features to be used for classification.

#### Context Of Separable Convolution

-In our approach, we utilize pointwise convolution for the initial step (1) to demix signals and depthwise convolution for the subsequent step (2) to independently learn temporal features from each demixed signal.

#### Network structure
![image](https://github.com/aarsh-12/BCS_Drowsiness_Detection/assets/169232982/5e1f5de8-49b2-4b59-938c-78181d045fb8)

- The network consists of seven layers and its structure is shown in Fig. 1. The pointwise convolution and depthwise convolution are implemented in the first two layers, which are followed by a ReLU activation layer, a batch normalization layer, a global average pooling layer, a dense layer and a
Softmax activation layer. 

- This "InterpretableCNN" model enhances interpretability of EEG-based driver drowsiness detection, leveraging depthwise separable convolution for efficient feature extraction and classification.

### Interpretation Techniques

- Deriving insights into the characteristics of EEG signals learned by deep learning networks is crucial for validating models, ensuring they capture relevant features and potentially uncovering neurophysiological patterns related to mental states. 
- Existing methods for interpreting EEG signal classification models include visualizing kernel weights, summarizing hidden unit activations, and calculating feature relevance. However, these techniques often fail to explain specific characteristics of individual EEG samples or address noise impact.
- the Class Activation Map (CAM) method is a powerful interpretation technique that can localize
the discriminative regions of each input sample for a CNN model trained to solve a classification task.
- However, CAM is designed for CNNs with standard convolutional layers and does not directly apply to models like ours, which involve pointwise convolutions in the initial layer, altering the alignment of activation maps.
- To address this, inspired by the CNN-Fixation method, a new way to interpret the model is proposed. This technique identifies the most important spots in the activation map that aid in model classification. These spots are then traced back to the corresponding areas in the original EEG sample using weighted sums. By focusing on the top important spots, a heatmap is created that highlights the key parts of the input signal relevant for classification, providing a clearer understanding of how the model makes decisions.

### Methods For Comparison

#### Deep Learning Methods

#### EEGNet
- Uses 2D convolution and depthwise layers.
- Tested on various EEG datasets and shown to be effective for driver drowsiness detection.

#### Sinc-ShallowNet
- Features a sinc-convolutional layer and depthwise layers.
- Includes a variation called Conv-ShallowNet with a standard convolutional layer for comparison.

#### Conventional Base line Methods

#### RelativePower:
Calculates the relative power of Delta, Theta, Alpha, and Beta bands from EEG channels.

#### LogPower:
Computes the natural log of band power features.

#### PowerRatio:
Uses ratios of different band powers as indicators of drowsiness.

#### WaveletEntropy:
Extracts wavelet entropy features using the Mexican Hat Wavelet.

#### FourEntropies:
Combines sample, fuzzy, approximate, and spectral entropy features.

#### Variations in comparison
They compared the model with its variations to understand the impact of each component.
- 1DConv: Replaces separable convolutions with a standard 1D convolutional layer.
- NoDepthwise: Removes the depthwise convolutional layer.
- NoPointwise: Removes the pointwise convolutional layer.
- NoBatchNorm: Removes the batch normalization layer.

### Evaluation on The Proposed Method
A leave-one-subject-out cross-validation was conducted to compare the classifiers. In this method, data from one subject is used for testing while data from others is used for training. This process is repeated for each subject.

#### Mean Accuracy on Balanced Dataset:

- Each model was trained for 1 to 50 epochs, with the process repeated 10 times for each epoch, resulting in 110 folds per epoch.
- InterpretableCNN outperformed its variations, with separable convolution and batch normalization contributing positively to its performance.

#### Mean Accuracy of Conventional Methods:

- LogPower+GNB achieved the highest accuracy at 72.68%.
- SVM was the best classifier for RelativePower, PowerRatio, and FourEntropies.
- Logistic Regression performed best with WaveletEntropy, achieving 60.40%.
- Band power methods (RelativePower, LogPower, PowerRatio) generally performed better than entropy-based methods.

![image](https://github.com/aarsh-12/BCS_Drowsiness_Detection/assets/169232982/f02e8875-2534-4333-96c4-4eae87acb324)

![image](https://github.com/aarsh-12/BCS_Drowsiness_Detection/assets/169232982/bfda7b87-99bf-441e-8c6f-38c6b9134b0b)

![image](https://github.com/aarsh-12/BCS_Drowsiness_Detection/assets/169232982/75f833a7-ed6a-43f3-a79e-7c7f4181133c)

#### Interpretation on the learned characteristics from EEG signals

- The study explores using interpretable deep learning models to analyze EEG signals across subjects to distinguish between alert and drowsy states. 
- The model identifies Alpha spindles and Theta band bursts as indicators of drowsiness, and Beta waves from peripheral channels and EMG activities as indicators of alertness. 
- Artifacts occasionally present in drowsy signals can mislead the model. The study proposes an interpretation technique inspired by CAM and Fixation-CNN methods to explain the model's decisions. 
- Improving preprocessing to handle artifacts like sensor noise is crucial, while reconsidering how samples are labeled could enhance classification accuracy. 
- Future work aims to interpret deep learning models more comprehensively for calibration-free brain-computer interfaces.

## Conclusion
- Developed a new CNN model to study EEG signals and detect drowsiness.
- Used a compact design with special techniques to process EEG data over time and space.
- Created methods to show which parts of the data the model uses to make decisions.
- Showed the model performs better than other methods for recognizing drowsiness across different people.
- Found important features like Alpha spindles that help tell if someone is drowsy or alert.
- Explored why some signals were misclassified and how to fix these issues.
- Shows a promising way to understand complex EEG data for making brain-computer interfaces without needing calibration.





















