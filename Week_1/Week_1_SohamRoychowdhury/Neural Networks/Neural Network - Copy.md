# Neural Networks: A Summary

Neural networks are a class of machine learning algorithms inspired by the structure and functioning of the human brain. They are composed of interconnected nodes (neurons) organized in layers. Neural networks are capable of learning complex patterns in data and making predictions or decisions based on that learning.

![Neural-Networks-Architecture.png](../_resources/Neural-Networks-Architecture.png)

## Key Components
1. **Neurons:** These are the basic units of a neural network. Each neuron receives inputs, performs a computation, and produces an output.
Each neuron carries a value between -1 and 1 which is called the activation of that neuron. Let us denote by ***a<sup>(l)</sup><sub>k</sub>***, where l denotes the current layer to which the neuron belongs and l denotes the index of the neuron.

2. **Layers:** Neurons are organized into layers. Typically, a neural network consists of an input layer, one or more hidden layers, and an output layer.

3. **Weights:** Weights signify the weightage of  the connection among the neurons of one layer to the neurons of the next layer. Let us denote it by ***w<sub>m,n</sub>***, where n denotes the source index and m denotes the destination index.

4. **Activation Functions:** Activation functions introduce non-linearity into the neural network, allowing it to learn complex relationships in the data. It is mostly required to scale the value to a range of 0 to 1. An example may be the sigmoid function, ***σ(x)=1/(1+e<sup>-x</sup>)***


![Screenshot 2024-05-09 203301.png](../_resources/Screenshot%202024-05-09%20203301.png)



5. **Biases**: Sometimes we might require the activation function to give a stable output only when the input is greater than a certain value say ***b***. 

6. **Loss Function:** This function quantifies how well the network's predictions match the actual targets. During training, the goal is to minimize the loss function. This may be done by *Gradient Descent*.

## Working
Let ***W*** be the matrix of ***w<sup>(l)</sup><sub>m,n</sub>*** , ***a<sup>(l)</sup>*** be the column matrix of all ***a<sup>(l)</sup><sub>n</sub>***  's and ***b<sup>(l)</sup>*** be the column matrix of the biases ***b<sup>(l)</sup><sub>m</sub>*** 's. Then the activations of the next layer i.e  ***a<sup>(l+1)</sup>***  would be given as σ(***W.a<sup>(l)</sup>***+***b<sup>(l)</sup>***).

Eg: for l=0, the input looks like:


![Screenshot 2024-05-09 203420.png](../_resources/Screenshot%202024-05-09%20203420.png)



Finally the activations of the final layer is obtained. Furthermore Gradient descent is applied to minimise the cost function and get the desired output. 


