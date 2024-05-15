# Neocognitron, Fukushima1980

## Introduction 
- The paper proposes a neural network model called the "neocognitron" for visual pattern recognition.
  
- Recognizes patterns by recognizing geometrical similarities (Gestalt) of their shapes without affected by their position nor by small distortion of their shapes. 
- Has an ability of self learning (learning without a "teacher").
- After completion of self-organization, the network acquires a structure similar to the hierarchy model of the visual nervous system proposed by Hubel
and Wiesel (1962, 1965). 
- According to the hierarchy model by Hubel and Wiesel, the neural network in the visual cortex has a hierarchy structure : LGB (lateral geniculate
body) --> simple cells --> complex cells --> lower order hypercomplex cells --> higher order hypercomplex cells.
- A structure similar to hierarchy model is introduced in this model. Its basically an extension to the hierarchy model.
- After completion of self-organization, the response of the cells of the deepest layer of our network is dependent only upon the shape of the stimulus pattern,
and is not affected by the position where the pattern is presented. That is, the
network has an ability of position-invariant pattern-recognition.

## Structure 
![image](https://github.com/roses-and-thorns/BCS_Drowsiness_Detection/assets/169232982/c6ddec48-fa5f-4407-92f4-5b747bc153b3)

![image](https://github.com/roses-and-thorns/BCS_Drowsiness_Detection/assets/169232982/c3ead523-6895-4ccf-8de7-8e651fdfc9eb)


- The neocognitron is structured as a cascade of modular units, beginning with an input layer $U_0$.
  
- The modular structure consists of two layers :
  - One consisting of "**S-cells**", correspnding to  simple cells or lower order hypercomplex cells, denoted as $U_{Sl}$ in the l-th module.
  - Other consisting of "**C-cells**", corresponding to complex cells or higher order hypercomplex cells, denoted as $U_{Cl}$ in the l-th module.
- Only the input synapses to S-cells are supposed to have plasticity and to be modifiable.
- The input layer $U_0$ consists of a photoreceptor array. The output of a photoreceptor is denoted by $u_0$(n),
  where n= ($n_x$, $n_y$ ) is the two-dimensional coordinates indicating the location of the cell. 
- S-cells and C-cells within a layer are organized into subgroups based on the optimal stimulus features of their receptive fields,
  forming what is termed a "**cell-plane**". Each cell-plane comprises cells arranged in a two-dimensional array.
- Figure 2 is a schematic diagram illustrating theinterconnections between layers. Each tetragon drawn with heavy lines represents an
  S-plane or a C-plane,and each vertical tetragon drawn with thin lines, in which S-planes or C-planes are enclosed, represents an S-layer or a C-layer. 
- The ellipse shown in the figure represent the "__connectable__" area not the connected one, as synaptic connections to S-cells have plasticity.
-  As layers deepen, receptive fields enlarge, with cell density decreasing accordingly. In the last module, each C-cell's receptive field covers
   the entire input layer, with only one C-cell per C-plane.
-  A C-cell have synaptic connections from a group of S-cells in its corresponding S-plane (i.e. the preceding S-plane with the same k~-number as that of the C-cell).
  The efficiencies of these synaptic connections are so determined that the C-cell will respond strongly whenever at least one S-cell in its connecting area yields a
  large output.

### Outputs
- Of S-cells :

  
  ![image](https://github.com/roses-and-thorns/BCS_Drowsiness_Detection/assets/169232982/cd31a721-863a-4756-a239-2b7d14252044)

  ![image](https://github.com/roses-and-thorns/BCS_Drowsiness_Detection/assets/169232982/a868d981-268f-4625-963f-c96916c76e07)

- Of C-cells :
  
  ![image](https://github.com/roses-and-thorns/BCS_Drowsiness_Detection/assets/169232982/7b2ae1fe-13ca-4d95-9361-b84aca3ba5a8)
  
  ![image](https://github.com/roses-and-thorns/BCS_Drowsiness_Detection/assets/169232982/6907e259-9504-43a3-8307-f2b08ea97189)

​
## Self-Organization
- Learning without a "teacher"
  
- Repeatedly given a set of stimulus patterns but no other info.
- One of the basic hypotheses employed in the neocognitron is the assumption that all the S-cells in the same S-plane have
input synapses of the same spatial distribution, and that only the positions of the presynaptic cells shift in parallel in accordance with the shift in position of
individual S-cells' receptive fields.
- At first, every time a stimulus pattern is presented a few "representaive" S-cells are chosen which have yielded large outputs, at most 1 from each layer.
​- The input synapses to a representative S-cell are reinforced in the same manner as in the case of r.m.s.- type cognitron 

![image](https://github.com/roses-and-thorns/BCS_Drowsiness_Detection/assets/169232982/e96b15a8-dbbb-4fa8-b7c4-5c49bdcf1bd5)

- The procedure for selecting the representatives is given below.
  - Within an S-layer, we focus on a group of S-cells whose receptive fields are close together on the input layer.
    
  - If we organize the S-planes of an S-layer as shown in Figure 4, this group of S-cells forms a vertical column within the S-layer, which we call an "S-column".
  - From each S-column, we select the S-cell with the highest output as a candidate for representation.
  - If multiple candidates appear in a single S-plane, we choose the highest output as the representative.
  - If there's only a single candidate, it automatically becomes the represantative.
  - If there are no candidates, then there are no representatives from that plane.
  - In simple words, by choosing representatives in this way, each group of S-cells focuses on a specific feature of the stimulus patterns.This prevents
     having multiple groups focusing on the same feature, which could cause redundancy. Only a few groups choose representatives at a time,
     while the rest do so for different patterns.

## Rough Sketches of working of network


![image](https://github.com/roses-and-thorns/BCS_Drowsiness_Detection/assets/169232982/56e727e5-14e6-40b0-bc2a-0fc0eac8b869)

- So , the crux of it is that, each layer identifies certain feature in the given image, as the cell that represnts that feature in a plane yields a large output.
  The following layers combine these features to identify more complex features, and finally lead to identifying the pattern by connecting various features of the pattern.

- You may wonder, if for identifying only one pattern it takes these many layers. Then it might get exponentially more difficult to accomodate identifying multiple patterns.
  But the thing is that several of these features are common to multiple patterns, you end up not needing as much of new layers as you mght have imagined.

## Computer Simulation

- In the computer simulation, they considered a seven layered network. $U_0$ -> $U_{S1}$ -> $U_{C1}$ -> $U_{S2}$ -> $U_{C2}$ -> $U_{S3}$ -> $U_{C3}$.

- Although the number of cells contained in $S_l$ is the same for every S-layer, the size of $S_l$, which is projected to and observed at layer $U_0$,
increases for the hinder layers because of decrease in density of the cells in a cell-plane.

![image](https://github.com/roses-and-thorns/BCS_Drowsiness_Detection/assets/169232982/1c677122-d9ac-4949-87e6-2da179ab9bd2)

- In order to self-organize, they provided some stimulus patterns as shown in the Fig. 6.

- All the images from a to g have generated the same result for all the different set of images. That is, the neocognitron has correctly
recognized these patterns without affected by shift in position like (a) ~ (c), nor by distortion in shape or size
like (d)~ (f), nor by some insufficiency of the patterns or some noise like (g). 


![image](https://github.com/roses-and-thorns/BCS_Drowsiness_Detection/assets/169232982/e2f7dedf-f1ea-476c-8c69-a88328473e32)


- Figure7 displays how individual cells in the neocognitron have responded to stimulus pattern "4". 

- A second experiment was done by using different forms of "X" , "Y" , "T" and "Z". They resemble each other in shape, still the neocognitron distinguished them.

- In a third experiment using "0","1"...,"9". It could have worked but it would require more than just 24-cell planes, but they couldn't do it
 due to the lack of memory space on their computer.


## Conclusion

> The "neocognitron" proposed in this paper has an ability to recognize stimulus patterns without affected by shift in position nor by a small distortion in shape
 of the stimulus patterns by self-organization ,i.e. , learning without a teacher.

Thanks for reading!
----






















 
