---
created: 2025-03-06T09:36
updated: 2025-03-13T09:07
tags:
  - ml/architecture/components
  - video
featured_image: imgs/youtube/0VLAoVGf_74.webp
thumbnail: imgs/resized/4995f977c0377e12f204c1037a8fd0bc_86cf658e.webp
---
---
![Link](https://youtu.be/0VLAoVGf_74?si=cNWfYzDZ2IK5t6oQ)

---
## Core Ideas:
- [[Attention]]
- [[KV Caching]]
- [[Latent Spaces]]

Instead of sharing the $K, V$ matrices across heads, we only share the projection from the latent space between heads and this projection matrix is shared between both $K, V$ matrices. 

So, the flow is like this:

$$
X \overset{W_{Q}W_{UK}^T}{\to} X(W_{Q}W_{UK}^T) \overset{L_{KV}^T}{\to} QK^T \to \text{softmax}\left( \frac{QK^T}{\sqrt{ d }} \right) \overset{L_{KV}}{\to} AL_{KV} \overset{W_{UV}}{\to} \text{Self-Attention(X)}
$$
$L_{KV} = XW_{DKV}$, essentially a projection matrix for our latent space. 

In words, starting from input matrix $X$, we perform a query projection + key matrix multiplication + $QK^T$ projection into latent space at the same time. Then, we project out of the latent space to get our standard $QK^T$ matrix. 

This attention is then sent back into latent space. Then, we finally project into normal space + perform value projection at the same time. After this, we can finally perform our output attention across heads.  

---
### Result
- KV Cache per token = $d_{l}l$, the dimension of the latent space and the layers.
- Also, somehow attention is better as a whole?
- This is magic(not really a result) 