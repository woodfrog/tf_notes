## Some notes on training 

### Conventional training loss and validation loss 
By convention, the printed training loss is always the average loss of previous
steps while the validation loss is the loss for the current step(a single step).
So it's reasonable that the training loss will be greater than validation loss
at the begining stage of training.


### Saving and Restoring

It almost suffices to use tf.train.Saver for save model parameters and restore pre-trained model.

[A more detailed blog](https://blog.metaflow.fr/tensorflow-saving-restoring-and-mixing-multiple-models-c4c94d5d7125) on this topic.

### Debug and TensorBoard

- tf.summary.FileWriter for writing summary information which can later be used by TensorBoard.

- [Official tutorial](https://www.tensorflow.org/programmers_guide/debugger) on how to use tfdbg for various purposes, it's a quite useful tool!