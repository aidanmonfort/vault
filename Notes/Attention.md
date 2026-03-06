---
created: 2025-03-06T09:36
updated: 2025-03-13T09:07
tags:
  - ml/architecture/components
---
---
## Problem
The problem with language modeling is the sequential aspect of it. Prior to the concept of self-attention, the common approach was to use different types of gated neural network architectures such as [[LSTM]] or [[Recurrent Neural Networks|RNNs]].

One of the issues with these architectures is the handling of long context scenarios. Given a paragraph, or even a set of paragraphs, it is difficult to perform auto-regressive(next token) modeling as context gets lost in the many tokens from the paragraphs. 

## How Attention Works
---
Given a sequence of token embeddings, $W \in \mathbb{R}^{N \times d}$, we compute three new data matrices.

1. $Q = WQ_{proj}, Q \in \mathbb{R}^{N \times d_k}$, The query matrix is generally thought of as each token *asking* a question.
2. $K = WK_{proj}, K \in \mathbb{R}^{N \times d_k}$, The key matrix is thought of as each token *answering* a question. 
3. $V = WV_{proj}, V \in \mathbb{R}^{N \times d_k}$, The value matrix, is essentially: given how the tokens attend to each other, how should we actually update their embeddings.

Then, attention is computed as 
$$
\text{Attention}(Q, K, V) = \text{softmax}(\frac{QK^T}{\sqrt{d_k}})V
$$
This is only a single head of attention, to make this better, [[Multihead Attention|MHA]] is normally used. 
### So how do we interpret this?
---
First, the $QK^T$ is the dot product matrix produced by multiplying our query projections of each token with the key projections of each token. Essentially, how similar are these projections/how *well* does a token answer a question. 

These values are then scaled by the square root of their dimensionality. 
Applying the softmax function to this $QK^T \in \mathbb{R}^{N \times N}$  matrix on the columns only is turning each column into a probability distribution that models the importance of the token $i$ on every other token in column $i$. 

For interpretability, this tends to be very important, as attention maps can be modeled and we get a sort of heatmap for how tokens are attending to each other. 

After this softmax function, we multiply by, $V$, the value matrix. This is simply how are we actually updating our token embeddings based on the attention that we see. 

There are some interesting properties of the $QK^T$ matrix. In the original setting, the bottom right half of this matrix is masked. What this is doing in the context of NLP is ensuring that our model is not "cheating" by using the "future" tokens to attend to previous tokens. 

### Efficiency
---
There are a few tricks that can be used to make everything more efficient. First, we can compute the query, key, and value matrices all at the same time. We do this by using a lot of concatenation:
$$
[Q, K, V] = W[Q_{proj}, K_{proj}, V_{proj}]
$$

Another useful trick for inference is $KV$ caching. In this standard auto-regressive approach, if we wanted to calculate the attention for an $N$ length sequence of tokens, we would need to perform an $O(n^{2})$ operation. 

In the context of [[LLM|LLMs]], this is pretty much impossible. This value of $N$ tends towards extremely large values so for generating a new token, we need to optimize. An observation is that if we want to produce a new token, to create its embedding, we only need to compute its query matrix and then multiply that with the stored $K, V$ matrices. 

The result of this is that the next token will only be an $O(n)$ operation which is much better. However, like a lot of things in machine learning, this introduced its own issue. 

How do we efficiently store $KV$ cache as $N$ grows. Given a context of length $N$, we need to store $N \times d_{k} + N \times d_{k}$ matrices just for each head of attention. Given multiple heads and multiple layers, this does not scale well. 

There's a whole block of research on [[KV Caching]], so for methods, look there. 