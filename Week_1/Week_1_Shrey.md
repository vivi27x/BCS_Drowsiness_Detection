

## What is a neural network?
- It is (*drumroll*) a network of neurons, where neurons are basically a variable that holds a number between 0 and 1 (more conveniently something that is a function that gives a number b/w zero and one based on the values of the previous layers)
- an image here is just a set of grayscale pixel values of a 28*28 grid, each of these pixels becomes our first layer
- there are additionally 2 hidden layers and the last result layers which predicts the likelyhood of our digits to be from 0-9
-The activation between one layer results in the activation between the next layer
- A layered structured is a good idea because ideally we can have one layer can be tuned to recognise basic edges and the next to recognise a collection of those basic edges to form structures like a loop or a line which rolls on to the last layer where different collection of structures at diff positions result in a number, for other options too a layer is a good idea for all the data that can be broken down to smaller recognisable subparts
- The correlation between one layer and the other is such that the value of each neuron in the next layer is a weighted sum of the others in the prev layer, the weights decided to recognise the activation of z certain part of the image. We also want the value of the weighted sum to be between 0 and 1 so we use a function to squish the value, here the sigmoid function was used. We also add some bias in the weighted some, a constant added if we want a neuron to lightup only after a certain limit.
- We can conveniently represent the values of the neurons of one layer as a vector and a weighted sum which turns them into neurons of the other as a matrix and add a bias vector and apply a sigmoid function to each of the values.
- These weights and biases are then found by gradient descent, training your network with some data, comparing what your function gives out and then tweaking the weights and biases on the basis of how wrong it is
- Some updates to the squishing function, Rectified Linear Unit function is used nowadays f(a) = max(0,a), which is preferred because biologically neurons turn to 0 after a certain threshold. 



## What is a convolution?
- We have two dices one cool way to visualise the cases where there comes out a specific value is listing the outcomes, flipping one list and sliding it along the other.
- if there are non uniform probabilities of the outcomes of a die, multiply the corresponding probabilities and add them up while sliding each step and noting the value this basically is a convolution
- The same process can also be used as a moving average where you slide a filter layer over a graph
- the same in 2d done to an image where a pixel is basically a vector of three values, and your filter is a matrix with numbers representing the weights given to the pixels. You slide that filter along that image and create a second image with each pixel representing the outcome of that applied filter.
- The definition implies that the output image is a convolution of the original image and a **180 degree flipped version of that kernel**
- We can blur the image if all of the entries in the kernel are the same, elegantly blur it if the numbers in the kernel are according to a gaussian dist, sharpen the image and even find the vertical or horiziontal edges if the edge entries differ in the sign.
- Computers generally take a lot of time in convolving to arrays although a Fast Fourier Transform is a Better, Faster, Stronger method to do so.
- Multiplying two polynomials, a point by point operation that takes just multiplying n terms to find out the polynomial, is the same as just figuring out the coefficients and convolving them, which takes n^2 operations.  
- So whenever we want to convolve a list of numbers, treat them as polynobials, multiply n specific terms which is omega^n, construct a system of linear equations and solve it quickly using the redundancies.
- Why multiplying numbers is basically a convolution is because we write the number as composed of 10^i, and now we can convolute the two polynomials having the same coefficients and put 10 in the result.
- 
- 
