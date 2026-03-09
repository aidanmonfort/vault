---
created: 2025-03-06T09:36
updated: 2025-03-13T09:07
tags:
  - ml/architecture/components
---
---
Now that we know what [[Attention]] is, how is it actually used in practice?

If we have just one set of $Q, K, V$ matrices, for any given sequence, is there only one good answer for attention scores? 

Probably not, so we use concatenated attention heads that are then projected with a final matrix. 
In essence, given $\{ SA_{1}, SA_{2}, \dots, SA_{n}\}$ we have:
$$
\text{MHA}(X) = [SA_{1}(X), \dots, SA_{n}(X)]W_{O}, W_{O} \in \mathbb{R}^{nd_{k} \times d_{\text{proj}}}
$$

Where each $SA_{i}$ has its own $Q, K, V$ matrices. 

Pretty simple idea overall, but tends to be a little VRAM bottled necked in long context because of [[KV Caching]]. Some alternatives to MHA are [[Multi-query Attention|MQA]], [[Grouped-query Attention|GQA]], and [[Multihead Latent Attention|MLA]]. 