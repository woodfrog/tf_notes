## [Threading and Queues](https://www.tensorflow.org/programmers_guide/threading_and_queues)

- Can use **Tensorboard's graph functionality** to take a closer look at the queues in computation graphs. **Note: the computation process in Tensorflow is strictly divided into two phases. In the first phase, the graph is build where each tensor's shape is determined and each node's type and data are also decided (there can be all kinds of nodes like initializers, variables, constants, etc.). In the second phase, i.e. the running phase, the data is fed into the computation graph and flow through the graph with the form of tensors until all required operations are completed.**

- A Queue is also a node in the tensorflow graph, and other nodes (always enqueue nodes) can enqueue new items into the queue, while dequeue nodes can fetch items from it. (Queue methods like enqueue and dequeue must run on the same device as the queue itself).

- One typical usage of queue is in the input architecture of RandomShuffleQueue for preparing inputs for training a model. There are multiple threads preparing training examples and push the examples into the queue. At the same time, training thread executes training ops that constantly dequeues mini-batches from the queue. (**Many functions are implemented using this fashion. For example, the slice\_input\_producer is implemented using a Queue - a QueueRunner for its Queue is added to the current Graph's QUEUE\_RUNNER collection. And tf.train.batch also does this.**)


I use the example in tensorflow/how\_tos/reading\_data and export the computation graph and display it in Tensorboard, it's a good way to take a deeper look at how queues work. The preparing threads enqueue lots of example, and training thread fetches them to do the training operations. Below is the graph for tf.train.batch, we can see there are several operations attatched to the fifo\_queue. The training thread uses dequeue ops to fetch batches from the queue. Here the batch size is 100, the tensor has shape (100, 784) - 784 = 28 \* 28 for MNIST image.  

![](https://github.com/woodfrog/tf_notes/blob/master/reading_data/tf_train_batch.png?raw=true)


- We should use tf.train.start\_queue\_runners to start all queue runners collected in the graph.

	
	start_queue_runners(
	    sess=None,
	    coord=None,
	    daemon=True,
	    start=True,
	    collection=tf.GraphKeys.QUEUE_RUNNERS
	)	

	sess specifies the Session used to run the queue ops (default to the default session). tf.Session support multiple threads.



## [Reading Data](https://www.tensorflow.org/programmers_guide/reading_data#preloaded_data)

Three major ways for reading data:

1. Feeding use run() or eval()'s feed\_dict argument. The batches of data are generated by normal Python codes and then fed into the placeholder in the Tensorflow Graph. Errors will be raised if the corresponding placeholder is not filled with data during the evaluation process of ops. See [example](https://github.com/tensorflow/tensorflow/blob/r1.2/tensorflow/examples/tutorials/mnist/fully_connected_feed.py).

2. Reading from files.
	
	[This tutorial](https://www.tensorflow.org/tutorials/deep_cnn#prepare_the_data) and its [code repo](https://github.com/tensorflow/models/tree/master/tutorials/image/cifar10) provide quite complete information about the whole process of building input pipeline from binary data and train the model. Moreover, This tutorial also shows how to train on **multiple GPUs**.
	
	For converting other data into the standard TFRecord for later reading, check out [this tensorflow example code](https://github.com/tensorflow/tensorflow/blob/r1.2/tensorflow/examples/how_tos/reading_data/convert_to_records.py) as well as the tf.parse_single_example.
	
	As described by the reading data tutorial, the typical pipeline for reading records from files has the following stages:
	
	- The list of filenames
	- Optional filename shuffling
 	- Optional epoch limit
	- Filename queue
	- A Reader for the file format
	- A decoder for a record read by the reader
	- Optional preprocessing
	- Example queue

	Each stages of the overall pipelines are connected by several queues. **tf.train.Queuerunner**s are added to the graph. Each QueueRunner is responsible for one stage. After the graph is constructed and we want to start training, **tf.train.start_queue_runners** must be called to let the QueueRunners in the graph start its threads running their enqueueing operations. 
	
	It's also recommended to use a **tf.Coordinatior** to coordinate all the working threads. See the docs for details.
	
	

	
3. Preloaded data (only for small datasets which can be entirely held in memory). See [example](https://github.com/tensorflow/tensorflow/blob/r1.2/tensorflow/examples/how_tos/reading_data/fully_connected_preloaded.py).


