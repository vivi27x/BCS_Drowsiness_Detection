
# Neural Networks 
### Need for Neural Networks 

![Screenshot 2024-05-09 152912](https://github.com/roses-and-thorns/BCS_Drowsiness_Detection/assets/169232982/b875e019-5bd0-4aca-b888-7c8b922a051d)

It's fascinating how our brain can look at all three of the images and conclude they all represent the same number (i.e., 3). However, it would seem daunting if you were tasked to write a code that could also do that for you. That's where Neural networks come in.
### Structure and Functions
- Composed of a network of neurons arranged in layers.

- A neuron is like a cell holding a value(activation value) from 0 to 1.
- A lit(or active) neuron has a higher activation value.
- All neurons in a layer are connected to each neuron in the next layer.
- The first layer(input layer) consists of all neurons corresponding to the input image.
- The last layer(output layer) consists of ten neurons each representing a digit from 0 to  (the activation value indicating how likely the computer thinks the image represents that number).
- The intermediate layers(hidden layers) contain neurons that try to identify other fine features in the images (like edges or loops in the images) which interconnect to help identify the number.

 ![image](https://github.com/roses-and-thorns/BCS_Drowsiness_Detection/assets/169232982/a53a505e-7254-4fce-8efb-8d18871f286c)

### Weights and biases
Each connection between neurons has a specific 'weight' assigned to it. Then the weighted sum of all the activations in the first layer is calculated. Sometimes we want the sum to be greater or less than a certain value for it to be considered, in that case, a number called 'bias' is added. This sum represents the activation of the neuron in the next layer. To get it between 0 and 1, we use the sigmoid function $\sigma$(x) = $\dfrac{1}{1+e^{-x}}$.

### Notations and Linear Algebra
Writing the complete weighted sum for each neuron is a bit cumbersome. So instead, we use matrix notations for representing the weights, bias, and activations. The formula then would be 

$$ A_{n+1} = W \cdot A_n + B $$


where,

$$
A_m = 
\begin{pmatrix}
a_{1,m} \\
a_{2,m} \\
\vdots \\
a_{n,m}
\end{pmatrix}
$$

$$
W_{m,n} = 
\begin{pmatrix}
w_{1,1} & w_{1,2} & \cdots & w_{1,n} \\
w_{2,1} & w_{2,2} & \cdots & w_{2,n} \\
\vdots & \vdots & \ddots & \vdots \\
w_{m,1} & w_{m,2} & \cdots & w_{m,n} 
\end{pmatrix}
$$

$$
B = 
\begin{pmatrix}
b_1 \\
b_2 \\
\vdots \\
b_n
\end{pmatrix}
$$

 The attached screenshot explains it :
 
 ![Screenshot 2024-05-09 180453](https://github.com/roses-and-thorns/BCS_Drowsiness_Detection/assets/169232982/0aa369d6-82d5-4227-802a-d0794b6f0c9c)



# Convolution
It's a way of combining two different lists of numbers.
#### Formula 


$$ (f \ast g)(n) = \sum_{m=1}^{n} f_m \cdot g_{n-m} $$


or for continuous lists(functions) :
$$(f \ast g)(t):=\int_{-\infty}^{\infty} f(\tau) g(t-\tau) d \tau$$

- [1, 2, 3] $\ast$ [4, 5, 6] = [4, 13, 28, 27, 18]
### Examples

To understand it better let's take the example of rolling a pair of dice,  each die has its own set of probabilities for a number to show up. To find the probability that the sum of numbers adds up to a particular number, we can use convolution. It's like the sliding window approach.
 
 ![Screenshot 2024-05-09 185821](https://github.com/roses-and-thorns/BCS_Drowsiness_Detection/assets/169232982/b29b6297-9b00-41e4-947e-68f5bb9b1a43)

Another application of convolution is __moving average__.
It helps in smoothening out a graph. You take a list of let's say 5 numbers each having the value 0.2. After convolving with the original function, you'll get a smoothened version of the list. 

![image](https://github.com/roses-and-thorns/BCS_Drowsiness_Detection/assets/169232982/d15af170-2d93-4e13-97ca-995c153d8491)


![image](https://github.com/roses-and-thorns/BCS_Drowsiness_Detection/assets/169232982/3b29c221-6811-4ff7-b9fc-5765233623fd)

Repeating the same thing with a 3 x 3 grid in a 2-D image will give a blurring effect, as it takes an average of all nearby squares.

![image](https://github.com/roses-and-thorns/BCS_Drowsiness_Detection/assets/169232982/4411bfa1-28ba-4385-a391-4b342031c639) 
 
 In image processing context the 3 x 3 grid chosen is called kernel.
 with different kernels, you get different effects.
![image](https://github.com/roses-and-thorns/BCS_Drowsiness_Detection/assets/169232982/3658b222-0b90-46da-b332-b25adbdfaca6)


### FFT Convolve

One thing to notice is that when you multiply two polynomials together, the coefficients of their products can be found by convolving the products of the polynomials.

The time complexity of normal convolution methods are $O(n^2)$, but in FFT we use the polynomial multiplication analogy, by finding the polynomial by multiplying both lists and using the values at different points to find the function. 
We can find a polynomial of degree n if we know its value at n different points, but it can be a bit difficult to calculate. For this, we use the Discrete Fourier Transform. This helps to perform the operation in $O(n*log(n))$ time complexity.

![image](https://github.com/roses-and-thorns/BCS_Drowsiness_Detection/assets/169232982/27d5a088-4d26-449c-b930-aa092d964ef2)


To summarize the FFT algorithm :

![image](https://github.com/roses-and-thorns/BCS_Drowsiness_Detection/assets/169232982/5348ab56-8de9-430a-9ab3-477fb690d0b3)
---
