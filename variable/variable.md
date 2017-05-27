## Variables

Some notes taken when reading [tensorflow programming guide's variable section](https://www.tensorflow.org/programmers_guide/)

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

This subsection is about the usage of tf.variable_scope() and tf.get_variable()
and how can they help when we intend to share large sets of variables.

1. tf.get_variable(<name>, <shape>, <initializer>): creates or returns a variable
with the given name.

2. tf.variable_scope(<scope_name>): manages namespaces for names passed to
   get_variable()

For more details, see the ipython notebook for concrete examples.

3. Set the reuse = True if we want to reuse some variables inside certain name
   scope.

4. The mechanism of tf.get_variable(). 
    * case1: the reuse state for the current name scope is False, so it will
      create new variable with the provided shape and data type. And the name
      will be scope name + 'name' parameter of the variable. If a variable with
      the same full name already exists, the function raises a ValueError. 

    * case2: the reuse state for the current scope is True. Then the
      get_variable function will search for an existing variable with the
      specified name. If no such variable exists, a ValueError will be raised
      again.

5. The variable scope influences both variable names and op names, while the
   name scope only have impacts on the name of ops but not variables.


