# Evaluation of pre‐training large language models on leadership‐class supercomputers

> [Paper](https://link.springer.com/article/10.1007/s11227-023-05479-7)


## Introduction

The training of large language models (LLMs) is compute intensive and requires large amounts of data.

## Scaling Laws of Transformers

The loss of LLMs scales with both the training data and model parameters. Consequently, it scales with the amount of computation.

The total number of floating point operations (FLOPs) is approximately, 

\\( T_{FLOPS} ∼ 6 \times P \times D\\)

where P and D are number of model parameters and tokens, respectively. 

compared to the attention and other blocks, the feed forward block typically requires the most computation. 
For each element of a feed-forward weight matrix, there are a total of 6 FLOPs per input token. 
the computation hence scales quadratically with the model size.

For example, training a 175B parameter GPT3 model requires \\(3.7×10^{24}\\) FLOPs, and it quickly grows to \\(1.2×10^{26}\\) FLOPs for a 1T parameter GPT-style model.

## Runtime and energy projection

the runtime can be straightforwardly predicted via

\\( t = T_{FLOPs}∕R_{FLOPs} \\)
\\( ∼ 120 \times P^2∕R_{FLOPs}, \\)

where \\(T_{FLOPs}\\) and \\(R_{FLOPs}\\) are the compute operations in FLOPs and training performance in FLOPS

![Eval](./imgs/eval_llms_com_1.png)


The energy consumption can be evaluated by: 

\\(E = t \times R_{𝚆𝚊𝚝𝚝}\\)

where \\(R_{𝚆𝚊𝚝𝚝}\\) is the averaged power measured from few iterations.

For Summit and Crusher: the peak performance in half precision for the V100 (112 TFLOPS) and MI250X (384 TFLOPS) GPUs and linear scaling up to full system


## Results

The training performance for FSDP and DeepSpeed-Megatron is 62.1 and 65.1 TFLOPS, respectively. From this baseline, the performance drops 20% and 44% for DeepSpeed-Megatron when using tensor parallelism within a NUMA domain and a node on Summit, respectively. The impact for FSDP is less (30% within a node compared to 44% for DeepSpeed-Megatron) due to less frequent communication and a smaller total message size. 

#### Scaling analysis

We scale up the LLMs training on both Summit and Crusher: 

![Eval](./imgs/eval_llms_com_2.png)

The scaling efficiency is about 97%, signaling Frontier can be a promising platform for training LLMs of these model sizes

#### Energy consumption

To estimate the energy usage, we trace the GPU power in watts during the training for FSDP training of GPT 175B model on Summit and Crusher. 
One batch step takes 359 and 301 s, correspondingly. 

The averaged power usage is about 85 and 408 Watts, for Summit and Crusher, respectively, and the corresponding computational efficiency is 0.165 and 0.235 TFLOPS/Watt.

As Crusher system bears the same architecture as the first Exascale system Frontier and their unprecedented mix-precision capability, we believe they are well-suited as the platform for training LLMs at extreme scale.

``` admonish important
One caveat to consider in our estimation is that the analysis is based on the current implementations of GPT-NeoX (DeepSpeed-Megatron) and PyTorch (FSDP). It’s important to note that the field is rapidly evolving, with ongoing advancements that can further reduce communication costs.
```

## Conclusion

For theoretical peak and achievable performance, the minimum per-device communication bandwidth needed is 37 and 94 GB/s, respectively.
The current 25 GB/s per-device on Crusher is not sufficient to support linear scaling for training GPT 1T model. 

We ignore I/O requirement in our analysis because it can be straightforwardly hidden among computations given the typical global batch size of millions of tokens. 

## Ideas

- Graph with Computation need (FLOPs) and ideal training time (days) assuming peak performance and perfect scaling for optimal training of LLMs on Summit and Frontier, respectively. This assumes perfect scaling --> can we do it with estimated scaling from Frontier?

- Compare real benchmarks with projections from Yin paper
