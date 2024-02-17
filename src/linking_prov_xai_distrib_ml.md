# Linking PROV and XAI in distributed ML

> [Paper](https://ieeexplore.ieee.org/abstract/document/8885193)

## Introduction

The process to register data provenance to guarantee explainability needs to also encompass all pre-processing steps and analyis in the pipeline (not just the ML part). This highlights the need for an end-to-end pipeline for XAI. 
This also has to take into account data lineage and *how* and *why* it got to the present place. 

## Challenges

To track reproducibility: 
- Note the hyperparameters;
- Fix the random interactions and numbers; 
- Save all configurations.

Several challenges still persist: 
- Make all steps reproducible: which involves making all provenance information available as well as all data processing steps. This involves an active partecipation from both database and ML communities. 
- Provenance granularity: coarse granularity is a simple high level description of basic data preparation. Fine-grained granularity implies on the other hand to track all information at each individual record. In many cases, tuple level granularity is enough (adaptable to the ML task at hand, not all projects require the same explainability level). 
- Data volume: the solution has to be scalable and we need to store information about which process and node did what. For this, a specialized data format can be used (ex. HDF5). 
- Biases and Fairness: biases are accentuated in a distributed environment, where we optimize for speed. 
- Data freshness: we should track the time of creation and modification of the ML system and data relative to it. 
- Variability and lack of standards: it is not clear which provenance information is needed for an arbitrary ML system. Different communitied need to agree on standards, so APIs for multiple backends, distributed query engines, and data integration systems. 
- Data protection and privacy: problem with storing and utilization of sensitive data. Once anonymized, it loses a lot of quality. We need provacy compliant trade-offs, to also provide provenance and XAI. K-anonimity and separation of duties must be expanded appropriately. 

> IS THERE A WAY TO UNDERSTAND AUTOMATICALLY THE GRANULARITY NEEDED?

## Related Stuff

- Provenance for decisionmaking: track data flow to enable identification of entities responsible for actions and decisions (accountability). 
- Provenance in a distributed setting: RAMP framework (for map-reduced operator), already implemented in Apache spark. 
- Bias: problems related to data (duh), no real solution but mitigation and XAI.  


