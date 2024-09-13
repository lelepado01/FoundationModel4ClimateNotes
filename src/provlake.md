# ProvLake

> [Paper](https://arxiv.org/abs/2010.00330) | [Code](https://github.com/IBM/multi-data-lineage-capture-py)

### Introduction

Contributions: 
- Characterization of the lifecycle and taxonomy of data lineage
- Design decisions to build tools 
- Lessons learnt after evaluating on ML application

Captures the entire lifecycle of ML tools, various phases: 
- Data curation
- Learning data preparation
- Training
- Evaluation

The paper addresses the challenge of high eterogeneity of different contexts, tools, and data sources.
Need to track / assess / understand / explain data, models, and transformation processes. 

Creates a comprehensive characterization of the lifecycle of data lineage, and a taxonomy of data lineage (prov to support the lifecycle). 
Data design to query the provenance data. Creation of Prov-ML (new prov standard) and expansion. 

Also set of experiments to showcase ProvML. 

### Lifecycle of ML Data Lineage

Actors: 
- Domain scientists: data curation
- ML engineers: ML model design 

(it's a slider, not a binary)

Process includes:
- Raw data
- Data curation
- Domain data
- Learning data preparation
- Learning data
- Training
- Evaluation
- Final model

Provenance data is captured at each stage.
- Domain specific: curation, data and metadata
- Machine learning: data preparation, training, evaluation
- Execution: runtime provenance (info about environment, nodes, etc.)

Types of analysis: 
- Online analysis: monitor / debug / inspect in real time
- Offline analysis: post-mortem analysis

### Provenance in ML Lifecycle

- Data integration with context aware Knowlwedge Graphs
- Multiple workflows on data lakes
- Keep prospections and retrospective analysis
- Design a conceptual data scheme to capture provenance data
- Easy data linkage and query