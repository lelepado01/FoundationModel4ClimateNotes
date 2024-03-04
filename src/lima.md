# LIMA: Fine-grained Lineage Tracing and Reuse in Machine Learning Systems

> [Paper](https://dl.acm.org/doi/abs/10.1145/3448016.3452788) | No code?

## Introduction

Data scientists pose hypotheses, design experiments, and analyze results to build machine learning models. This requires building ML pipelines for data cleaning, feature engineering, model selection, and hyperparameter tuning. This causes high computational redundancy which has been adressed in a coarse way. 

LIMA offers a fine-grained lineage tracing and reuse system for ML pipelines with low overhead. It captures the lineage of data and models at the level of individual data samples and model parameters. It shows performance improvements of up to 12%. 

###### Data Provenance in ML Systems: 
captures information about the origin, processing, and usage of data. Similarly, lineage has been used for low-overhead fault tolerance in data parallel frameworks.

###### Non-Determinism: 
same runs with the same input do not yield the same result. When computing lineage of high level primitives, seed parameters need to be kept into consideration to maintain reproducibility. This non-determininsm limits the use of coarse-grained lineage systems. 

## LIMA

Uses fine-grained lineage tracing and reuse inside ML systems. A lineage DAG is maintained, where nodes represent the executed operations (including parameters that make them deterministic) and edges are data dependencies. 
The DAG is recursively built while executing the conditional control flow and operations. 

## Redundancy

Types of redundancy in fine-grained lineage systems:
- Full function or block redundancy: potential for full reuse of the outputs of a function or block. 
- Full operation redundancy: last level operations can be reused for equivalent inputs, given that all non-determinism is exposed to these operations and cast to a basic input as well. 
- Partial operation redundancy: operation inputs with oberlappin rows or columns further allow reuse by extraction from (or augmentation of) previously computed results.

These types of redundancy motivate the design with: 
- fine-grained lineage tracing and reuse
- multi-level lineage reuse
- exploitation of both full and partial reuse

## Lineage Tracing

we introduce the idea of lineage deduplication for loops and functions. 

LIMA maintains in a thread lineage DAGs for all live variables of this execution context

A lineage DAG L is a directed, acyclic graph, whose nodes (or lineage items) represent operations and their outputs, and whose edges represent data dependencies. Lineage items consist of an ID, an opcode, and more. Leaf nodes are literals or matrix creation operations (e.g., read or rand), and multiple inner nodes might refer to the same inputs. Thus, the lineage DAG is a data flow graph. 

###### Lineage Tracing: 
The immutable lineage DAG for live variables is then incrementally built by lineage tracing as we execute runtime instructions. 

###### Comparisons: 
When working with multiple, potentially overlapping lineage DAGs, a key operation is the comparison of two lineage DAGs for equivalence or containment. 

###### Lineage Deduplication: 
the problem with fine-grained lineage tracing is that it can lead to very large lineage DAGs. This is due to the repetition of execution paths in loops and functions. This approach uses deduplication as a form of compression, by extracting lineage sub-graphs and storing them only once (as a single lineage item). 

- Loop Deduplication setup and tracing: analyze the control flow to aid deduplication. Trace a temporary lineage DAG for each iteration of the loop. Keep a bitvector containing the taken paths. 
- Function Deduplication: same process, but for functions without loops or other function calls; 
- Handling non-determinism: model the seeds as input placeholders of the lineage path. Trace the seeds and add them as input to the deduplicated lineage DAG.  

Also supports task parallel loops.

## Experiments

Testing run on 
- Autoencoder
- PCA and Cross Validation
- PCA and Naive Bayes

SystemDS with LIMA shows competitive results, even when keeping into account the different level of granulaity of the lineage DAGs this approach is able to capture.