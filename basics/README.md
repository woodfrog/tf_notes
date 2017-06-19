## The usage of some tf basic operations

- tf.split
		split(
    		value,
    		num_or_size_splits,
    		axis=0,
    		num=None,
    		name='split'
		)
		This operation splits the value tensor into several sub-tensors. 
		num_or_size_splits can be either a number or a 1-D tensor to specify the method for splitting.
		The return value is a list of tensors containing the results of splitting.

- tf.concat
		concat(
		    values,
		     axis,
		    name='concat'
		)
		Concatenates tensors along one dimension.
		values should be a list of tensors to be concatenated.
		axis specifies the dimension to be concatenatedi (the index in the shape).	


- tf.expand\_dims
		expand_dims(
	    		input,
	    		axis=None,
	    		name=None,
	    		dim=None
		)
		Insert a dimension of 1 at the dimension index axis of input's shape. If we want to insert at the tail, can you negative index.	
	

- tf.squeeze
		squeeze(
		    input,
		    axis=None,
		    name=None,
		    squeeze_dims=None
		)	
		Removes dimensions of size 1 from the shape of the input tensor.
		Or we can use axis to specify the dimensions for removing 1.

- tf.tile
		tile(
	    		input,
	    		multiples,
	    		name=None
		)	
		Constructing a new tensor by tiling the given input tensor.
		It replicates input **multiples** times. 
		The shape of multiples should be the same as input. Then the corresponding dimensions of input will be replicated. 


- tf.reduce\_sum
		reduce_sum(
		    input_tensor,
		    axis=None,
		    keep_dims=False,
		    name=None,
		    reduction_indices=None
		)
		Reduces input_tensor along the dimensions given in axis. Unless keep_dims is true, the rank of the tensor is reduced b		y 1 for each entry in axis. **If keep_dims is true, the reduced dimensions are retained with length 1.**
		keep_dims is useful for operations like normalization, since we have to compute the sum of entries along some axises a		nd then applying elementwise multiplication.
	

- tf.gather 

	gather(
	    params,
	    indices,
	    validate_indices=None,
	    name=None
	)

	Gather slices from params according to indices.
	indices should be an integer tensor of any dimension, but usually 0-D or 1-D. 
	The output has the shape indices.shape + params.shape[1:]
