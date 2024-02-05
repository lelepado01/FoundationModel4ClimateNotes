# Advances, Challenges and Opportunities in Trustworthy AI

## Introduction

The design and sculpting process of data to develop AI often relies on manual work, and may critically affect the trustworthiness of the AI model.
Technical advances may help in creating a data-for-AI pipeline, which is more scalable and rigorous. 

Dataset creation is one of the major pain points in Ai, due to the cost ofo curation and annotation. Data scientists spend twice as much time on data loading, cleansing and visualization than on model building.

Also AI models tend to risk picking up biases and spurious correlations from the data, which can lead to unfair or unsafe decisions. 
More attention needs to be placed on developing methods and standards for improving data-for-AI pipelines. 

## Data Design

The data design process is critical for mitigating biases and ensuring generalizability and reliability of the model. 

Data has to be appropriate for the task, and have good coverage for representing different classes of users, while currently it is limited or offers biased coverage. 
Also, synthetic data can be used to shorten the gap and avoid performance drops. 

One other promising approach is to engage broader communities in the data design process, by having them partecipate in citizen-science data creation. 

Data-nutrition labels have also been used to capture metadata about the data design and annotation processes. 

## Data Sculpting

Once the initial dataset is collected, a substantial amount of work is needed to sculpt or refine the data to make it suitable for AI. 

Data valuation is used to measure changes in AI model's behaviour when different data are removed from the training process. These changes can be measured using metrics such as Shapely scores or influence approximation. 

A similar approach is to leverage the prediction uncertainty to detect poor quality data points. 
Over 3% of all test samples in benchmark datasets such as ImageNet are misannotated. 

An alternative is to sistematically clean dirty data to improve the quality of the AI model. These methods include ActiveClean, which identifies the subset of dirty data that are critical for the model. 

Data annotation is a major bottleneck and a source of error. Currently it often relies on manual labelling, which can be expensive and error-prone. 
Also some annotations may require domain expertise, which is not always available. 

One approach is data programming, where data is labelled with a set of rules. Another is active learning, where the most descriptive samples are prioritized for annotation (most informative points). 
Also other approaches for visual data use eye-tracking, to understand the most informative parts of the image, where the expert focuses on.

When data is limited, augmentation can be used to generate new samples and improve reliability. Techniques such as mixup create new samples by interpolating between existing ones.

## Data to evaluate AI

The goal of AI evaluation is to assess its generalization ability, robustness and trustworthyness. 
The evaluation data should be carefully designed to capture the real world setting where the model may be used, while being different from the training data.
Also, annotations should be labelled by an expert different from the one who labelled the training data. 
This data has to make sure that the model is not using spurious correlations to shortcut the task and not generalize well. 

Systematic data ablation is a good approach for checking for potential shortcuts, the model is tested on ablated input data, and the performance is compared to the original data. 

Class-specific evaluation is also important, as it can reveal biases in the model. Multi-accuracy auditing is a technique to find data subgroups where the model performs poorly. 

When metadata is not available, methods such as Domino allow to identify clusters of evaluation data where the model is mistake prone, and create a a natural language explanation of these model errors. 

## Data regulation and policies

Developers must conduct conformity assessments on AI products. Some data regulatory requirements may impede the development of trustworthy AI. Privacy concerns can impede the curation of representative data with access to sensitive attributes.

Privacy can itself become a bias, as companies can hoard expensive datasets and leave smaller institutions and academia to scrape the internet for lower quality and potentially biased data. 

Data erasure can also be a challenge, as large AI models memorize user information and selectively eraseing it can be difficult without leaving knowledge gaps in the model.