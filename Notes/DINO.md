---
created: 2026-03-06T13:00
updated: 2026-03-06T13:00
tags:
  - "#ml/papers"
featured_image: imgs/Pasted image 20260306113644.png
thumbnail: imgs/resized/423355b808aa5bf2d63d117f8e4a407f_86cf658e.webp
---
---
[Link](https://arxiv.org/pdf/2104.14294)
[Code](https://github.com/facebookresearch/dino)

Background Papers/Info:
- [[Self-supervised Learning]] 
- [[ViT]]
---

Summary: 
Main goal of the paper is to use self-supervision to train a [[ViT]] so that the resulting model learns particularly robust representations. In practice, the model tends to learn semantic segmentation feature maps particularly well. They do this through self-DIstillation with NO labels.

![[Pasted image 20260306113644.png]]

The general idea from the DINO paper is that we want to train a student model with the same architecture and weights as its teacher. The main question is how to do this without the models collapsing to the same result. 

They do this through a few novel methods. 

First, they extract different views. 2 of which are global views, and the rest are smaller, local patches. The global views are only used by the teacher model, but the student receives all of the views. This promotes some type of local-to-global correspondence as they say in the paper. 

Second, gradients are only passed through the student network with [[Stochastic Gradient Descent|SGD]]. The teacher network only learns through the update rule:

$$
\theta_t = \lambda\theta_t + (1 - \lambda)\theta_s, \lambda\text{ is chosen to be close to 1 and scheduled}
$$
Third, to help avoid collapse, two things are done to the teacher networks outputs. The outputs are centered so that no single dimension dominates the output. Then, a small temperature value is applied to the softmax used for the teacher, this helps the teacher avoid collapse to a uniform distribution. 
