# Neural Networks <br>
**MOHIT** : Why did the neural network choose plain vanilla architecture ? <br>
**WILLIAM** : hmmm....why??<br>
**MOHIT** : Because sometimes, simplicity is the "key-relu-sation" to success!<br>
**WILL** : What's that brudda ! <br>
**MOHIT** : Lemme explain....(clears this throat)<br>
# So What are Neural Networks ?<br>
In the midst of solving an assignment when you think of searching the question on Google, have you ever thought how you Google lens detects what you have written ?<br>
Well let us take a simple example, say you have a handwritten digit umm say 9, what you feed to the computer is basically an image of the digits written( in our case say the image is 28x28 pixels and each pixels is a number between 0 and 1 where 0 is black and 1 is white/fully lit up) and we know image is a 2D array of pixel with correspoding values.<br>
Lets use Plain Vanilla NN aka Multilayer perceptron. so that first layer will have 784 neurons with all the values and our goal is that the last layer has 10 neurons and the brightest neuron will be the output.<br>
How this happens is the unique combinations of neurons in first layer determine the **activation** of the neurons in the 2nd layer and same goes on.<br>
Lets dive deeper, what the NN uses the 2D array to detect specific components such as straight line, loops, ends etc. and then uses its knowledge of training for ex. an 8 consists of 2 loops and a 9 consists of a loop and a line.<br>
For detecting components, NN basically uses edge detection.<br>
Coming back to the layer to layer relation, basically any neuron in a layer is crudely the **weighted sum** of the neurons in the layer before it. To ensure the weighted sum is between 0 to 1, we feed it into the **Sigmoid** function. Also we want that after only certain value of weighted sum, the neuron fires up, it is called the Bias.<br>
Basically what the function looks like is **a<sup>1</sup> = sigma(Wa<sup>0</sup> + b)** where b is the bias and W is weight associated.<br>

Overall you can think of neuron as a thing that holds a number or better say it is a function that takes input and output number.<br>
Find it complicated? Who said human life is easy ><.<br>
Thank you.<br>