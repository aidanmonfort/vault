---
created: 2026-03-19T10:34
updated: 2026-03-19 10:35
tags:
featured_image: imgs/vae_latent_scatter.png
thumbnail: imgs/resized/8d89b52bbf3d530bfbcab0cf31605d64_86cf658e.webp
---
---
[Link](https://arxiv.org/pdf/1312.6114)

### Related Topics:
- [[Autoencoders]]
- [[Expectation-Maximization]]

### Notes: 
---

Assume we have some fairly large dataset $X$ that has $n$ samples. We assume that the data is generated using some hidden latent variables. However, we want these latent variable to be *continuous* rather than discrete. 

More concretely, we have a latent variable $\mathbf{z}$ that is generated from a prior $p_{\theta}(\mathbf{z})$ and then some conditional distribution $p_{\theta}(\mathbf{x}^i | \mathbf{z})$ that we can use to generate the data. 

Because of the setup, the marginal distribution for $\mathbf{x}$ is $p_{\theta}(\mathbf{x}) = \int p_{\theta}(\mathbf{x}|\mathbf{z})p_{\theta}(\mathbf{z})d\mathbf{z}$. We want to assume that this is intractable.

In the same way, we assume the posterior:
$$
p_{\theta}(\mathbf{z}|\mathbf{x}) = \frac{p_{\theta}(\mathbf{x}|\mathbf{z})p_{\theta}(\mathbf{z})}{p_{\theta}(\mathbf{x})}
$$
is intractable. 

This eliminates two simple methods for optimizing $\theta$. 
Since the marginal is intractable, we can't just differentiate to find $\theta$. Since the posterior is intractable, we can not do the first step of the EM algorithm. Next, since we assume the dataset is large, we can not do any type of sampling thing since it is going to be slow. 

We want to find a way to use mini-batches to do some type of gradient method for the parameters $\theta$. 

### ELBO Derivation:
---


### VAE:
---
When we train a VAE using purely the KL divergence, the resulting latent space looks something like:
![[vae_latent_scatter.png]]

This is to be expected, since we decided the prior was a standard normal, the model will just project to the standard normal, this is not really useful, and our decoder actually won't even be trained since it does not get used. 

When we add our reconstruction loss. Note: I used [[Loss Functions#MSE|MSE]] as reconstruction loss, but [[Loss Functions#Binary Cross-Entropy|BCE]] will work too:
![[vae_elbo_latent_bce_scatter.png]]

The result is clustered samples where the posterior is still close to the standard normal. Making this dense around the unit circle means we can efficiently sample from the posterior to generate new samples or augment existing ones in a predictable manner.
Note: I train for only ~100 epochs here, but longer would help with the squeeze into the standard normal. 

We aren't as likely to fall into pure noise like with standard autoencoders. We can visualize the data manifold too with the unit square. 

![[vae_elbo_manifold_bce_grid.png]]
