# Oak Ridge base FM for Earth System Predictability

113B parameters with hybrid tensor data orthogonal parallelism technique (Hybrid STOP)

Uses unique math property of matrix chain multiplpication distributes model parameters in alternating row/columns shards. 
It combines tensor parallelism + FSDP. Better scalablity, avoids peak memory usage, keeps parameters shared through memory

y = xAB

It gathers partially and not globally, which makes the process faster on memory.

Uses 684 PetaFLOPS to 1.6 ExaFLOPS throughput across 49152 GPUs. 

91 climate variables from 10 CMIP datasets, 1.2M data points. 

Optimizations: 
- Architecture optimization: problematic convergence with large attention logits (adds layer normalization before the self attention)
- Hierarchical parallelism: add also DDP on top of H-STOP (this speeds up training)
- Activation checkpoints: trade compute for memory savings in LLMs
- Mixed Precision: use bfloat16 to make large computations easier
- Layer wrapping: iterative FSDP sharding and prefetch

