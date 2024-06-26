# EEG-based Cross-Subject Driver Drowsiness Recognition with an Interpretable Convolutional Neural Network

## Introduction:
-  In the past many efforts have been made to investigate monitoring of driver drowsiness using electroencephalogram (EEG), which is believed to be the most practical  modality for capturing brain dynamics due to its high temporal resolution and low cost.
-  However,the main problem is  building a calibration-free drowsiness recognition system is still a challenging task. The difficulty lies in capturing common drowsiness-related patterns from a diversity of EEG signals with a low signal-to-noise rate.
-  deep learning allows end-to-end learning without the need for a prior feature crafting. Such models can directly learn essential characteristics from raw high-dimensional data.
-  However, existing work in the area of EEG signal processing mostly treats deep learning models as black-box classifiers, while what have been learned by the models and to which extent they are affected by the noise from EEG data are still underexplored.
-  This paper proposes a novel Convolutional Neural Network (CNN) named “InterpretableCNN” for driver drowsiness recognition and discovering common drowsiness related patterns of EEG signals across different subjects.

## Related Works:
#### A. Existing driver monitoring systems:
- Driver monitoring system is a safety system installed on 
vehicles for monitoring the alertness of drivers and making 
alarm when the driver gets drowsy or falls asleep.
-  camera-based, driver behavior-based and physiological signal-based methods are primarily used by car manufacturers for drowsiness detection.In comparison to existing methods, EEG has the advantage of directly monitoring brain activities with a high temporal resolution, so that it allows drowsiness to be detected in an early stage before it is reflected from the driver behaviors.

#### B. EEG-based driver drowsiness recognition:
- EEG measures voltage difference on the scalp, which is 
resulted from ion currents 
- Existing EEG systems have 1 to 256 electrodes, and the placement of electrodes follows a formal standard called 10–20 system or International 10–20 system.
- EEG channels follow an alphanumeric naming convention. The channel name starts with one- or two-letter acronym and ends with a number or letter "z", e.g., AF3, Cz, and T4. Letter Fp, F, T, P, O, and C stand for pre-frontal,frontal, temporal, parietal, occipital and central, respectively.The ending digit denotes the placement of the electrode on the coronal line, while "z", standing for zero, denotes the center of the coronal line.
- drowsiness can in general cause an increase in power of the 
Theta and Alpha frequency bands. They further concluded that 
the increase in lower Alpha power occurs only when subjects 
are struggling not to sleep, while the Alpha power will decrease 
when subjects fall asleep.

## Materials And Method:
#### Data preperation:
- A public EEG dataset  was used in the study. The dataset was collected from 27 subjects (aged from 22 to 28) in a sustained-driving task in a virtual reality simulator.
- In the process, lane-departure events were randomly introduced which drifted the car away from the central lane. The participants were required to respond immediately to the events by driving the car back to central lane. The drowsiness level can be reflected by how fast the subjects respond to the events
- The EEG signals were sampled at 500 Hz with 30 electrodes 
and processed with 1-50 Hz bandpass filters and artifact 
rejection.
- We further down-sampled the original data to 128 Hz and extracted the EEG samples of 3-second length prior to the car deviation events for each trail.
- Each sample has a dimension of 30 (channels) × 384 (sample points). We followed methods described in to select and label the EEG samples. Specifically, the local reaction time (RT), which is the time taken by the subject to respond to the car drift event, and the global-RT, which is the average of RTs within a 90-second window before the car drift event, were 
calculated for each sample.
- Samples with both local-RT and global-RT shorter than 1.5 times alert-RT were labeled as alert state, while samples with both local-RT and global-RT longer than 2.5 times alert-RT were labeled as drowsy state.

### Network Design:


![Screenshot 2024-06-26 085603.png](./Screenshot%202024-06-26%20085603.png)


#### 1) The core idea:
- The EEG signals can be viewed as a mixture of cortical source signals generated from different areas of the brain. However, the recorded data are inevitably contaminated by artifacts caused by different electrical activities.
- Considering learning directly from the noisy and redundant EEG data usually leads to unsatisfactory recognition results, spatial filtering techniques were proposed to improve the data quality by extracting a set of new signals from the raw multi-channel recordings of EEG with minimal contamination and redundancy.
- Suppose the EEG signals recorded from m electrodes are {𝒙𝒊}𝑖=1,2…𝑚. 𝑁1 new signals {𝒔𝒋}𝑗=1,2…𝑁1 can be obtained from linear combination of the original m signals.

