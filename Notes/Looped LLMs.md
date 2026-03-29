---
tags:
  - ml/architecture
  - video
created: 2026-03-08T13:15
updated: 2026-03-09T17:59
featured_image: imgs/youtube/pDsTcrRVNc0.webp
thumbnail: imgs/resized/ba3589add57b55c453909d4c973be858_86cf658e.webp
---
---
![Link](https://youtu.be/pDsTcrRVNc0?si=Be3MxP-CLqrksMs4)

[Link](https://ouro-llm.github.io/)

---
### Core ideas:
- Is reasoning through extended context enough?
- Is reasoning just based on vocabulary enough?

In modern [[LLM|LLMs]], reasoning is accomplished primarily through chain of thought, context scaling, or some type of inference scaling. 

![[Pasted image 20260309120829.png]]

The main idea is using this looped structure architecture with some type of gate to determine whether the output is "refined" enough. They set limits on the number of loops, which makes sense. 

Something not really mentioned in the video the tokens/s. I would imagine that it suffers quite a bit from this looped structure. Additionally, [[KV Caching]] must be a similar challenge since multiple loops means multiple caches. 

It seems like the architecture should in theory be pretty similar to an architecture with residual connections between to the output, although empirically they do outperform other larger models. 

Some more modern diffusion based LLMs have some similar iterative refinement ideas going on. 