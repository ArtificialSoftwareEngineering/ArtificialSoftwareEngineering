# Source Code Generators with Deep Autoregressive Models

> *Last update:* December 3th 2020; *Maintaned by* @danaderp

## The granularity problem in autoregressive models
When we try to train a generative net from source code, the tensor configuration for source code follows the same guidelines of Natural Language. For example, a RNN "reads" a sequence of characters (or tokens) to start the training. Usually, the documents used for the training are assembled into a unique file and the file is segmented into sequences of *n* length. We rely on the fact that these sequences have complete meaning since the sequences are derived from a complete semantic text. However, when we use the searchnet dataset, we are facing a distinct problem. The search net dataset is composed of methods. Methods that might not have a complete semantic context. That is, the methods are missing of classes, packages, or relevant project information. When we create the sequences from methods, we need to -at least- preserve the information within the method. We must use the entire set of tokens that compose each method so that the RNN extrapolates a hidden feature from the data. 

If we are training a Deep Neural Net with a method granularity, the tensor representation must corresponds to the requirements of such dataset to preserve the most information. Therefore, if the dataset changes in the future, the tensor representation must change as well. 
