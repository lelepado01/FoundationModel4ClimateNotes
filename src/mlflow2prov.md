
# MLFlow2PROV

> [Paper](https://dl.acm.org/doi/pdf/10.1145/3595360.3595859) | [Code](https://github.com/mariusschlegel/mlflow2prov/)

## Introduction

MLFlow allows to simplify the structured collection of artifacts and metadata from ML training. One of its problems is taht is suffers from limited provenance collection capabilities. 

MLFlow2PROV is a tool that allows to collect provenance from MLFlow and store it in a PROV-JSON file. Its creates a W3C compliant model which captures ML experiments and and activities from MLflow or other processes. It extracts the provenance metadata grapth from the model, enabling querying, analysis and processing of the information. 

It introduces a PROV compliant provenance model (git + MLflow), extracting given a version control repository the provenance of the code and the data. 
The goal is to capture git related activities (and workflows) and MLflow related activities (and workflows) and to store them in a PROV-JSON file.

## PROV recap

- Agent: An entity that bears some form of responsibility for an activity taking place, for the existence of an entity, or for another agent's activity.

- Entity: A physical, digital, conceptual, or other kind of thing with some fixed aspects; entities may be real or imaginary. 

An entity can *beAttributedTo* an agent, *wasDerivedFrom* another entity, *wasGeneratedBy* an activity, *wasInfluencedBy* another entity, and *wasInformedBy* another activity. 

- Activity: Something that occurs over a period of time and acts upon or with entities; it may include consuming, processing, transforming, modifying, relocating, using, or generating entities.

An activity can *wasAssociatedWith* an agent, *used* an entity, *wasInformedBy* another activity, and *wasStartedBy* and *wasEndedBy* an entity.

## MLFlow2PROV Actions

- **extract**: from the resources of an MLflow experiment, it extracts the provenance metadata graph and stores it in a PROV-JSON file.
- **load**: file containing a provenance graph
- **save**: file containing a provenance graph
- **merge**: multiple provenance graphs into a common graph
- **transform**: can merge duplicate agents, eliminate duplicate entities, replace user-related info, and so on...
- **statistics**: print stats for the provenance graph

Process steps:

- input data through for example a yaml file. 
- extract provenance VCS repo (git) --> intermediate representation
- extract provenance MLflow and artifacts --> intermediate representation
- provenance graphs generation and processing
- output: provenance graph in PROV-JSON format or document