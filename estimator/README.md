# Estimators

[Original document](https://www.tensorflow.org/programmers_guide/estimators)

[API page for the base class Estimator](https://www.tensorflow.org/api_docs/python/tf/estimator/Estimator)

## Overview

Tensorflow's Estimator is a high-level API introduced in version 1.4. It encapsulates:

* training
* evaluation
* prediction
* export for serving

And it's both device(CPU, GPU, or TPU) and platform(single machine or cluster) independent. When using Estimator, there is no need to explicitly handle Graph and Session as in the low-level Tensorflow.


Pre-made Estimator is simple to use, and the user only needs to implement a dataset importing function.

## Custom Estimators

to be continued
