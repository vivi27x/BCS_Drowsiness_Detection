

## Analysis of the Neocognitron paper?
### Description of the Network
 - The papers that came before this has a flaw that they could recognize characters, but not if they were shifted or their size was changed. People tried to normalize the position and size of a character seeing some paramters but if the input had some noise or distortion they couldn't, so they weren't actually recognizing patterns, this model is able to do so.
 - The network has an input layer which is basically the image array and connected to it stacks of modules having two layers, the S-cell layer and the C-cell layer.
 - This is inspired by the structure of the brain's visual cortex, where it also has the stacking of simple and complex cells, where deep down in the network, a cell can response to a more complicated feature and along with it is insensitive to shift. The brain has only 2 such modules( and yet it can make do?), we have several.
 - These s or c layers are also divided into subgroups according to what feature they are recognizing, this subgroup is known as a cell plane. Basically all the cells in a single plane have the same receptive field (are sensitive to the same feature) but at different positions. The torch is at different positions.
 - A cell of each layer *may* be connected to the cells only in the position of the torchlight.
 - So the deeper the layer, the larger the receptive field of each cell from that layer. And the density of cells decreases as receptive fields increase.(Because pehle ek feature ke liye chhoti chhoti receptive field thi aur har ek ke liye cell, as receptive field badhi uske liye cell kam hote gaye). At the end receptive field coves the entire area.
 - The S and C cells are excitatory(?), we also have inhibitory cells(?)
 - The cells are analog type, which means that the neuron takes a value from (0,infinity) and the S cells have shunting type inhibitory inputs, which means they use ReLU
 - (I dont get the math)
 - The connections from S->C are fixed, they need no change in weights, the efficiencies(weights) so determined that C cell responds strongly to atleast one  S cell lighting up in that plane, here the normalisation function is phi(?)*x/(a+x), where a is a constant which specifies the degree of saturation
 - We present a pattern to the model and select "Representative"(The ones that have a large output taking care that only one is selected from a single S-plane) S cells from each S-layer and all the other cells in the S-plane change their weights by the same amounts as their Rep Cells
 - How exactly do we choose rep cells, We consider an S-column, a cookie cutter passed across all the layers, which is the collection of cells whose receptive fields are nearly the same. One S cell may be in several columns, So we see, when presented with a stimuli in a column, the S-cell yielding the largest output is chosen as a candidate, if no cell is activated we dont choose any. 
 - Using this process we can make sure that there are no redundant S-planes.
 - A rough Sketch of how it works is, if our model is recognising Alphabets and we present it with an A, a can be broken down into several smaller patterns one of them being ^ at the top, so one the ^ recognizers in the plane S1 lights up, so the one neuron in the C1 layer representing the ^, connected to all the recognizers in the S1 layer lights up, the same happens for several other features and some cell in the S2 layers recognizes different parts of the A and so on
 - The S cell in the S2 layer also checks that other features which are to be extracted in other S1 layers are not checked by the help of inhibitory cells in the C1 layer.
 - To it may feel that as we increase the input patters, the number of feature recognizing layers also increases. In reality, as we increase the number of patterns, we can find several features in common.
 - From examples we see that incase we have several input patterns and they are different we should increase the number of cell planes
 - The same can be applied to auditory responses too if the graph is given as an input signal.
 - Good Stuff, will improve upon my understanding of math and update the math details

