# NEOCOGNITRON : WAY OUT OF THE MATRIX ?
In this paper, [Kunihiko Fukushima](https://en.wikipedia.org/wiki/Kunihiko_Fukushima) develops a neural network model that recognizes visual patterns even if they are shifted in space or are distorted by small amounts. The striking feature is that it does using unsupervised learning.
He wanted to create such a neural network that resembles the human brain in terms of pattern recognition to understand how the brain works. Curious to know the mechanism of the brain, he made the structure of neocognitron similar to the visual cortex of vertebrates. 
In the abstract section, he describes how a network, after **self-organization**, resembles the hierarchy model of the visual nervous system proposed by Hubel and Wiesel. The network includes an input layer (like a photoreceptor array) followed by modular structures connected in a cascade. Each module has two layers of cells: "S-cells" in the first layer, akin to simple cells or lower-order hypercomplex cells, and "C-cells" in the second layer, similar to complex cells or higher-order hypercomplex cells. Only input synapses to S-cells are plastic and modifiable.
The S layer in l-th module is denoted as U<sub>Sl</sub> similarly C layer in the l-th module is denoted as U<sub>Sl</sub>. The input layer U<sub>0</sub> consists of photoreceptors whose output is denoted as u<sub>0</sub>(**n**) where **n**=(n<sub>x</sub>,n<sub>y</sub>) denotes the location of cell. Each layer of S and C cells have subgroups known as S and C planes that are formed according to stimulus features of their receptive fields.
* * *

![d50ea1f036c9403ccc7cca51351e782e.png](../_resources/d50ea1f036c9403ccc7cca51351e782e.png)
It is assumed that all the cells in a single cell plane have input synapses of the **same spatial distribution**.
![b637e83787a1afc2cac7f7041ea82579.png](../_resources/b637e83787a1afc2cac7f7041ea82579.png)

Figure 2 depicts a cell from each layer receiving connections from cells within an enclosed area in the preceding layer, represented by an ellipse. Specifically, the ellipses in the figure signify the connectable area rather than the exact connecting area for S-cells, indicating that not all interconnections shown are always formed due to synaptic plasticity. as the depth of cell-planes increases, the total number of cells within each plane decreases. In the final module, C-cells have extensive receptive fields covering the entire input layer U<sub>0</sub>, leading to each C-plane containing only one C-cell due to this broad coverage.The synaptic connections from S-layers to C-layers are fixed and unmodifiable. Even if a stimulus pattern which 
has revoked a large response from a C-cell is shifted a little in position, the C-cell will keep responding as before, because another presynaptic S-cell will become to respond instead.
* * *

During the **self organization**, the first step is to select representative cells everytime input is given. These are the S cells that have highest output. Atmost one representative cell is allowed in each S plane.Initially, the network is in kind of blank state as it is not biased toward particular orientation.
![74331ac3fd669d99c62d1f72267acb45.png](../_resources/74331ac3fd669d99c62d1f72267acb45.png)
An S column is a group of S cells within an S layer. These S cells have receptive fields that are placed close together in a small area on the input layer. The S-column contains S-cells from all the S-planes within the S-layer so it includes different types of feature extracting cells. All S-cells within an S-column have receptive fields that are almost at the same position. This alignment allows the S-column to analyze input features within a localized region.he concept of S-columns is similar to the idea of "hypercolumns" proposed by Hubel and Wiesel. Hypercolumns are groups of neurons in the visual cortex that respond to specific features of the input. Now, the S cell which yields the largest output is made the representative cell in that S column. It is possible for a S cell to be contained in two or more columns as the columns also overlap each other sometimes.


![alt text](../_resources/image.png)
The selection of representatives in each S-plane ensures that distinct features are detected across layers, preventing redundancy in connections. 
* * *

After self orgranization, we have different feature extracting cells which recognize different components in the image.

![5e78b3699c1eaffb36d3c9ae19ddf0fa.png](../_resources/5e78b3699c1eaffb36d3c9ae19ddf0fa.png)

This C-cell's response is relatively stable against positional shifts in the stimulus pattern compared to its presynaptic S-cells. In the next S layer, take example of the S cell shown in fig.5, it take input or say its synapses have been reinforced in such a way that it responds to only some features.
Since operations of this kind are repeatedly applied through a cascade connection of modular structures of S- and C-layers, each individual cell in the network becomes to have wider receptive field in accordance with the increased number of modules before it, and, at the same time, becomes more tolerant of shift in position of the input pattern.
In last layer that is U<sub>c3</sub> single c cells yields large output according to what pattern is recognized.
Firstly the network recognizes components of input in small visual fields and if they do not differ very much in all the fields , it decides that they are the same and this small allowance in each step that cascades down result in space invariancy of the pattern as the last layer's visual field is wide enough to see the whole input at once. This way neocognitron is also immune to some distortion in shapes.

The neural network in this study is simulated on a digital computer and consists of seven layers: U<sub>0</sub>, U<sub>s1</sub>, U<sub>c1</sub>, U<sub>s2</sub>, U<sub>c2</sub>, U<sub>s3</sub>, and U<sub>c3</sub>, with three modular stages following an input layer. Each layer except U<sub>o</sub> has 24 cell-planes (Kz), and the number of excitatory cells varies across layers: 16x16 in U<sub>0</sub>, 16x16x24 in U<sub>s1</sub>, 10x10x24 inU<sub>c1</sub>, 8x8x24 in U<sub>s2</sub>, 6x6x24 in U<sub>c2</sub>, 2x2x24 in U<sub>s3</sub>, and 24 in U<sub>c3</sub>, where each cell-plane in U<sub>c3</sub> contains one excitatory cell (C-cell). The connectable area S<sub>t</sub> always contains 5x5 cells in every S-layer. Therefore, the number of input synapses to each S-cell is 5x5 in Us1 and 5x5x24 in Us2 and Us3 due to the preceding C-layers with 24 cell-planes. Despite the consistent S<sub>t</sub> size, the projected area, observed at U<sub>o</sub>, grows for deeper layers due to reduced cell-plane density.

![7edd4b1b7ebd36e44f8b486ee678d35a.png](../_resources/7edd4b1b7ebd36e44f8b486ee678d35a.png)

During a computer simulation, a network is presented 20 images of each 0,1,2,3 and 4. After self organization is complete, we find the pattern revoke only one cell in the large layer i.e U<sub>c3</sub> and also the cell corresponds to only one pattern.
It is also found that the network correcctly recognizes pattern even after small distortions as showwn in fig.6. Figure7 displays how individual cells in the neocognitron have responded to stimulus pattern "4". In an experiment to check whether the network learn to discriminate between resembling images, it is presented with image of "X","Y" and "Z" as they have common components and it is found that the network learns to differentiate between them successfully.
If there are more number of patterns to be recognized, it is better to increase the number of cell planes in each layer in order to increase the accuracy. 
* * *

**CONCLUSION**
The neocognitron 
- recognizes patterns
- not affected by shift in position or small distortions
- learns without a teacher 
- has a function of self organization
- The author does not advocate that the neocognitron is a complete model for the mechanism of pattern recognition in the brain, but he proposes it as a working hypothesis for some neural
mechanisms of visual pattern recognition.







