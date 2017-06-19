## [Threading and Queues](https://www.tensorflow.org/programmers_guide/threading_and_queues)

- Can use **Tensorboard's graph functionality** to take a closer look at the queues in computation graphs. **Note: the computation process in Tensorflow is strictly divided into two phases. In the first phase, the graph is build where each tensor's shape is determined and each node's type and data are also decided (there can be all kinds of nodes like initializers, variables, constants, etc.). In the second phase, i.e. the running phase, the data is fed into the computation graph and flow through the graph with the form of tensors until all required operations are completed.**

- A Queue is also a node in the tensorflow graph, and other nodes (always enqueue nodes) can enqueue new items into the queue, while dequeue nodes can fetch items from it. (Queue methods like enqueue and dequeue must run on the same device as the queue itself).

- One typical usage of queue is in the input architecture of RandomShuffleQueue for preparing inputs for training a model. There are multiple threads preparing training examples and push the examples into the queue. At the same time, training thread executes training ops that constantly dequeues mini-batches from the queue. (**Many functions are implemented using this fashion. For example, the slice\_input\_producer is implemented using a Queue - a QueueRunner for its Queue is added to the current Graph's QUEUE\_RUNNER collection. And tf.train.batch also does this.**)


I use the example in tensorflow/how\_tos/reading\_data and export the computation graph and display it in Tensorboard, it's a good way to take a deeper look at how queues work. The preparing threads enqueue lots of example, and training thread fetches them to do the training operations. Below is the graph for tf.train.batch, we can see there are several operations attatched to the fifo\_queue. The training thread uses dequeue ops to fetch batches from the queue. Here the batch size is 100, the tensor has shape (100, 784) - 784 = 28 \* 28 for MNIST image.  

![](https://github.com/woodfrog/tf_notes/blob/master/reading_data/tf_train_batch.png?raw=true)

## [Reading Data](https://www.tensorflow.org/programmers_guide/reading_data#preloaded_data)