![Screenshot 2024-06-26 090111.png](./Screenshot%202024-06-26%20090111.png)
- In the above fig. the weights {𝑤𝑖,𝑗} are a set of spatial filters, which can be calculated based on various independent evaluation criteria such as distance measure, information measure, dependency measure, and consistency measure.
-  Since the obtained new set of signals {𝒔𝒋} are expected to contain minimal noise and redundancy, a set of features can be thus extracted from each new signal 𝒔𝒋 to be used for classification.

#### 2) The context of separable convolution :
- The proposed processing sequence of EEG signal is similar to the concept of depthwise separable convolution,with the purpose of reducing parameters and encouraging convergence of the network.
- A depthwise separable convolution, or called “separable convolution”, consists of a depthwise convolution, which is performed on each channel independently, and a pointwise convolution (or called “1x1 convolution”),which projects the channels onto a new space.
- In the context of image classification, the depthwise separable convolution is different from a standard 2D convolution in the aspect that it independently learns the spatial correlations (consisting of width and height of an image) and the cross-channel correlations with the depthwise and pointwise convolutions, respectively, instead of simultaneously learning the parameters in a 3D space
- For our case, we use the pointwise convolution to implement
the first processing step (1) of demixing the signals and the 
depthwise convolution to implement the second processing step 
(2) of learning temporal features from each demixed signal
independently.

#### 3) Network structure:
- The network consists of seven layers and its structure is shown in above  Fig. 
- The pointwise convolution and depthwise convolution are implemented in the first two layers, which are followed by a ReLU activation layer, a batch normalization layer, a global average pooling layer, a dense layer and a Softmax activation layer.
- In the first layer, we use 𝑁1 pointwise convolutional nodes to generate 𝑁1 new channels of signals with the same length. For a given input sample 𝑿(𝒎,𝒏), which contains m (=30) channels of 1-dimensional signal with length of n (=384). The i-th (1 ≤𝑖 ≤ 𝑁1) pointwise convolutional node has m weights {𝑤𝑖,𝑝(1)}𝑝=1,2,… ,𝑚 and 1 bias 𝑏𝑖(1) parameter.
- the output from the first layer is:

![Screenshot 2024-06-26 091820.png](./Screenshot%202024-06-26%20091820.png)
- We set 𝑁1=16, which is around half length of the input channels, in order to reduce redundancy and encourage convergence of the network
- In the second layer, depthwise convolutions are used to extract features from the 𝑁1 obtained signals. Specifically, each new signal 𝒉𝒊(𝟏) is convoluted with two nodes in the second layer. Since there are 𝑁1 channels of new signals output from the first layer, we have in total 2𝑁1 depthwise convolutional nodes.
- Suppose the length of the kernel is l, the i-th (1 ≤ 𝑖 ≤ 2𝑁1) node has weights {𝑤𝑖,𝑟(2)}1≤𝑟≤𝑙 and 1 bias 𝑏𝑖(2)parameter.
-  The output of the layer is:

![Screenshot 2024-06-26 092906.png](./Screenshot%202024-06-26%20092906.png)
- The 3rd and 4th layers are activation and batch normalization layers.

###  Interpretation technique:
- Deriving insights on what characteristics of EEG signals arelearned by the deep learning networks has become an important procedure of model validation, since it not only allows us to find out whether the classification is driven by relevant features in the data, but also potentially discover interesting neurophysiological patterns associated with different mental states.
- By comparison, the Class Activation Map (CAM) method is a powerful interpretation technique that can localize the discriminative regions of each input sample for a CNN model trained to solve a classification task.
- Suppose a given input EEG sample 𝑋(𝑚,𝑛)is classified with label c, where c is either 0 or 1 representing the alert or drowsy state, respectively. The objective is to find the heatmap 𝑆(𝑚,𝑛)𝐶 for 𝑋(𝑚,𝑛)that can reveal important regions for the prediction by the network. Suppose an inpu signal 𝑋(𝑚,𝑛)generates activation ℎ𝑐 (6) in the 6th layer of the network.


![Screenshot 2024-06-26 100733.png](./Screenshot%202024-06-26%20100733.png)

- The objective is to trace each of these discriminative locations 
for class c in 𝑀𝑖,𝑗 𝑐 throughout the network to the center of areas  in the input sample that contribute most to these high activations.
- The final heatmap for sample 𝑋(𝑚,𝑛) can be obtained by combining all the class discriminative points in the input sample with the Gaussian function.


![Screenshot 2024-06-26 101038.png](./Screenshot%202024-06-26%20101038.png)

