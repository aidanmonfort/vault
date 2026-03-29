---
created: 2026-03-09T18:00
updated: 2026-03-09T18:01
tags:
  - ml
featured_image: Screenshot 2026-03-11 at 11.46.57 PM.png
thumbnail: imgs/thumbnails/resized/5b0309facdfc782135509eab0302bea6_86cf658e.webp
---
---

At a high level, Diffusion is a process that aims to reverse some forward process in which ordered data becomes discorded and noisy. 

---
### Forward Process

The forward process can be modeled as a Markov chain where any given step only depends on its previous state. ![[Screenshot 2026-03-11 at 11.46.57 PM.png]]

The noise is typically Gaussian and each step in the chain is usually determined by a variance schedule(usually linear or cosine). 

Specifically, at any given step $\mathbf{x}_{t-1}$ we have:
$$
q(\mathbf{x}_{t}|\mathbf{x}_{t-1}) = \mathcal{N}(x_{t}; \sqrt{ 1- \beta_{t} }x_{t-1}, \beta_{t}\mathbf{I})
$$
Essentially, we have a gaussian centered at $\mathbf{x}_{t-1}$ with some variance $\beta_{t}$ added to produce this random walk. The $\sqrt{ 1-\beta_{t} }$ is to control exploding variances. If that was not there, then the variances would grow linear as they sum every time step in the markov chain.

Let $\alpha_{t} = 1 - \beta_{t}$. Notice:
$$
\begin{align}
\mathbf{x}_{1} &= \sqrt{ \alpha_{1} }\mathbf{x}_{0} + \sqrt{ 1 - \alpha_{1} }\epsilon_{1} \\
\mathbf{x}_{2} &= \sqrt{ \alpha_{2} }\mathbf{x}_{1} + \sqrt{ 1 - \alpha_{2} }\epsilon_{2} \\
\end{align}
$$
When we substitute, we can get:

$$
\begin{align}
\mathbf{x}_{2} &= \sqrt{ \alpha_{2} }(\sqrt{ \alpha_{1} }\mathbf{x}_{0} + \sqrt{ 1 - \alpha_{1} }\epsilon_{1}) + \sqrt{ 1 - \alpha_{2} }\epsilon_{2} \\
\mathbf{x}_{2} &= \sqrt{ \alpha_{2}\alpha_{1} }\mathbf{x_{0}} + \sqrt{ \alpha_{2} - \alpha_{2}\alpha_{1} }\epsilon_{1} + \sqrt{ 1-\alpha_{2} }\epsilon_{2}
\end{align}
$$

Adding these two Gaussian and their variances lead to:
$$
\mathbf{x}_{2} = \sqrt{ \alpha_{2}\alpha_{1} }\mathbf{x_{0}} + \sqrt{ 1 - \alpha_{2}\alpha_{1} }\epsilon
$$
When you continue this, the result is:

$$
\mathbf{x}_{t} = \sqrt{  \bar{\alpha}_{t}}\mathbf{x_{0}} + \sqrt{ 1 - \bar{\alpha}_{t} }\epsilon
$$

Where $\bar{\alpha}_{t} = \Pi_{i=1}^{t}\alpha_{i}$. 

This is pretty important when it comes to training, since this efficient sampling of $\mathbf{x}_{t}$ is one of the primary things that allows us to train effectively. 


---
### Reverse Process
![[Screenshot 2026-03-11 at 11.46.13 PM.png]]

Rather than trying to learn the Gaussian conditioned on $\mathbf{x}_{t-1}$ to get $\mathbf{x}_{t}$, and sampling from the Gaussian we can just learn the noise added at any given $t$. This is better since learning the data manifold throughout the markov chain is much much more difficult than the noise(just a Gaussian pretty much). 

If we have a model, $\epsilon_{\theta}(\mathbf{x_{t}}, t)$ that predicts the noise properly for $t$, then inference is fairly simple. 

Moving from $\mathbf{x}_{t} \to \mathbf{x_{0}}$ is just basically doing $\mathbf{x}_{t-1} = \mathbf{x_{t}} - c\epsilon_{\theta}(\mathbf{x_{t}}, t)$. There is some stuff with scaling based on our variance that is important, but the backwards steps are fairly simple. In practice, some more noise can be added to each of these backwards steps to make the generation more stochastic.  

---
### What does noise look like in different problem spaces?

From what I have seen, I think the biggest challenge in applying diffusion to different generation tasks can be determining what "noise" looks like and what it means to "add noise" to structured data. 
It seems like this choice is very make or break. In images, this is very simple since pixel space is very interpretable but in other things, like text generation, this is a lot more nuanced. 

---
Note: images from DDPM paper.