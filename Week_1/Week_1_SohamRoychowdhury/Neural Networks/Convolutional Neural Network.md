# Convolutional Neural Network : A Summmary
## What is convolution?
Suppose we have a sequence ***a*** : (1,2,3) and ***b*** :(4,5,6). Let's reverse ***b*** and place it beneath ***a*** such that 4 is beneath 1. 


![Screenshot 2024-05-09 201821.png](../_resources/Screenshot%202024-05-09%20201821.png)



Now let's multiply the terms intersecting and add. Each time we will shift ***b*** one place to the right. Thus we get the sequence (4,13,28,27,18). This is what is defined as ***(a * b)***  . This may be applied to the problem of rolling two dice and calculating the probability of the sum to be equal to***n***. That would be equal to ***Σ<sup>i=n</sup><sub>i=1</sub> a<sub>i</sub> .b<sub>n-i</sub>***

## Anology for 2-D system:
We can take an example of blurring an image wherein we have a smaller matrix carrying weightages which traverses over the image and after convolution assigns a single value to the centre pixel. The same is elaborated in the picture. The column matrices indicates the original pixels' colour saturation in terms of *Red, Green and Blue*.


![Screenshot 2024-05-09 195519.png](../_resources/Screenshot%202024-05-09%20195519.png)

## FFT Convolution:
We can also observe convolution as follows:

![Screenshot 2024-05-09 200622.png](../_resources/Screenshot%202024-05-09%20200622.png)

The addition of the elements along the diagonals give the required convolution. Also we can visualize it in terms of a polynomial multiplication

![Screenshot 2024-05-09 200851.png](../_resources/Screenshot%202024-05-09%20200851.png)

But, this will still give a time complexity of ***O(N<sup>2</sup>)***. However if we solve the required number of equations using different values of x, we will get the resulting coefficients. Still it is a cumbersome process. Hence we can use Fourrier Transformation: we can substitute complex roots of unity in place of x resulting in a reduced time complexity of ***O(N log(N))***.





![Screenshot 2024-05-09 201713.png](../_resources/Screenshot%202024-05-09%20201713.png)