### Methods for comparison:
#### 1) Deep learning methods:
- The first deep learning model  used for comparison is the benchmark CNN model for EEG signal classification-EEGNet proposed by Lawhern et al.
- EEGNet uses a 2D convolutional layer to filter the raw signals, which is followed by a spatial depthwise convolutional layer and a temporal depthwise convolutional layer to extract features. The model was tested on several Brain Computer Interface (BCI) datasets and achieved higher accuracies than conventional methods.
- The second deep learning model  used for comparison is the Sinc-ShallowNet model proposed by Davide et al. The model has a sinc convolutional layer and a depthwise convolutional layer to process the raw EEG data in a temporal-spacial sequence.
- In addition,the paper  also talks about the  implementation of a variation of the model named “Conv-ShallowNet”, which replaces the sinc-convolutional layer with a standard convolutional layer for comparison.

#### 2) Conventional baseline methods:
- Conventional methods for EEG signal classification mainly involve the stages of feature extraction and feature classification.
- In order to have a comprehensive understanding on the performance of different conventional methods on the dataset, paper  implemented five baseline methods for feature extraction and test them on eight different classifiers for comparison.
- EEG band power features have been regarded as golden standard for EEG signal classification. For driver drowsiness recognition, many works  have found a strong relationship between drowsiness and band power features of EEG signals.Therefore, the first three baseline methods use different forms of band power features, which are relative band power features, log of band power features , and the ratio of band power features . The fourth baseline method uses the wavelet entropy features , while the fifth baseline method uses a combination of four entropies features , which are sample entropy, fuzzy entropy, approximate entropy and spectral entropy.

#### 3) Variations of the model for comparison:
- The proposed model is compared with its variations in order 
to understand how each part of the model influences its overall 
performance. 
- Firstly, in order to evaluate the benefits of using the separable 
convolution over the standard 1-dimensional convolution, we 
replace the pointwise and the depthwise convolutional layers of 
the network with a standard convolutional layer containing 32 
kernels with length of 64. We name this model as “1DConv”
- In the second and the third variations, we remove the 
depthwise convolutional layer and the pointwise convolutional 
layer, respectively, in order to understand how these two layers 
contribute to the final classification. We name these model as 
“NoDepthwise” and “NoPointwise”, repectively.
- Finally, we consider a variation of the model, where the batch 
normalization layer is removed. We name the model as 
“NoBatchNorm”.

### Implementation details:
- initial tests showed that all these deep learning models have a fast converge followed by a significant drop on the accuracies for this dataset when using the default batch normalization layer provided by both the Pytorch and TensorFlow libraries.
- In order to solve the problem, we conducted minor modifications on all the comparison models by disabling estimation of the computed mean and variance.
- For training of the neural network models, although different optimizers have been used in various deep architectures, such as Sobolev gradient based optimizers, we used Adam due to its low computational cost and efficiency in our technique.
- As for the conventional methods, band power features were extracted using the Welch method from the SciPy library . The classifiers were implemented with the sklearn library and the default parameters were used.

## Evalution On the Proposed Model
### A. Model comparison results:
- conducted leave-one-subject-out cross validation to compare the classifiers.
- Specifically, the EEG data from one subject are used for testing, while data from all the other subjects are used for training the classifiers. The process is iterated until every subject serves once as the test subject.
- considered the ideal case in Section 1), where the balanced dataset is used for a standard evaluation on the performance of different classifiers. In Section 2), we compare selected classifiers on the unbalanced dataset, which is closer to the real life case.

### 1) Mean accuracy comparison on the balanced dataset:


![Screenshot 2024-06-26 150621.png](./Screenshot%202024-06-26%20150621.png)



![Screenshot 2024-06-26 150638.png](./Screenshot%202024-06-26%20150638.png)


- compared the mean accuracies of different classifiers on the balanced dataset. We trained each deep learning model from 1 to 50 epochs. Considering neural networks are stochastic, we randomized the network parameters for each iteration and repeated the process for 10 times. In this way, 10 (times) x 11 (subjects) = 110 folds were created for each epoch.
- The mean classification accuracies of the proposed model InterpretableCNN and the benchmark deep learning models against training epochs from 1 to 50 are shown in Figure.
- As it can be seen in the figure, InterpretableCNN has an overall 
better performance than the other four models.
- The results indicate that the class discriminative EEG features contained in this dataset could be well captured by shallow neural networks, since the both the InterpretableCNN and ShallowNet models have shallower structures compared to EEGNets
- We further investigate Interpretable CNN by comparing its performance with its variations. As it can be seen from the results shown in Fig.
- The obtained results indicate that the separable convolution can indeed boost the performance of the model, while the performance when using a standard 1D convolutional layer is similar to that when a single pointwise or a depthwise convolutional layer is used in the model. In addition, we can also observe that the performance of the model is largely affected when the batch normalization layer is removed.

### 2) Individual comparison results on the unbalanced dataset:


![Screenshot 2024-06-26 150756.png](./Screenshot%202024-06-26%20150756.png)

