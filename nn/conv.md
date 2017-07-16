# Details about Convolution layers

[A good tutorial for various kinds of convolutional layers](http://deeplearning.net/software/theano/tutorial/conv_arithmetic.html)


## About Transposed Convolution

- Convolution can be expressed with a matrix C composed of the filter elements.

-  Think about how backprop is done for conv layers (actually with the matrix C, the computation for conv layers is quite similar to that of fc layers). In the forward pass, activations and result of applying activation functions are computed and stored. **During the backward pass, dErr/d(activation) is computed from tail to head. This part can be achieved by multiplying the transpose of C with the loss of the next layer.**

*Note from the tutorial: The transposed convolution operation can be thought of as the gradient of some convolution with respect to its input, which is usually how transposed convolutions are implemented in practice.*

*Finally note that it is always possible to implement a transposed convolution with a direct convolution. The disadvantage is that it usually involves adding many columns and rows of zeros to the input, resulting in a much less efficient implementation.*

Look at the tutorial for visualization!

