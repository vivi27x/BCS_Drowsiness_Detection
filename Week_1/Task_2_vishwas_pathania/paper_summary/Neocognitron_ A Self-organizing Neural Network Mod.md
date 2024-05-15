# Neocognitron: A Self-organizing Neural Network Model for a Mechanism of Pattern Recognition Unaffected by Shift in Position(summary by vishwas pathania)
#### introduction
- A neural network model for a mechanism of 
**visual pattern recognition** is proposed in this paper. 
- The network is self-organized by **"learning without a 
teacher"**, and acquires an ability to recognize stimulus 
patterns based on the geometrical similarity of their shapes **without affected by their positions**. This network is given a nickname "neocognitron".
- Through self-organization, the network becomes a network that resembles our visual nervous system. first layer = photoreceptors, and after it’s a cascade connection of S-cells (simple cells) and C-cells (complex cell). And the S-cells have modifiable plasticity!
- Using unsupervised learning it can recognize patterns based on geometric similarity — not being affected by position shift or shape distortions. 
- After self-organization through unsupervised learning — it ends up being similar to the visual nervous system proposed by Hubel and Wiesel. Which is the visual cortex has this hierarchy structure: LGB (lateral geniculate body) → simple cells → complex cells → lower-order hypercomplex cells → higher-order hypercomplex cells.
-  the cells in the highest stage are supposed to respond only to specific stimulus patterns without affected by the position or the size of the stimuli. 
-   the response of the cells of the deepest layer of our network is dependent only upon the shape of the stimulus pattern, and is not affected by the position where the pattern is presented. That is, the network has an ability of **position-invariant pattern- recognition.**

#### structure of the network
the structure is shown in the figure:

![Screenshot 2024-05-11 225004.png](./Screenshot%202024-05-11%20225004.png)



![Screenshot 2024-05-11 225023.png](./Screenshot%202024-05-11%20225023.png)

- As shown in Figure, the neocognitron consists of a 
cascade connection of a number of modular structures 
preceded by an input layer U o.
- Each of the modular structure is composed of two layers of cells connected in a cascade.
-  The first layer of the module consists of "S-cells", which correspond to simple cells or lower order hypercomplex cells according to the classifi- 
cation of Hubel and Wiesel.  The second layer of the module consists of "C-cells", which correspond to complex cells or higher order hyper- 
complex cells. We call it C-layer and denote the C-layer in the l-th module as Ucl.
- In the neocognitron, only the input synapses to S-cells are supposed to have plasticity and to be modifiable. 
- The input layer U 0 consists of a photoreceptor array. The output of a photoreceptor is denoted by u0(n ), where n=(nx, ny ) is the two dimensional co-cordinates indicating the location of the cell. 
- S-cells or C-cells in a layer are sorted into sub- groups according to the optimum stimulus features of their receptive fields. Since the cells in each subgroup are set in a two-dimensional array, we call the sub- group as a **"cell-plane"**.
- the model is based on the hypothesis  that all the cells in a single cell-plane have input synapses of the same spatial distribution, and only the positions of the presynaptic cells are shifted in parallel from cell to cell. Hence, all the cells in a single cell-plane have receptive fields of the same function, but at different positions. 
- The circles represent the areas to which proceeding cells connect. But for S-Cells they get to choose which parts within the area they want to connect with.
- We can also see that the deeper the layer is in the networks, the more the receptive field increases. The last layer’s receptive field covers the entire input layer — thus it becomes the output cell.
- here is the equation for the output of simple cell

![Screenshot 2024-05-11 225049.png](./Screenshot%202024-05-11%20225049.png)
- C-cell have synaptic connections from a group of S-cells in its corresponding S-plane .The efficiencies of these synaptic connections are so determined that the C-cell will respond strongly whenever at least one S-cell in its connecting area yields a large output.

- here is the eqaution for the output of complex cell

![Screenshot 2024-05-11 225124.png](./Screenshot%202024-05-11%20225124.png)


#### Self-organization of the Network
- At first, several **"representative"** S-cells are selected from each S-layer every time when a stimulus pattern is presented. The representative is selected among the S-cells which have yielded large outputs, but the number of the representatives is so restricted that more than one representative are not selected from any single S-plane.
- The procedure for selecting the representatives is 
given below:
> - At first, in an S-layer, we watch a group of S-cells whose receptive fields are situated within a small area on the input layer. If we arrange the S-planes of an S-layer in a manner shown in Figure

![Screenshot 2024-05-11 225139.png](./Screenshot%202024-05-11%20225139.png)
> the group of S-cells constitute a column in an S-layer. Accordingly, we call the group as an **"S-column"**. An S-column contains S-cells from all the S-planes. That is, an S-column contains various kinds of feature extracting cells in it, but the receptive fields of these cells are situated almost at the same position.
> - From each S-column, every time when a stimulus pattern is presented, the S-cell which is yielding the largest output is chosen as a candidate for the representatives. 
> - If two or more candidates appear in a single S-plane, only the one which is yielding the largest output among them is selected as the representative from that S-plane.
> -  each S-plane becomes selectively sensitive to one of the features of the stimulus patterns, and there is not a possibility of formation of redundant connections such that two or more S-planes are used for detection of one and the same feature.

####  Rough Sketches of the Working of the Network 
-  

![Screenshot 2024-05-11 225209.png](./Screenshot%202024-05-11%20225209.png)

- Each layer plays its role in extracting certain geometric shapes from the input image. And then slowly as we go deeper and deeper into the network it starts combining them together and recognizes that it’s an A! The S-cells are naturally wired such that it’s only when it receives certain signals (like the last layer which will only respond when it gets all 3 components of the A)
- Now, this is for a single A, but what if we had a thousand different letters? Well, it’s okay since as we add more letters, they’ll end up sharing the same features, so we’re still okay. in this way we can counter the distortions in the patterns.

#### Computer Simulation 


![Screenshot 2024-05-11 225229.png](./Screenshot%202024-05-11%20225229.png)

-  In the computer simulation, we consider a seven layered network: Uo-Us1 ->Ucl-> Us2 ->Uc2->Us3->Uc3. That is, the network has three stages of modular structures preceded by an input layer. 
- The number of cell-planes in each layer is 24 for all the layers except U o. The numbers of excitatory cells in these seven layers are: 16x 16 in Uo, 16x 16x24 in Us1, 10x 10x 24in Ucl, 8 x 8 x 24in Us2, 6x 6x 24in Uc2, 2 x 2 • 24 in Us3, and 24 in Uc3. In the last layer Uc3, each of the 24 cell planes contains only one excitatory cell (i.e. C-cell). 
- The number of cells contained in the connectable area S t is always 5 x 5 for every S-layer. Hence, the number of input synapses 3 to each S-cell is 5 x 5 in layer Usl and 5 x 5 x 24 in layers Us2 and Us3.
- Each stimulus pattern has become to elicit an output only from one of the C-cells of layer Uc3, and conversely, this C-cell has become selectively responsive only to that stimulus pattern. That is, none of the C-cells of layer Uc3 responds to more than one stimulus pattern.

#### conclusion
This paper proposes neurocognition, which has the ability to recognize patterns, with distortions and shifts, through an unsupervised manner by recognizing the geometric shapes.