- compared the best baseline methods with the proposed method on unbalanced data for each individual.Specifically, we conduct leave-one-subject-out cross validation, where the unbalanced EEG data from one subject is used for testing, while the balanced data from all the other subjects are used for training in order to obtain the unbiased classifiers. Besides accuracy, we also use another two metrics,which are precision and recall, to evaluate the classification on the unbalanced data.
- By looking at individual classification results, we find that Subject 2 has a low accuracy for almost all the classifiers.

### B. Interpretation on the learned characteristics from EEG signals
- investigated what patterns have been learned by the model to distinguish between alert and drowsy EEG signals with the interpretation method.
- In addition, we also explore the reasons behind some wrongly 
classified samples for selected subjects discussed in the previous section.
- We have found that most EEG samples classified as drowsy signals by the model with a high confidence level commonly contain a high portion of Theta waves or alpha waves.
FIG 3:


![Screenshot 2024-06-26 154818.png](./Screenshot%202024-06-26%20154818.png)
FIG 4:


![Screenshot 2024-06-26 154828.png](./Screenshot%202024-06-26%20154828.png)

- For the first sample shown in Fig. 3(a), it can be observed that the model has identified several episodes that contain rhythmic bursts in the Theta band as strong evidence of the drowsy state. These bursts in the Theta band, or called “drowsy bursts”, have been found to frequently appear in EEG signals during drowsiness .
- For the samples shown in Fig. 3(b-d), it can be observed that the model has identified spindle like structures in Alpha frequency from several episodes of the signal as indicators of drowsiness.
- observed another interesting pattern that the central and centro-parietal EEG channels, e.g., Cz in Fig. 3(b), usually play a more importance role than peripheral channels for drowsiness classification. One possible reason is that these channels mostly contain cleaner cortical signals, where the drowsiness-related features are more distinguishable than those from the peripheral or frontal channels, which are more likely to becontaminated by artifacts caused by brain muscle tension or eye movements.
- . For the first two samples shown in Fig. 4(a) and 4(b), the model has 
identified several episodes of the signals from peripheral EEG channels (including F7, FT7, T5, O1, O2 and TP8), which result in high relative power in the Beta frequency band, as evidence for the classification. 
- in Fig. 4(c) and 4(d), it can be observed that the model has identified several episodes that contain large voltage change of signals from frontal EEG channels as evidence of alertness. These large-amplitude and low frequency waves, resulting a high power in the Delta frequency band, are caused by eye blinks and eye movement activities during the wakeful state.
- these artifacts including EMG and eye movement activities are 
the strongest components of wakeful EEG signals.
FIG 5:
![Screenshot 2024-06-26 155112.png](./Screenshot%202024-06-26%20155112.png)



- we find that sensor noise contained in the EEG signals is one of the major reasons that lead to the low classification accuracy. As it can be seen in the example shown in Fig. 5(a), the model has falsely identified the noise, which causes significant fluctuations in the TP7 channel, as evidence of the alert state.
- We have also found that the EMG activities could be a common factor that affects the classification across different subjects. 
- FIG 6:

![Screenshot 2024-06-26 155122.png](./Screenshot%202024-06-26%20155122.png)


- From the three representative samples shown in Fig. 6, we can observe that the model has falsely identified several episodes containing EMG activities from peripheral EEG channels, e.g., F7, FT7, as evidence for its classification, regardless of the apparent drowsiness-related Alphaspindles 
contained in the samples. 

## Conclusion:
- In this paper, we consider a promising topic of usinginterpretable deep learning models to discover meaningful patterns related to different mental states from cross-subject EEG signals.
- The model has a compact structure and it uses separable convolutions to process the EEG signals in a spatial temporal sequence. In order to allow the model to “explain” its decisions, we designed an interpretation technique, which is inspired by the CAM and Fixation-CNN methods, to reveal the important local regions of the sample for the classification.
-  we found the model had learned biologically meaningful features 
from the EEG signals to distinguish between alert and drowsy states
- Specifically, the model has discovered neurologically interpretable features, such as Alpha spindles and bursts in Theta band, as evidence of drowsiness. 
- It has also learned to recognize eye blink and eye movement features, as well as the Beta waves from peripheral EEG channels, which are mixtures of cortical signals and EMG activities, as evidence of alertness.
- In addition, we also explored the reasons behind some wrongly classified samples in order to understand how the cross-subject classification accuracy can be further improved.
- The obtained results indicate it is necessary to carefully design
the pre-processing pipeline for dealing with different kinds of 
artifacts and noise in the signals according to their impacts on 
the classification task.
- this research paper illustrates a promising direction to discover 
meaningful patterns related to different mental states from 
complex EEG signals towards calibration-free brain computer 
interfaces.















