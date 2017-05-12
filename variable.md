## Variables


### Creation and Initialization 

1. tf.Variable always requires the shape of the tensor to be specified. And this
   is done by passing a tensor as the initial value to the Variable()
   constructor.

2. Calling tf.Variable() adds some ops to the graph:
    * A variable op that holds the variable value.
    * Initializer op for setting the variable's initial value (actually a
      tf.assign op).
    * ops for initial value such as zeros op.

3. Devide placement for variable. The variables can be placed on specified
   device using a **with tf.device** context manager.

4. Run the initializer. All the initializer must be run explicitly (cus they are
   essentially all ops ). This can be achieved by setting a global variable
   initializer and run it in our session.


### Saving and Loading

1. To easily save and restore a model, we can use tf.train.Saver object. It's
   constructor adds **save** and **restore** ops to the graph for all, or a
   specified list, of variables in our graph. And this object also provides us
   corresponding methods to run these operations to read and write our variables
   from/to checkpoint files.

2. Use 'tf.train.Saver()' to instantiate a saver which manages all variables in
   the model. And use 'saver.retore()' to restore variables from checkpoint
   files.

### Sharing Variables 
