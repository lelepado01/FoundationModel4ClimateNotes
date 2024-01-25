
# Trustworthy AI

Sources: 

> []()

## Introduction

This list provides essential requirements for designing trustworthy AI systems. 

- **Human agency and oversight**: AI systems should complement and empower humans without replacing them
- **Technical robustness and safety**: AI systems should be technically robust and perform as expected by the users
- **Privacy and data governance**: AI systems should protect user data and govern its usage at every step of its lifecycle.
- **Transparency**: The transparency of an AI system refers to the need to explain, interpret, and reproduce its decisions
- **Diversity, non-discrimination, and fairness**: AI systems should treat all sections of society fairly without discriminating based on factors such as socio-economic determinants
- **Societal and environmental well-being**: AI systems should not cause any harm to society or the environment during their design, development, and use
- **Accountability**: AI systems should be able to justify their decisions

## TRUSTWORTHY AI REQUIREMENTS

#### Fairness

Pre-processing models: 
- Bias mitigation method for word embedding, which approximates the effect of removing a small sample of training data based on the bias of the resulting system. This system is helpful to trace the origin of the bias in the dataset
- T-closeness technique for discrimination prevention. This technique is helpful to clean data of historical decisions before using it and provides a formal guarantee about the level of discrimination present in the dataset.

In-processing models: 
- Fair classifiers using decision boundaries, ensuring fairness concerning one or more sensitive attributes.
- Regression algorithms fair by applying and weighting a regularizer to the standard loss function. This method provides both individual and group fairness and can calculate a numerical value for the effect of fairness on accuracy. 
- Bias mitigation method using adversarial learning, which uses the concept of maximizing predictor accuracy while minimizing the ability to predict protected attributes. This method is helpful for both classification and regression tasks

Post-processing models: 
- Removes bias by adjusting the learned predictor to balance among supervised learning methods. This method mitigates bias while preserving the privacy of the system.
- Different classifiers for different groups to mitigate bias. This approach is beneficial if all of the groups are not represented equally in the data.

Bias detection methods: 
- Test generation mechanism to detect bias in the system. It detects all combinations of protected and non-protected attributes that can lead to discrimination through directed and undirected search.
- Fairness testing approach known as the Flip Test, which tests fairness at the individual level to detect statistical and casual discrimination.

#### Explainability

Pre-modeling approaches: 
- Explaining the datasets on which the system is trained. Researchers proposed visualization techniques to better understand the data before using it.
- Achieve explainable data is through data standardization. Data labeling, in which data is labeled based on its quantitative and qualitative properties
- Creating a data sheet consisting of all information related to the data collection process, dataset features, and recommended use.

In-modeling approaches: 
- Utilize the graph structure of trees where internal nodes represent tests on features and leaf nodes represent class labels. Different paths from the root to leaf nodes represent different interpretable classification rules
- Linear models to provide interpretability by visualizing the weight and sign of the features for a given output. This means that if the weight is high and the sign is positive, it will increase the output of the model.

Post-modeling approaches: building proxy models on top of black-box/complex models
- Feature importance explainability approaches: provide explainability by assigning feature importance values to the input variables. These values reflect which features played more critical role in the decision-making process. 
    - LIME (Local Interpretable Model-agnostic Explanations), which provides local interpretability to different classifiers and regressors by highlighting essential features that led to the decision.
    - LRP (Layerwise Relevance Propagation) for image classification algorithms, which includes interpretability by computing every pixel’s contribution to the prediction made by the classifier. This method utilizes heat maps to visualize the pixel importance.
    - SHAP (SHapely Additive exPlanations) method provides interpretability by assigning feature scores to each attribute for different predictions.

- Example-based explainability approaches: provide explanations and interpretability by creating proxy examples of the model and are based on selecting some instances from the input dataset and monitoring their corresponding outputs to explain the system. 
    - MMD-critic, which uses both prototype building and criticism selection to provide human-level interpretability. This method claims that prototypes are not enough to give interpretability to complex black boxes.
    - Providing counterfactual explanations that describe only the most essential variable that led to a decision and how a slight change in that variable can lead to a completely different outcome.

- Rule-based explainability approaches: rule-extraction techniques to give comprehensibility to artificial neural networks. These techniques provide a comprehensive description of the knowledge learned in the training phase using the system’s input and output
    - TCAV (Testing with Concept Activation Vectors), which uses the internal state of neural networks to provide interpretability

- Visualization-based explainability approaches: offer explainability by visualizing the internal working of opaque AI systems
    - Visualizing how the change in the feature importance affects the model performance.
    - Visualizing the contribution of the evidence for the final decision to provide explainability to classifiers

#### Accountability

Algorithmic accountability includes assessing the algorithms based on various parameters and assigning responsibilities of harm to different stakeholders involved in developing the algorithms.

Ex-Ante methods: before the actual development of the algorithms and mainly deal with the algorithms’ planning and design phase, which helps assign responsibilities for the decisions made by the algorithm even before its actual development. 
- Assign different priorities to different algorithm values through discussion between various stakeholders and the public council. This method will help algorithms resolve conflicting issues through prioritization, which prevents harm and will lead to better governance and accountability. The one drawback of this type of method is that it is difficult for people with different interests to agree on a single design. 
- Laying out all the design specifications and clearly describing what the system is intended to do in different circumstances enforces better governance and accountability.
- Time frame mechanism in the design process that prevents harm by timely reevaluating the system to ensure it is working as per the prior specifications and guidelines. This timely checking of the system will help governance and increase the user’s trust in the system.

In-Ante methods: implementing accountability measures in the development lifecycle of the AI system itself and ensure that AI systems are developed as specified in the planning and design phase
- Ensure that the data used for training is diverse and does not have any bias
- Guarantees that an appropriate model has been chosen based on the problem requirements
- Ensure that proper testing is done before deploying the system

Total transparency could lead to many adverse effects like loss of privacy, loss of trade secrets, and more attacks. There can be cases where total transparency can lead to less answerability. Because of these side effects, they proposed that total transparency for accountability should not be provided to the general public but only to the oversight agencies the public should trust

Post-Ante methods: providing accountability measures after the model is deployed.
- legal framework to ensure that the deployed model works within the specified boundaries
- ethical algorithm audit that can be used for external validation of the system, helping the deployed system to be free from biases and errors and safe to use
- algorithmic auditing technique to detect algorithmic bias in the system. They discussed how auditing techniques would help operationalized bias mitigation methods and lead to the development of fair algorithms

#### Privacy

Some researchers have proposed federated learning to provide privacy to the user data using the concept of collaborative learning where the raw data is not shared among the devices; instead, the model is shared after being trained on local devices. 

- Distributed learning method that uses data stored on mobile devices to compute a shared learning model, which prevents the need to centralize data storage providing data privacy as data is distributed over users’ mobile devices. 
- PEFL (Privacy Enhanced Federated Learning) approach, a non-interactive approach that can prevent data leaks when different entities interact.

