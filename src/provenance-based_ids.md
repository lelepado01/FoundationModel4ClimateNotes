# Provenance based IDs

Not yet mature. Robustness against dedicated adversaries is not yet proven. 

It offers: 
- Runtime behaviour training
- Finetune ML systemon prov files
- Unified event format

Adversarial validation is necessary to prove robustness. Problem space is critical, requires knowledge of the system (domain knowledge). 

Data guided attach search through ProvNinja.
- Identifies conspicuous events (data + attack graph)
- Replace with common events (search for replacement with attack grapth and event summary)
- Camouflage process: summarize the expected behaviour (execution profile + expected behaviour). Mimic benign behaviour from an incouspicuous attack grapth (camouflaged). 
- Validate: feature space validation, problem space validation, implementation, integration, and deployment.

This method decreases detection rate of attacks by 57%. 
Supports adversarial testing and verification. 