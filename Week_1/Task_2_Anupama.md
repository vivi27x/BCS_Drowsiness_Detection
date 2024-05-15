## Notes on the Research paper 

#### 1. From the title: 
* Neo-cognitron 
* Self – organizing 
* Pattern recognition 
* Unaffected by position 

#### 2. From the abstract: 
* Struct like hierarchal model of visual nervous system proposed by Hubel and Wiesel 
* Input layer/photoreceptor array –> modules 
* Each module – 2 layers - Simple cells + Complex cells 
* Each C-cell of the last layer responds to only one pattern 

#### 3. From the introduction: 
* Neocognitron – further extension of cognitron 
* Hubel Wiesel model – LGB -> S cells -> C cells -> lower order hypercomplex cells -> higher order hypercomplex cells 
* Lower-higher connection is similar to Scell-Ccell connection 
* HW model not completely true, but the main stream of info flow can be adopted 
* HW model doesn’t tell us about cells in stages higher than higher order hypercomplex cells. 
* Cells in inferotemporal cortex – responds selectively to more complicated features – called “grandmother cells” 
* Neocognitron – extended hierarchy structure – position-invariant pattern recognition in even the deepest layers 

#### 4. From the conclusion: 
* Recognition without effect of position or small distortion 
* Self-organization – no teacher 
* Acquires ability to recognize by learing repeating patterns 
* In the human brain, diff ways to recognize native and foreign alphabets. Model presents a NN like former. 
* Future problem: deciphering illegible letters 

#### 5. Structure of the network 
* Cascade connection of modular structures (lth module = S layer USl+ C layer UCl) preceded by input layer Uo  
* S-cells and C-cells put into subgroups called “cell-plane” according to optimum stimulus features 
* All cells in a single plane look for a specific pattern but at dfferent positions 
* If a stimulus that evokes a response from one S cell is shifted in position, it evokes a equally large response from some other S cell in the same plane. So, the corresponding C cell will respond as before. 

#### 6. Self-organization of the Network 
(I have not included the mathematical part because I did not understand it)
* Network is presented with a set of stimulus patterns 
* When a stimulus pattern is presented: 
    * “Representative” S-cells are selected based on 
        * Large outputs 
        * Not more than one per S-plane 
    * Input synapses to representative S cells and other S cells on the same plane are reinforced 
    * No changes are made to planes from which there are no representative cells 
    * S column – S cells belonging to multiple planes that have the same receptive field 
    * How are representatives selected?
        * For each S column, S cell yielding the largest output is selected 
        * If more than 1 of the same plane are selected, the brightest one is chosen. 
        * If only 1 is selected, it is chosen unconditionally. 
        * If no candidate is selected, then it is left as it is. 
        * This way, redundancy is avoided. 

#### 7. Rough sketches of the working of the network 
* Let’s say A is the input 
* S1 plane picks up ^ shaped features. A S cell near the top would have picked it up. 
* A C cell in C1 has connections with a group of cells in S1. Hence, the C cell responds to ^ feature situated in a certain area. 
* The same procedure follows for all other features also. 
* In the next module, each S cell receives signals from all the C planes 
* More complicated shapes are detected after piecing together the information from the previous module. 
* This repeats and then eventually A is detected. 
* As we go deeper into the network, the receptive field becomes wider implying more tolerance towards position shift. 
* Dealing with distortion: 
    * Even if the input pattern does not entirely match the learned pattern, neocognitron can still figure it out. 
    * This is because initial receptive fields are smaller. 
    * Hence, even if only the topmost and bottommost parts match, it can make it out. 
    * Hence, it can tolerate little distortion in shape. 

#### 8. Computer simulation 
* 7layered network (input + 3 modules) 
* No. Of cell planes = 24 (in all except input layer) 
* No. Of excitatory cells: 
    * Input layer = 16x16 
    * S1 = 16x16x24 
    * C1 = 10x10x24 
    * S2 = 8x8x24 
    * C2 = 6x6x24 
    * S3 = 2x2x24 
    * C3 = 24 
* Connectable area of a S layer has 5x5 cells 
    * All S cells in US1 have 5x5 input synapses from U0 
    * All S cells in US2 and US3 have 5x5x24 input synapses from UC2 and UC3 respectively 
    * The no. of excitatory synapses to each C cell is 5x5 in C1 and C2 and 2x2 in C3 
    * Every S column contains 5x5x24 cells in S1 and S2 and 2x2x24 cells in S3 
* This model works well with 0-4 
* This works fine even when similar patterns like X,Y,Z are presented 
* It also works when number of stimulus is increased to 0-9 
    * In this case though, a small deviation affects the output 
    * This means, number of cell planes are not sufficient 
