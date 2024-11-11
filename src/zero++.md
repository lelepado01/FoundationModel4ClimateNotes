# Zero ++

Improvement on Zero redundancy optimizer. 

Cons: when on low bandwidth clusters, or with small batchsizes, the high communication overhead can be a bottleneck and lower the effectuve throughput. 

Communication volume reduction techniques:
- Block quantization for allgather: shrink down all model parameters to a single block, block based quantization (indipendent for each set of model parameters); 
- Data remapping that trades off more memory for less communication: hierarchical weights partitioning (maintain a copy of the model in each partition, but only update a subset of the weights in each partition);
- All to all quantized gradient averaging paradigms: new gradient communication paradigm that reduces communication volume. Gradient compression with block based INT4 quantization, but the precision is recovered before the reduction operator to preserve the accuracy of the final model.

4x reduction in comms volume, 2x better throughput.

Comms volume reduction: from 3M to 0.75M.