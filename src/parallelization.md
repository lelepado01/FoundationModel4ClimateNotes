# Parallelization

## Techniques for pytorch
 - DDP: the model is copied on all processes, the dataset is split on all the workers and each model is fed a different batch gradient communication is used to keep the models in sync (also overlap of gradient computation)
 - RPC: used if training paradigm can’t fit using DDP
 - Collective Comms: foundation for RPC and DDP, low level APIs

## Paradigms
 - Model Parallelism: each worker focuses on a portion of the model, best for large models.
 - Data Parallelism: split train set on each worker, shared weights (DDP)
 - Parameter server architecture: central node with parameters, workers update the weights by computing the gradient 
 - All-Reduce Comms: several workers compute private gradient, then combine with all-reduce operation to share global gradient.
 - Gradient accumulation: compute gradient on several minibatches, used if comms overhead is high.

## Distributed deep learning

Distributed training is the process of subdividing the training workload of, for example, a large neural
network across multiple processors. These processors are often referred to as workers, and they are
tasked to compute in parallel to speed up the training process. There are two approaches to parallelism:
data and model. In data parallelism, the full training set is divided between all the workers, where a
copy of the model is also kept. Training is done either synchronously, where all the workers wait for
each other, synchronize the gradients, and only then perform the backward step; or asynchronously,
where a selected worker is tasked with keeping an updated version of the weights, and all the others
can read and write from this worker, often called a ”parameter server”. Using the latter procedure
means that all resources are used at the same time, without any delay. However, it also means that
only one worker at a time is training with the latest version of the weights. In large clusters the
centralized nature of this approach can also create bottlenecks. Model parallelism, on the other hand,
divides the model either horizontally, i.e. node-wise, or vertically, i.e. layer-wise, between several
workers who are allowed to run at the same time. This approach also reduces the footprint of the
model in each worker, making it lighter on the GPU’s memory.


### DDP

Distributed Data Parallel is a method of data parallelism that enables a program to operate on
numerous machines simultaneously. Applications utilizing DDP generate numerous processes and
initialize one DDP instance for each process. 

### FSDP

In some cases, it may not be possible to create a duplicate of the model for every process. In
these instances, Fully Sharded Data Parallel may be utilized, where the optimiser states, gradients,
and parameters of the model are subdivided across all DDP ranks. In this case, the neural network is
divided into smaller sub-models, each of which represents a portion of the parameters of the overall
model. This approach allows different parts of the model to be processed simultaneously by different
processing units, and can be used in conjunction with a data-parallel approach that splits the training
set to achieve even faster processing times. This results in a program that has less impact on GPU
memory, thus reducing execution times.

### DeepSpeed

DeepSpeed is a deep learning optimisation suite that enables efficient scalability and faster
execution times for both training and inference of large machine learning models. It was developed
by Microsoft and claims to offer a 15x speedup over other state-of-the-art parallelization techniques.
It provides memory efficient data parallelism and enables training without model parallelism through
a novel solution called Zero Redundancy Optimizer. Unlike basic data parallelism, where memory
states are replicated across data-parallel processes, ZeRO partitions model states and gradients to save
significant memory. Several other memory optimisation techniques are also used, such as Constant
Buffer Optimisation, which combines all communication-based operations into a single operand, and
Contiguous Memory Optimisation, which reduces fragmentation during training.