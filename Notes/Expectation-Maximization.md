---
created: 2026-03-09T17:15
updated: 2026-03-10T14:54
tags:
  - algorithms
  - ml
---
---

This is a technique used to maximize the likelihood of parameters when some states are hidden. 
In standard settings, if we are given a set of data with no unknown variables, and want to do something like find parameters $\mu, \Sigma$ for a gaussian such that we maximize the likelihood of these parameters, then we can do some pretty simple derivatives, and solve by setting to 0.

---
### Problem:
Assume we have some data matrix $X$ such that each $\mathbf{x}_{i} \in X$ has some hidden label and we want to assign parameters $\Theta_{i}$ such that we can describe the data as well as label each point. 

### Expectation Maximization(EM) Algorithm at a High Level
We can converge to a set of local parameters for each cluster and a label for each data sample that maximize the likelihood simultaneously. Let $w_{ij}$ be a soft assignment for sample $i$ to label $k$. 



> [!NOTE] EM
> 1. Randomly initialize all $\Theta$.
> 2. Until Convergence{
>
> 	1. Based on parameters $\Theta$, estimate all $w_{ij}$ using log-likelihood. 
> 	2. Based on soft labels $w_{ij}$, maximize the parameters for each cluster/label.
>
> }

---
### When does this not work?

### Reliance on initialization of $\Theta$
EM is very reliant on the initialization of the parameters. Since it converges to a local maximum, there is not a guarantee that this will give the global maximum. This can be mitigated through multiple random initializations. 

### Intractable expectation step: 
If the hidden/latent variable is complex, computing the posterior can become intractable. In something like a neural network, where $X$ can be a highly non-linear function of $Z$, calculating the posterior is intractable. This is the motivation for [[VAE]] and a lot of [[Variational Inference]].