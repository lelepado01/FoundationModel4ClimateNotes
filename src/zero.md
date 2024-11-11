# ZERO

Eliminates memory redundancy (model state is the source of largest memory usage). 
- Data Parallelism: poor memory efficiency
- Memory Parallelism: poor compute efficiency and communication overhead

Zero DP: data parallel efficiency + efficient communication
- Optimizer state partitioning: 4x memory reduction
- Gradient partitioning: 8x memory reduction
- Parameter partitioning: memory reduction proportional to the number of partitions (DP degree) but 50% more communication volume

What is left is residual buffers / activations / gradients

Zero-R optimizes activations memory
- Identifies activations replications
- Defines optimized state for temporary storage / buffers
- Manages memory based on lifetimes to prevent memory fragmentation

Is ZERO + MP useful?
It can reduce memory footprint of very large models. 

