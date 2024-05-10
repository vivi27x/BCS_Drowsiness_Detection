# Week – 1 Tasks 

### Intro to neural networks 

Neural networks, as the name suggests, are a network of “neurons” mimicking the functioning of the human brain. They are built to perform functions that might seem effortless and straightforward to a human but complicated to a computer. An example of such a task is recognition of hand-written numbers.  Let’s look at the structure of a neural network suited to perform this. 

The first layer consists of 28x28 (the number of pixels in the square grid in which the number is written) neurons whose activation ranges from 0 to 1 depending on how “lit” the pixel is. The last year consists of 10 neurons each representing each number (category). The layers in between are known as “hidden layers”. 

Now, what does each layer do? Any number can be split into components (like loops and lines) and these components can further be split into subcomponents (for example, a loop is collection of smaller lines). Each layer recognises components, gets activated accordingly and influences the next for piecing the data together and eventually recognizing the digit in the final layer.  

This makes us question, how this “influencing” happens. This is achieved by the acquired values of “weights” and “biases”.  

Weights decide how strong the positive or negative influence of a neuron is on another of the subsequent layer. For example, to pick up an edge, the weights of the pixels at the edge are positive and around it are negative. To squish this weighted sum to a value between 0 and 1, it is manipulated using the sigmoid function which results in a value close to 0 if the sum is negative and a value close to 1 if the sum is positive. 

Moreover, to make sure a neuron is meaningfully activated only when the weighted sum is more than a particular value, a threshold value called the “bias” is added to the sum before being passed into the sigmoid function. Learning refers to acquiring the right weights and biases through training. 

 

A mathematical notation of the above concept is the multiplication of the weights matrix with the column matrix of activation values of the neurons of a layer. Then adding the bias matrix followed by passing the resulting matrix into the sigmoid function. 

The video concludes with Lisha Li mentioning that modern systems use ReLU which is max (0, a) in place of sigmoid as it is easier to train using the former.  

 

### What is Convolution? 

The simplest definition of a convolution is it is a way of combining two arrays of numbers. So how is a convolution performed? First, flip the second matrix. Then, compute the sum of the product of the elements that align. Repeat using different offsets to produce the convolution. 

Furthermore, convolution has a variety of applications that include adding two probability distributions, calculating a moving average inside a little window to smoothen out the data. The second application can also be implemented using a 2D matrix to blur images. The “little window”, known as the kernel, refers to a smaller matrix that is multiplied over the bigger matrix (In this case a picture). Its values can be changed to obtain different results. 

The 2D blur obtained using a matrix with equal entries that add up to one can be further refined by using values corresponding to a Gaussian distribution. Moreover, a kernel with a positive left column, zero middle column and a negative right column can be used to detect vertical edges. Similarly, a kernel with a positive top row, zero middle row and a negative bottom row can be used to detect horizontal edges. 

Not only can convolution be used to blur images but also it can be used to sharpen them. Part of processing using a CNN involves determining the right kernel. 

Another crucial point is the length of the output. When convolving an array of length n with another of length m, we obtain an array of length n+m-1. However, in the context of computer science, we must truncate some part of the resulting array such that its size matches the biggest input size. 

While convolving involves steps of the order N, another method known as FFTconvolve involves steps of the order Nlog(N) and hence speeding up the process for colossal arrays.  

The FFTconvolve method is mathematically explained by the relation between convolution and the coefficients in polynomial multiplication. We already know that we can find the coefficients of a polynomial resulting from f.g by using convolution. We also know that any polynomial of degree n can be found if given n+1 points that satisfy it. Thus, we can calculate the coefficients directly using sample points to find the convolution. This is further simplified by using roots of unity (Fast Fourier Transform). 

The structure of a fftconvolve is as follows.  Fast Fourier transform both arrays considering the elements as coefficients of polynomials. Then, multiply the obtained arrays point-wise. Then, use inverse FFT to find the convolution. 

The video concludes with an additional insight that multiplication is also a kind of convolution and hence multiplication of large numbers can be simplified instead of using old school methods of multiplying digit by digit. 

 

 