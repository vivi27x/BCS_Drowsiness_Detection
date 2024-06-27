From the abstract
* challenging to design a calibration-free system, since EEG signals vary significantly among different subjects and recording sessions. 
* convolutional neural network + interpretation technique that allows sample-wise analysis 
* separable convolutions, spatial-temporal sequence 
* average accuracy of 78.35% 
* Biologically meaningful features like alpha spindles recognized 
* Wrong classification and analysis 
* Towards calibration free system 

From the introduction
* Driver’s drowsiness – leading factor of accidents 
* Challenge – low signal to noise rate 
* Variability of EEG across different subjects – due to electrode displacements, skin electrode impedance, different head shapes and sizes, different brain activity patterns, disturbance by task-irrelevant brain activities 
* Conventional methods – hand-crafted features that might exclude other relevant info 
* Deep learning – eliminates need for prior feature crafting 
* Existing works in EEG processing treats DL models as black box classifiers 
* “Interpretable CNN” - compact structure and it uses separable convolutions to process the EEG signals in a spatial-temporal sequence 
* Interpretation technique to locate regions of input signal that are important 

Related works: 
* Existing driver monitoring systems 
    * Alarm when driver is drowsy 
    * Lexus 2006, Toyota – first monitoring system– CCD camera to track face using infrared LED detectors 
    * Focus & Mondeo models, Ford – drowsiness detection through lane-tracking performance 
    * Biometric car seat prototype, Ford – monitor inattention with multiple physiological signals: 
        * Seatbelt with integrated piezoelectric film to monitor respiration 
        * Infrared sensors are placed on the steering wheel spokes to monitor the driver's facial temperature 
        * Conductive sensors built into the rim of the steering wheel can monitor the heart rate and skin conductivity 
    * Maxima model, Nissan – drowsy driving predicted using steering pattern 
    * EEG’s advantage over above – direct monitoring of brain activities detects drowsiness in early stages 
* EEG-based driver drowsiness recognition 
    * EEG measures voltage difference on scalp 
    * 1-256 electrodes 
    * 10-20 system 
    * Channel name – 1 or 2 letter acronyms + number or ‘z’ 
        * F – frontal, P-parietal, Fp - prefrontal etc 
        * Number – placement on the coronal line, z = zero (centre of coronal line) 
    * Experiment conclusions: 
        * Higher power of theta, alpha during night driving compared to morning driving 
        * Increased power of alpha, beta from sleep deprived subjects 
        * Higher power in the EEG frequency power bands during the early sleep stage 
        * Drowsiness can cause increased power of theta, alpha 
        * Increase in lower alpha occurs only when subjects are trying not to sleep, alpha decreases once asleep 
    * While using deep learning, processes of feature extraction and classifier training are combined under the same learning framework 
    * DL attempts at drowsiness detection: 
        * a simple convolutional network consisting of two convolutional layers, a max-pooling layer, a flatten and a fully connected layer to classify single-channel EEG data for Advance Driver Assistance Systems 
        * a deep CNN model on a mobile device to detect drowsiness from single-channel EEG signals - cascaded CNN + attention mechanism layer 
        * EEG-based Spatial–Temporal CNN (ESTCNN) - three core blocks - each block convolution layer + ReLU layer + batch normalization layer. 
        * EEG-Conv - traditional CNN 
        * EEG-Conv-R - CNN + deep residual learning 
    * This paper proposes a compact CNN model that deals with multi-channel EEG signals + a visualization technique for the model to “explain” its decisions 

Material and methods 
* Data preparation 
    * Experiment: 
        * 27 subjects aged 22-28 
        * Sustained-driving task in a virtual reality simulator 
        * Lane departure events drift car away.  
        * Response rate to events studied 
    * Dataset description 
        * 500Hz, 30 electrodes, 1-50 Hz bandpass filter, artifact rejection 
        * Down sampled to 128Hz, samples of 3 second length prior to event 
        * Each sample has dimension 30(channels)x384(sample points) 
        * Local reaction time (RT) - time taken by the subject to respond to the car drift event 
        * Global reaction time – average of RTs within 90 sec windows before the drift event 
        * Baseline “alert-RT” – 5th percentile of local RTs 
        * Samples with both local RT, global RT < 1.5xalert RT labelled as alert state 
        * Samples with both local RT, global RT> 2.5xalert RT labelled as drowsy state 
        * Sessions with less than 50 samples of either class discarded 
        * Among multiple sessions of the same subject, the session with the most balanced class distribution was selected 
        * The above steps were done to avoid the model from learning the subject 
        * Final – 2952 samples from 11 different subjects 
        * Balanced dataset also developed by choosing most alert, most drowsy state for each subject 
