---
created: 2026-03-06T13:01
updated: 2026-03-06T13:22
tags:
  - ml/papers
featured_image: imgs/Screenshot 2026-03-06 at 1.03.22 PM.png
thumbnail: imgs/resized/2e01b45203712eca7818fddfa4df994d_86cf658e.webp
---
---
[Link](https://arxiv.org/pdf/2010.11929)
[Code](https://github.com/google-research/vision_transformer)

Background Papers/Info:
- [[Attention]] 
---

Summary: 
![[Screenshot 2026-03-06 at 1.03.22 PM.png]]

The transformer architecture was integral to the development of modern [[LLM]]'s, but the standard in [[Computer Vision]] at the time was still just to use other backbones like [[ResNet]] or standard [[Convolutional Neural Networks|CNNs]]. This paper essentially changes this. Their core idea is very simple. In the same way that [[LLM|LLMs]] treat training text as a stream of tokens, a given image can be broken into a stream of input tokens that are just patches from the image. 

The paper reports extremely strong results when pre-training models on the massive JFT-300M dataset but still is outperformed by [[ResNet|ResNets]] when pre-trained on moderately sized models like ImageNet1k. 

The [[Transformer]] is known to be prone to overfitting on smaller datasets and that pattern stays pretty consistent here, but when training on the larger dataset, the large sample size allows the transformer to generalize well and achieve the SOTA.  