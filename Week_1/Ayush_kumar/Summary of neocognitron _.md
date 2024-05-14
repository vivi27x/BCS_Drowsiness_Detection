Summary of neocognitron :

Neocognitron: A self-organizing neural network model for a mechanism of pattern recognition unaffected by shift in position.

- Before neocognitron , conventional cognitron is being used it also has the ability to recognise patterns but its response was dependent upon the position of the input patterns. Different for the different positions of the same pattern.
- Unsupervised learning model nocognitron, After completion of self-organization, the response of the cells of the deepest layer of our network is dependent only upon the shape of the stimulus pattern and is not affected by the position where the pattern is presented. That is, the network has the ability of position-invariant pattern- recognition.
- It is an unsupervised learning model we do not need any teacher to train it is self-organising after the completion of self oraganization it ends up similar to visual nervous system.

Structure of the network-

- The system is comprised of modules that have a cascade connection preceded by an input layer Uo. Each modular structure is made up of two layers. The first layer is called the S-layer and consists of "S-cells". It is denoted as the S layer of the lth module, which is called Usl. The second layer of the module is called the C-layer and consists of "C-cells". It is denoted as the C-layer of the lth module, which is called Ucl.

![](Aspose.Words.5c02b727-e5e1-4fcf-8295-58705e4572e9.001.jpeg)

- Here each thin-line rectangular block called layer and dark square box called plane and plane is made up of array of cells. C and S-cell are excitatory cells. ●
- In a plane all cell have input synapses of same spatial distribution only the positions of the presynaptic cells are shifted in parallel from cell to cell.
- The circular region is called receptive field- The region of the input space thatare nueronis responsive to. Total no. of cells decreases as depth of cell plane in the network by this the respective field of the last layer is so large that covers the entire input.
- For the calculation of density of cells is done by maths part but that i am not really able to understand.

Rough sketch of the working of the network-

- Let’s say we are tracking “A” in the input pattern so different-2 S plane work to identify different part of A let’s say the upper part of A is traced in 1st plane so cells in upper region shows a large output.
- C-cell has the synaptic connection with previous S-cell situated in inside receptive field of c.
- If a cell within the receptive field displays a large output in the S-cell, it can trigger the C-cell and activate it. Due to translation invariance, the response of the C-cell is less affected by any shift in the position of the stimuli pattern. Therefore, the C-cell located at the top of the plane will respond to this particular feature, and a similar process will occur for the rest of the features...
- Some of the features pattern in C cell are not covered inside the receptive field of S-cell here inhibitory cells makes the inhibitory synaptic connection to this S-cell This kind of operation is applied repeatedly make wider receptive field that help to include missing features.
- So for so Different pattern we train the models for so many random small pattern that collectively make a input pattern and then compared to show the result.