* Network design 
    * The core idea 
        * Spatial filtering technique to denoise 
        * N1 new signals are obtained using the linear combination of the EEG signals from m electrodes 
        * The weights are a set of spatial filters 
        * Some examples are Independent Component Analysis, Common Spatial Pattern, Minimal Energy Combination etc 
        * Features are then extracted from each one of the new N1 signals 
        * Our model uses a processing pipeline to do the above 
    * The context of separable convolution 
        * Depth wise separable convolution = depth wise convolution performed on each channel independently + pointwise convolution which projects channels onto a new space 
        * Pointwise convolution – demixing signals 
        * Depth wise convolution – learning temporal features of demixed signals 
    * Network Structure 
        * 7 layers 
        * First two layers = pointwise, depth wise convolution 
        * Followed by ReLU activation layer, batch normalisation layer, global average pooling layer, dense layer, SoftMax activation layer 
        * First layer – N1 pointwise convolutional nodes to generate 𝑁1 new channels of signals with the same length 
        * Input sample X(m,n), m=no. Of channels = 30, n= signal length 
        * Output from first layer – N1 linear combinations of input eeg signals  
        * N1 = 16 to encourage convergence 
        * Second layer – depth wise convolution used to extract features – every new signal from the prev layer is convoluted at two nodes – so, 2N1 nodes 
        * A kernel of length l (l number of weights) is used. H i,j of second layer is convolution of the kernel over the h i/2, j or h (i+1)/2, j signal depending on whether i is even or odd. 
        * This means, i = 1 of the first layer will be connected to both i =1 and i =2 of the second layer 
        * L is chosen as 64 
        * Size of output is (2N1, n-l+1) = (32, 321) 
        * Third layer – ReLU 
        * Fourth layer – Batch normalization 
        * Fifth layer - Global Average Pooling – Averages values from each node – reduces parameters – prevents overfitting 
        * Sixth layer – two nodes (0,1) - Dense layer – Linear combination over all nodes 
        * Seventh layer – SoftMax activation layer – two nodes (0,1) 

Interpretation technique 
* allows us to find out whether the classification is driven by relevant features, discover neurophysiological patterns 
* Class Activation Map (CAM) - most powerful technique 
* For each input sample – heatmap generated from activation after last convolutional layer 
* Then interpolated to size of input sample 
* CAM – designed for deep CNN with only standard conv layers – cannot be used models involving convolutions in the spatial dimensional or having structures more than basic convolutions blocks 
* Inspired by CNN- fixation method, only a small portion in the activation map that contribute most is traced back to areas of input 
* Objective is to trace location throughout the network to the centre of high activation areas. 
* Final heatmap can be obtained by combining all the class discriminative points in the input sample with the Gaussian function 
* Third, fourth layers do not affect topology, so we needn’t consider them. 
* Only convolutional layers affect topology 
* Top 100 discriminative locations in class activation map are traced 

Methods for comparison 
* Deep learning methods 
    * EEGNet 
        * 2D conv layer to filter -> spatial depth wise conv layer + temporal depth wise conv layer for feature extraction 
    * Sinc Shallow Net 
        * sinc-convolutional layer and a depth wise convolutional layer to process the raw EEG data in a temporal spatial sequence 

* Conventional baseline methods 
    * 5 baseline methods – for feature extraction applied and tested on 8 diff classifiers 
        * Relative power 
            * Absolute power of each band calculated, and relative power calculated 
        * Log power 
            * Natural log of band power calculated 
        * Power ratio 
            *  (i) (θ +α)/β, (ii) α/β, (iii) (θ + α)/ (α + β) and (iv) θ/β are good indicators of driver drowsiness so are calculated. 
        * Wavelet Entropy 
            * Mexican hat wavelet used 
            * wavelet entropy feature for each EEG channel is calculated by applying the Shannon function on the normalized wavelet coefficients 
        * Four Entropies 
            * approximate entropy and spectral entropy and the fuzzy entropy is calculated. Then, each feature dim for each subject is normalised 

* Classifiers 
    * Different classifiers have been implemented, which include Decision Tree (DT), Random Forest (RF), k nearest neighbors (KNeighbors) etc 

* Variation of model for comparison 
    * First variation – standard 1D convolutional layer instead of first two layers 
    * Second and third variation – depth wise and point wise convolutional layers are removed 
    * Fourth variation – remove batch normalization layer 

Evaluation on the proposed method 
* Mean accuracy comparison 
    * While tested, shallower networks (Interpretable CNN and Shallow Net) performed better 
    * Model’s accuracy decreased 2% in first, second and third variant 
    * Fourth variation decreased accuracy even more 
    * highest mean accuracy of 72.68% is achieved by LogPower + GNB. 
* LOSO comparison 
    * precision score is calculated by dividing the correctly classified drowsy samples by the total number of samples classified with the label of drowsiness. 
    * recall score is calculated by dividing the correctly classified drowsy samples by the total number of drowsy samples 
    * the proposed model has the highest mean accuracy of 77.70% among the five models. 

Interpretation on the learned characteristics 
* Learned characteristics of drowsiness 
    * a high portion of Theta waves or alpha waves 
    * rhythmic bursts in the Theta band - “drowsy bursts” 
    * spindle like structures in Alpha frequency or a narrow frequency peak within the alpha band - indicators of early drowsiness 
    * the central and centro-parietal EEG channels play a more important role 
* Learned characteristics of alertness 
    * More artifacts – due to eye movement – strong indicator of wakeful state 
    * High power of beta, delta (caused by eye movements) 
    * Large voltage changes of signals from the frontal EEG channels 
* Reasons for wrong classification 
    * Sensor noise – eg, presence of spindle like features in all bands 
    * EMG activities 

From the conclusion
* A CNN model – for discovering common patterns related to diff mental states 
* Separable convolutions  
* Eeg signals processed in a spatial-temporal sequence 
* Interpretation techniques by highlighting relevant parts of input 
* Biologically meaningful features like alpha spindles recognized 
* Wrong classification and analysis 
* Towards calibration free system 

 