# Source Code Generators with Deep Autoregressive Models

> *Last update:* December 3th 2020; *Maintaned by* @danaderp

## The granularity problem in autoregressive models
When we try to train a generative net from source code, the tensor configuration for source code follows the same guidelines of Natural Language. For example, a RNN "reads" a sequence of characters (or tokens) to start the training. Usually, the documents used for the training are assembled into a unique file and the file is segmented into sequences of *n* length. We rely on the fact that these sequences have complete meaning since the sequences are derived from a complete semantic text. However, when we use the searchnet dataset, we are facing a distinct problem. The search net dataset is composed of methods. Methods that might not have a complete semantic context. That is, the methods are missing of classes, packages, or relevant project information. When we create the sequences from methods, we need to -at least- preserve the information within the method. We must use the entire set of tokens that compose each method so that the RNN extrapolates a hidden feature from the data. 

If we are training a Deep Neural Net with method granularity, the tensor representation must corresponds to the requirements of such dataset to preserve the most information. Therefore, if the dataset changes in the future, the tensor representation must change as well. 

We must assume that the source code has a sequence-based nature and, therefore, we must treat it as such. We are not taking into account any structural information contain in the source code. 


## RNN and Transformers in interventional studies

We cannot compare one to one RNNs vs Transformers that easy. Those are completly different architectures and it does not make sense to understand each architecture based on the same hyperparemeter. We must split the analysis into two categories: Inter-autoregressive intervention, which means means between two autoregressive models from diferent nature, and intra-autoregressive intervention, which meand means within or inside one autoregressive model from the same nature.

### Intra-model intervention
To estimate causal effects from the interventional experiments, we must identify a set of confounding variables that we must control to observe causal effects. However, there is an intrinsic problem in the hyperparemeters defined in RNN architectures from Transfomer architectures. Hyperparemeters with the same name in both architecures do not imply that have precisely the same meaning in both autoregressive architectures. 

For instance, the *seq_len* of an RNN has not the same definition as the *seq_len* of a Transformer. In the first place, the context window in a RNN might negatively impact the prediction if they are very long. Nonetheless, in a Transformer, the context windows do not have a relevant impact in the effiency. In the second place, it does not make sense to compare RNNs to Transformers because both of them have different mathematical constructions. The real question here: Is there any valid reason to compare RNNs and Transformers for interpretability purposes? We can derive causality conclusions by intervining hyperparameter within the same architecture. But we cannot interviene the same hyperparemeter for both architectures to derive any causal effect since the hyperparameter for the RNNs are not the same for the Transformers. 

Nevertheless, we can do compare RNNs among RNNs or Transformers among Transformers because they share same properties within the same category. 

We can intervene the models independely. That is, the counterfactual analysis would be around one model and the influence of their well defined hyperparameters. 

### Inter-model intervention
To estimate causal effects from distinct architectures we need to find variables that are truly comparable among models of distinct nature. Accuracy might me a nice candidate, but unfurtunatly, accuracy is consequence of the intervention, it is not a variable we want to control for. 

If we think about carefully, we can scale each autoregressive model and group them by the number of trainable parameters. Something like the "complexity" of the model. However, this type of comparison is based on size and 1) it might not have a real impact on the study of the performance or interpretability and 2) it's very difficult to set an exact numner of trainable parameters for each model. One possible solution is group the setting value within an interval thought. We could establish three ranges of complexities such as low, medium, and high. Then, we can draw conclusion from a joint intervention on the complexity size.

### Data intervention
>TODO data intervention must be clearly define here. 
Another candidate parameter to interviene is the data themselves. But we should bear in mind that data usually help to define the architecture. In our case, data are pushing us to in fact use autoregressive models and influence the design decision of the architecure. Therefore, if we interviene on the data, we must interviene on the design of the architecure. And we have already said that interviening in the design of the architecture is not possible for intra-model intervention since hyperparameters of one architecture do not have the same meaning or are comparable to the hyperparameters of the other one.

This previous statement is not the same as modifying (or mutating) within the same nature to observe downstream behavior on the architecture. Data modifications (or mutations) are independet from the hyperparameters definitions or design since all modifications are based on sequence intervention (all our data are sequence-based). In fact, if we want to mutate data is because we are interested in how these data affects the training under some well -defined and cotrolled hyperparameters. In conclusion, data intervention allow us to prove generalizability or how good the model is learning hidden features. Now, the question would be: Are the data an inter-model or intra-model intervention? Well, if data influences the model; then, data can be used to analyze both scenarios.  if the data preservers their sequence-based nature, we can indeed compare two autoregressive architecures from distinc tensor organization. 


