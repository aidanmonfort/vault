---
created: 2025-03-06T09:36
updated: 2025-03-13T09:07
tags:
  - ml
---
---
There is a lot of really rich research in the KV Cache space. Some of the research focuses on optimizing the architecture of blocks as seen in: [[Multi-query Attention|MQA]], [[Grouped-query Attention|GQA]], and [[Multihead Latent Attention|MLA]]. 

Other research focuses on reducing the token windows for context length. In any case, there is a hard physical limit to how much $KV$ from the sequence we can actually preserve in VRAM or general memory. 

Some papers focus on how to effectively learn from limited context length in pre-training to allow for longer context lengths in inference. 