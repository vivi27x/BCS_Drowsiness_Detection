# Research Paper Notes

## Inspiration
The idea of developing the model has been derived from the crucial need for a mechanism that could identify patterns irrespective of the presence of much noise and more importantly, change in position of the pattern.
The pattern can involve alphanumeric characters, shapes, etc. Also, it admires the real-life brain structures and how it works and the knowledge we had about it in those times ( mainly from physiology and some psychological experiments ).

## Structure of the Network
1. Each module consists of 2 layers, the S-layer ( simple or lower order hypercomplex cells ) and the C-layer ( complex or higher order hypercomplex cells ). For the l<sub>th</sub>-module, we denote these layers by U<sub>Sl</sub> and U<sub>Cl</sub> respectively. We also have a terminology for this i.e. S-plane and C-plane.
2. The input layer ( U<sub>o</sub> ) consists of photoreceptor cells, and their output is denoted by u<sub>o(n)</sub> where n is (n<sub>x</sub>,n<sub>y</sub>) i.e. the coordinates describing location of cell.
3. The S cells have modifiable synapsis ( terminology: have plasticity ), while this isn't true in the case of other cells.
4. The receptive field of the cells becomes bigger as we proceed to deeper layers.
5. The number of cells in the layer decreases as we proceed to deeper layers.

![structure.jpeg](https://github.com/KrishJain256/BCS-Drowsiness-Detection/blob/master/structure.jpeg)

## Mathematics
1. The output of an S-cell in the k-th S-plane of l-th module can be figured out to be

![cell_output.jpeg](https://github.com/KrishJain256/BCS-Drowsiness-Detection/blob/master/cell_output.jpeg)

2. The inhibitory cell v<sub>C l-1 (n)</sub> having inhibitory synapsis to the S-cell have an r.m.s type of output shown below. This inhibitory cell connects the C cell of the previous layer to the S cell of the current one.

![inhibitory_output.jpeg](https://github.com/KrishJain256/BCS-Drowsiness-Detection/blob/master/inhibitory_output.jpeg)

3. The C-cell output of the same layer in same module.

![c-output.jpeg](https://github.com/KrishJain256/BCS-Drowsiness-Detection/blob/master/c-output.jpeg)

4. Now, we can illustrate the output of the inhibitory cell that connect the S cell of the current layer to the C cell of the same layer.

![s to c inhibitory output.jpeg](https://github.com/KrishJain256/BCS-Drowsiness-Detection/blob/master/s%20to%20c%20inhibitory%20output.jpeg)

## Self organisation of the Network
Self organisation helps the model to recognize the patterns irrespective of change in position.
#### Procedure
1. In a S-layer, we watch a group of S cells. If the S planes are aligned to each other like a stack, we see that the receptive fields form a column structure.

![columns.jpeg](https://github.com/KrishJain256/BCS-Drowsiness-Detection/blob/master/columns.jpeg)

2. From each S-column, the cell showing the largest output is chosen as a candidate for the representatives. If no candidate appears in a plane, no representative is selected.
3. The input synapses to the representatives are reinforced.
4. All the other cells of the plane from which representative is selected have their inputs reinforced in the same way as the representative.
5. Even if one S-cell shows a high value, the next corresponding C-cell activates and hence, the pattern can be detected even when there is a change in the position of the pattern.

## Rough Working Diagram
1. Lets assume that the model has been self-organised and is shown patterns like "A","B",etc. repeatedly.
2. So, now when we pass the pattern "A" again

![visualize.jpeg](https://github.com/KrishJain256/BCS-Drowsiness-Detection/blob/master/visualize.jpeg)

3. Since the explanation now given in the paper was quite easy to comprehend, attaching the exact text.

![exp1.jpeg](https://github.com/KrishJain256/BCS-Drowsiness-Detection/blob/master/exp1.jpeg)

![exp2.jpeg](https://github.com/KrishJain256/BCS-Drowsiness-Detection/blob/master/exp2.jpeg)

#### Optimization and Scalabiity
Since, we need to detect a large number of patterns, we really do need to think about the scability of the algorithm. It comes out that, sicne the patterns would share common subpatterns like lines and arcs, it would be fine and the mechanism won't break for a larger set of characters, I mean patterns.

## Computer Simulation
#### Stats
1. We produce a seven layered network : U<sub>o</sub> → U<sub>S1</sub> → U<sub>C1</sub> → U<sub>S2</sub> → U<sub>C2</sub> → U<sub>S3</sub> → U<sub>C3</sub>
2. Number of cell planes in each layer is 24 except for the input layer.
3. The numbers of excitatory cells in these seven layers are: 16 x 16 in U<sub>o</sub>, 16 x 16 x 24 in U<sub>S1</sub>, 10 x 10 x 24 in U<sub>C1</sub>, 8 x 8 x 24 in U<sub>S2</sub>, 6 x 6 x 24 in U<sub>C2</sub>, 2 x 2 x 24 in U<sub>S3</sub>, and 24 in U<sub>C3</sub>. In the last layer U<sub>C3</sub>, each of the 24 cell planes contains only one excitatory cell (i.e. C-cell).
4. The number of cells contained in the connectable area S<sub>l</sub> is always 5 x 5 for every S-layer. Hence, the number of input synapses 3 to each S-cell is 5 x 5 in layer Usl and 5 x 5 x 24 in layers U<sub>S2</sub> and U<sub>S3</sub>.

Below is a mapping of the state of the last layer for different input patterns.

![mapping.jpeg](https://github.com/KrishJain256/BCS-Drowsiness-Detection/blob/master/mapping.jpeg)

If we try to give "4" as the input pattern, the below image shows the progressive state of every layer.

![try4.jpeg](https://github.com/KrishJain256/BCS-Drowsiness-Detection/blob/master/try4.jpeg)
