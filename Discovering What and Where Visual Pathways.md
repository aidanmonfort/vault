---
created: 2025-03-06T09:36
updated: 2025-03-13T09:07
tags:
  - "#ml/papers"
---
---
[Link](https://openaccess.thecvf.com/content/CVPR2024/papers/Zhang_Deciphering_What_and_Where_Visual_Pathways_from_Spectral_Clustering_of_CVPR_2024_paper.pdf)
[Code](https://github.com/xiao7199/layer_distributed_spectral_clustering/blob/main/main_cls.py)

Background Papers/Info:
- [[Eigen Theory]] 
- [[Unsupervised Learning]]
- [[Attention]]
---

Summary: 
![[Screenshot 2026-03-03 at 1.43.10 PM.png]]


This paper essentially aims to extract information from feature representations of networks at different levels of the model. It uses spectral clustering, and the novel idea is using the different feature levels to build the affinity matrix out of attention matrices.  

Two forms of affinity matrix:

$$
\begin{align*}
\mathcal{A}_{\text{what}} &= \{ A_{1}^{VV}, A_{2}^{VV}, \dots, A_{m}^{VV}\} \\
\mathcal{A}_{\text{where}} &= \{ A_{1}^{QK}, A_{2}^{QK}, \dots, A_{m}^{QK}\}
\end{align*}
$$

They formulate the clustering problem as a graph partitioning problem on these two formulations of affinity matrices. The goal is to solve the [[optimization]] problem:

$$
\max_{X} \underset{A \in \mathcal{A}}{\mathbb{E}} [g(X)^T D_A^{-1}Ag(X)]
$$
$X$ is essentially the eigenvectors of a lower dimensional representation of the affinity matrix. $g(\cdot)$ is a resampling function to make $X$ the same spatial resolution as $A$. $X^TX = I$ is set as a soft constraint to the problem using a Frobenius Regularization term. 

