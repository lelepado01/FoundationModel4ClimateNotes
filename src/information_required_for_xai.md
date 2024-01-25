# Information Required for XAI

> [Paper](https://ieeexplore.ieee.org/abstract/document/9319010)

## Summary

Introduction of a 6-w framework to create a graph based system to provide user with information about training and data used by the ML model. 

Open Issues: 
- Requirements for XAI decision support systems --> What info does the user need to make a decision?
- Can the user check all steps for an answer from the model?
- Security evidence of an AI system? Are there biases (even deliberate)? Safety Mismatches, Misrepresentations?

Informtion required for XAI:
- Human point of view --> ML systems are not transparent even for experts or designers
- Security point of view --> generated explanations can be misleading (deliberate manipulation of the results)

Provenance information: PROV-DM model, keeps history of data records, provenance linking of Input and Output of an AI system.

6W framework for provenance graph XAI design: 
- **Who**: user, developer, data generation, modification and explanation
- **Where / When**: process, system and design
- **Why**: Governance, policies and laws
- **What**: Data, documents, decision, system information
- **Which**: security, safety information and protocol 

TODO: WRAPPER AROUND AI MODEL CONTAINING INFO ABOUT TRAINING PROCESS, DATASET USED (STD, MEAN, VARIABLES --> IF INFO ABOUT DS ARE NOT MATCHING THEN PROBLEM?). HASH FUNCTION TO DETERMINE IF THE PROCESS OR RESULTS HAVE BEEN MANIPULATED. 
TODO: PROVIDE PREVIOUS RECORDS OF SIMIL. INPUT AND GT (THIS REQUIRES THE FULL DATASET), OTHERWISE JUST VARY THE INPUT SLIGHTLY TO SEE CERTAINTY AND POSSIBLE PIVOTAL FEATURES