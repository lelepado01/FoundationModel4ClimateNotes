# Experimental Transformer

> [Paper](https://arxiv.org/abs/2310.19961) | [Code](https://github.com/tung-nd/ExPT.git)

ExPT is a transformer architecture that uses unsupervised learning and in-context pretraining (few-shot training in Transformers). 

- **Pretraining**: unlabeled designs from context X (without score). Using synthetic data, so functions that operate on the same domain as the objective function. 
- **Fine-tuning** (Adaptation): the model conditions using a small amount of pairs <design, score>

How do we generate the functions? -> there are several ways (ex. Gaussian Mixtures, Gaussian Processes, etc.)
In this case Gaussian Processes are used with RBF kernels.

## Model

Encoder model is used for pairs \\(<\texttt{design}, \texttt{score}>\\), in conjunction with y_m, to create an hidden vector h. Token embedding is done with two linear layers, one for the pairs and one for the score. 

How do we model conditional probability? -> we use a **Variational Auto-Encoder** to model the conditional probability \\( p_{\theta}(x_i | h_i) \\).