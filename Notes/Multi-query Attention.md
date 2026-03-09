---
created: 2025-03-06T09:36
updated: 2025-03-13T09:07
tags:
  - ml/architecture/components
---
---
To address the large KV cache sizes of [[Multihead Attention|MHA]], an alternative is Multi-Query Attention(MQA). 
From MHA, we have $\{ SA_{1}, SA_{2}, \dots, SA_{n}\}$, where each $SA_{i}$ has its own $Q_{i}, K_{i}, V_{i}$.

In MQA, each $SA_{i}$ share $K, V$ matrices but maintain their own independent query matrices. 
In practice, you lose performance, but it still is a viable option for reducing [[KV Caching|KV Cache]] sizes. 