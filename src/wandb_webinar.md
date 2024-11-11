# Weights and Biases Webinar

- Sweep Feature: log hyperparameters optimization (e.g., learning rate, batch size, etc.)
- Frozen run: interrupt and continue training  (freeze configuration values)
- If GIT: check if a change is unstaged and take note in a diff file. Also check modifications in a notebook, if one is being used.
- Differences tables to check differences between runs (this is done in the explorer a posteriori)
- Tracking of system metrics both at process and system level (tracked every 20 seconds, so running averageis visualized)
- Lineage Tab: track different versions of the pipeline. Create / Consume artifacts (ex. create artifact of dataset for train / test split)
- Artifacts tab: log any file with run checksum (optmized for large files, so you don't have to store multiple copies of the same file)
- Register model to link to similar versions
