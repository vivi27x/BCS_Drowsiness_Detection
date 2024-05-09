# Neural Networks(by:Vishwas Pathania)
neural networks are inspired by brain.
In this video we will learn how neural networks are used for recognition of handwritten numbers.
- Neuron: A thing that holds a number(between 0 and 1).

#### how the network works:
> - A network starts with a bunch of cells that respond to each input of a 28*28 pixel image i.e. 784 neurons in total. 
> - each one of them carries a number representing the gray scale value which each pixel responds(ranging from 0 to 1) this number is called its **activation**.
> - these 784 neurons make up the first layer of the network.
> -  the last layer has 10 neurons each with a digit.
> - in between there are hidden layers. here we have taken two hidden layers with 16 neurons each.  
> - these all layers are connected and the firing on one layer causes firing of others.

a look of neural network:




![Screenshot 2024-05-08 161147.png](./Screenshot%202024-05-08%20161147.png)




 
#### what are the functions of the hidden layers:
the neurons in the first layer corresponds to edges of digits and the neurons the second hidden layer corresponds to loops and lines. these two layers light up a digit in the output layer.
basically there is some mechanism that can identify edges in pixels and convert edges into patterns and patterns into numbers.
#### weights and biases:
**weight** is assigned to each connections. these weights are numbers. then a weighted sum is calculated. now we need a value between 0 and 1 so a function called **sigmoid function** is used which squishify the weighted sum.sigmoid function  gives value near one when the weighted sum is positive but waht if we want activation meaningfull when weighted sum is greater than a specific value then we add a this specific value and this value is called **bias** 
> - every neuron in the second layer will be connected to all 784 neurons in the first layer and each of these 784 connections has its own weight and each one has a bias.
> - 784 * 16 + 16 * 16 + 16 * 10 weights.
> - 16+16+10 biases.

the maths behind this:




![Screenshot 2024-05-08 161109.png](./Screenshot%202024-05-08%20161109.png)




# Convolution
- formula: (f*g)(t)=integration{f(x).g(t-x)dx}

**visualisation:**





![Screenshot 2024-05-08 173750.png](./Screenshot%202024-05-08%20173750.png)





let's take a simple example of rolling a pair of dice:
> it will give 36 combinations. if we place the outcomes in a grid like shown in the image all the pairs that have a constant sum are seen along a diagonal. other method is to use sliding window concept.

convolution of (ai) and (bi) is shown in the **image**





![Screenshot 2024-05-08 173937.png](./Screenshot%202024-05-08%20173937.png)





(1,2,3)*(4,5,6)=(4,13,28,27,18)
Another common example:
**a moving average:** imagine if you have a long list of numbers and you take another list of numbers that all add up to one(five values and all equal to 1/5) then if we do sliding window convolution process then we are taking average of this data inside this small window as shown in the **figure**.





![Screenshot 2024-05-08 174043.png](./Screenshot%202024-05-08%20174043.png)





If we do the same on an image grid with a 3 cross 3 matrix each with value 1/9 then what basically is happening is each 1/9 is getting multiplied by each pixel on which it sits and the pixel is thought of vectors of three values then we are adding all these multiplied vectors which gives average on each color channel.this eventually will give a blurring effect.
#### fft convolve:
- it takes less time than other convolve functions
>- in simple convolution we multiply two polynomials with the coeffients given.but if we have two  big polynomials of n coefficients then the convolution  will take O(n^2).
>- now we need finite samples to get the coefficients. for eg: two outputs are enough to uniquely specify a linear polymail and 3 for quadratic.basically  we need to have the same number of coefficients as the number of equation.
>- but solving this would be difficult
>- now what fft uses is the idea that you choose to evaluate on avery specially selected set of complex numbers,the ones that sit evenly spaced on the unit circle.

visualisation:





![Screenshot 2024-05-08 174139.png](./Screenshot%202024-05-08%20174139.png)




