* * *
**INTRODUCTION**
In the context of EEG-based driver drowsiness recognition, designing a calibration-free system is challenging due to the variability of EEG signals among subjects and sessions. While deep learning methods have been employed for mental state recognition, their models often remain black-boxes. This paper introduces a novel CNN to detect drowsiness in drivers.
* * *
**DATA PREP** : 
The author has used a public eeg dataset obtained from 27 subjects (aged 22 to 28 yrs) in a VR driving simulator task. The task was enriched with events that included lane change. turning etc. The drowsiness level was interpreted from how quickly the driver responded to the change.
Based on the global and local reaction time, an inquisitve apporach was take to classify a sample to be alert or drowsy.
The EEG signal was originally of 500Hz and had data from 30 electrodes. The author downsampled it to 128Hz and exctracted events as 3 seconds of eeg signal prior to any occurence of change in game. 1-50 bandpass filter and artifact rejection followed up which led the author to have 30(no. of channels) x 384(no. of sample events).
* * *
**IDEA** 
For driver drowsiness recognition, it is proposed to use the feature extraction pipeline, where the raw EEG data were demixed with the ICA method and band power features were obtained from each of the demixed signals. 
* * *
**NETWORK STRUCTURE**
The network structure described consists of seven layers for classifying EEG signals. The layers are:

1. **First Layer**: Pointwise convolution with 16 nodes, generating 16 new channels of the same length as the input.
2. **Second Layer**: Depthwise convolution with 32 nodes, extracting features from the new signals. The output size is (32, 321).
3. **Third Layer**: ReLU activation layer.
4. **Fourth Layer**: Batch normalization layer.
5. **Fifth Layer**: Global Average Pooling (GAP) layer, reducing parameters to prevent overfitting.
6. **Sixth Layer**: Dense layer, producing final feature representation.
7. **Seventh Layer**: Softmax activation layer for binary classification (alert or drowsy state).

The model, named "InterpretableCNN," is designed to be interpretable, with classification results that can be explained using techniques detailed in the next section.
* * *
**INTERPRETATION TECHNIQUE** 
There a lots of common interpretation techiniques but no any fruitful ones so we focus on using CAMs that are basically heatmaps, it shows which areas the model focuses on which classifying. M(i,j) can be viewed as the distribution of the final activation ℎ𝑐 for class c in a map of size 2𝑁1 × (𝑛 − 𝑙 +1). The original CAM method finds the  heatmap by upsampling 𝑀𝑖,𝑗 𝑐 until it has the same size as the input sample.However, the method cannot be directly used for our model since the channels of the input signal are mixed by pointwise convolutions in the first layer, which makes the first (channel) dimension of 𝑀𝑖,𝑗 𝑐 misaligned with the first (channel) dimension of the input signal. ![c613c5ffc2203220549c5e8a8089a859.png](../_resources/c613c5ffc2203220549c5e8a8089a859.png)

We take following steps - 
1. We rank the 𝑀𝑖,𝑗𝑐  values in descending order 
2. To trace back 4 layers, first we realize the 3rd and 4th layer incur no topological change.
3. In the second layer, we can see that the odd and even rows are weighted sums. 
4.  We trace the top 100 (N=100) 
discriminative locations in class activation map 𝑀𝑖,𝑗𝑐, which accounts for around 1% of all entries of 𝑀𝑖,𝑗 𝑐.
* * *
**OBSERVATION**
We have found that most EEG samples classified as drowsy signals by the model with a high confidence level commonly contain a high portion of Theta waves or Alpha waves. It can be observed that the model has identified several episodes that contain rhythmic bursts in the Theta band as strong evidence of the drowsy state. These bursts in the Theta band, or called “drowsy bursts”, have been found to frequently appear in EEG signals during drowsiness.
It can be observed that the model has identified several episodes that contain large
voltage change of signals from frontal EEG channels as evidence of alertness. 
It is out of our expectation that the model uses features that are commonly regarded as artifacts contained in EEG as indicators of the alert state. In fact, these artifacts including EMG and eye movement activities are the strongest components of wakeful EEG signals, so that it makes sense to some extent that the model has identified such features from group statistics of the data
* * *
**CONCLUSION**
In this paper, we developed a novel CNN model for the purpose of discovering common patterns related to different mental states in EEG signals across different subjects. The model has a compact structure and it uses separable convolutions to process the EEG signals in a spatial-temporal sequence. 
The interpretation results show that the model has learned to identify biologically meaningful features, e.g., Alpha spindles, from the data and use them as evidence to distinguish between drowsy and alert EEG signals.