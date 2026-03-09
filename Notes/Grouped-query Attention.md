---
created: 2025-03-06T09:36
updated: 2025-03-13T09:07
tags:
  - ml/architecture/components
---
---
### Problems:
- [[Multihead Attention|MHA]] has large [[KV Caching|KV cache]] sizes
- [[Multi-query Attention|MQA]] loses too much performance

### GQA
Grouped-Query Attention(GQA) is the middle ground between these two ideas. 
Give our original formulation of MHA, $\{ SA_{1}, SA_{2}, \dots, SA_{n}\}$. Instead of just sharing the value matrix across all [[Attention]] heads, we break the set of attention heads into $k$ groups. 

Then, group $i$ will have their own shared $V_{i}$ for every attention head in the group.

---
### Impact:
[[KV Caching|KV Cache]] size for just MHA is $2 \times n \times l \times N \times d_{\text{head}}$. Where $n$ is the number of heads per layer, $l$ is the number of layers, $N$ is the sequence length, and $d_{\text{head}}$ is the internal dimension of the attention projections. 

For GQA, we reduce this by $k$ because of the grouping. It's not as much as MQA, but we are able to save more performance. 

- Used in Meta's Llama 3 models. 