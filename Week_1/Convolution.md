# Convolution<br>
Give two functions and I can add, subtract, multiply and divide them to get a new function but do you know about an equally fundamental operation to get a new function. Yeah I'm talking about Convolving them.<br>
**(f<sub> * </sub>g) = integration -infinity to +infinity of f(x)g(t-x)dx**<br>
Although the defining formula might seem daunting, the idea is pretty basic.<br>
Lets take an example an array A = [3,5,7,11,13,17,19] and array B =[1,2,4]. Convolving A and B is like Sliding B under A and taking the weighted sum of the enteries of A with corresponding weights in B.<br> 
Output is an array whose first entry is (3* 1 = 3) and second entry is (5* 1+ 3* 2+  = 11) and so on.
But what does it mean ?<br>
It is like taking weighted average of few entries of A at a time in an order.<br>
It can be seen as a smoothed out version of original data like if we did this on an image, we will get blurred images as each pixel will be of average brightness of the group of pixels in the original image.<br>
But in the vast forest of application of convolution, blurring is just a leaf.<br>
One use is edge detection.<br>
**WHAT CONVOLUTING NEURAL NETWORK?**<br>
It is basically a NN which uses available data to find suitable **Kernel** i.e the matrix using which you will convolve the image.<br>
WHAT IS FFT CONVOLVE ?<br>
Try doing convolution of 2 array of not so little size, you will find the task to be boring, tedious and time consuming. So instead of directly computing convolution, we use FFT.<br>
One can see convolution as multiplication of 2 polynomial functions with the array representing the coefficients. And therefore the resulting function obtained on multiplication is the required function whose coefficients represent the convolved array.<br>
Where is the use of FFT?<br>
We use point wise operation of the few outputs of 2 polynomials to get few data points and then use inverse FFT to recover a polynomial from those data points. It will be the required polynomial whose coefficients  will represent the convolved array.<br>
THANK YOU.<br>