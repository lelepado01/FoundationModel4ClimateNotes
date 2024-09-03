
# Establishing Data Provenance for Responsible Artificial Intelligence Systems

> [Paper](https://dl.acm.org/doi/10.1145/3503488)

We first review biases stemming from the data’s origins and pre-processing. We then discuss the current state of practice, the challenges it presents, and corresponding recommendations to address them.
highlighting how our recommendations can help establish data provenance

How does data provenance affect the four interrelated characteristics of responsible AI: fairness, accountability, transparency, and explainability?

### SOURCES OF DATA BIASES
- Biases from the Data’s Origins
    - Population data: developers often rely on access to unique data
    - Measurement error: the uncertainty of the input variables resulting either from the measurement itself or from pre-processing is often neglected (the precision of an AI-based system might be overestimated)
    - Data quality chasm: lack of data with adequate quality in settings where the AI system is used
    - Data repurposing: data collection practices also introduce misuse and biases (repurposing data is the norm in AI-based systems)
    - Data augmentation: can amplify existing biases within the dataset and mask the inadequacies of the collected data
- Biases from Data Pre-Processing
    - Dataset shifts: non-stationary nature of the environment and the population from which all the input data of AI-based systems are generated
    - Opaque pre-processing: in algorithms with intrinsic obscurity, such as deep neural networks, understanding the specific patterns being learned is difficult
    - Data labeling: identification and development of labels are often not transparent
    - Adversarial manipulation: small changes in the data input can lead to significant differences in the output (susceptible to adversarial manipulation)
    - Transfer learning: use the algorithm to solve similar problems


### RECOMMENDATIONS FOR IMPLEMENTING DATA PROVENANCE
- Establishing Organizational Data Governance
    - Managing meta-data: detailed information about the data captured in a data source (cataloging data and curating data)
    - Conducting data audits: assessing whether the data are fit for a specific purpose
- Demanding Data Traceability
    - Guiding data acquisition: Manual labeling regulation
    - Benefitting from blockchain technology: potential to upgrade the value of the data and provide more efficient and transparent results
- Leveraging Technological Advances for Data Provenance
    - Deriving explanations: XAI methods, such as LIME, LORE
    - Managing noisy data: attributed noise from features or class noise from labels/targets
    - Identifying inherent data structures: clearer understanding of the system’s behavior and the data helps judge the fair- ness of recommendations