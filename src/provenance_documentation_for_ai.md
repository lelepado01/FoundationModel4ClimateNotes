# Provenance Documentation for Trustworthy AI

> [Paper](https://direct.mit.edu/dint/article/5/1/139/109494/Provenance-documentation-to-enable-explainable-and)

## Summary

AI models should be transparent, explainable and trustworthy (TAI), using provenance to explain complex models. 
Provenance answers questions who-what-where to obtain reproducibility, trustworthiness and explainability. The idea is to be able to understand the metadata and the provenance of ML artifacts. (FATE in AI --> there is no roadmap yet)

Trustwothy AI: AI-based system that are lawful, ethical and robust in the face of adversarial attacks. This is to estabilsh XAI (Explainability). Some examples are DARPA XAI program, HLEG EU program (guidelines on AI). 

Post-Hoc Explainable techniques: 
 - Model specific: TSHAP, DeepLIFT, Grad-CAM
 - Model agnostic: LIME and SHAP

Provenance documentation is still necessary to complement XAI, increasing transparency with: 
- How data is collected
- Data ownership and rights
- Trace steps in data analysis

Tools for provenance documentation:
- W3C PROV anthology
- W3C PROV Data model (PROV-DM): web anthology language (PROVN) OWL2

Tools for validation and browsing of provenance documents: 
- PROV validator, Prov Viewer
- Common workflow language (CWL) also for ML
- PROV-JSON, OpenML, Model-DB
- prov-py allows to export provenance information from Python scripts
- Jupyter to automatically generate provenance information with packages and reproducibility