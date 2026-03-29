---
created: 2026-03-27T22:29
updated: 2026-03-27T22:29
tags:
  - ml
  - math
---
---
Here is a collection of loss functions, with different use cases. 

## Regression
---
Losses used for regression tasks.

### MSE
---
Mean Squared Error(MSE) is extremely common in neural network training since it is a very nice, easily differentiable, comparison between two tensors. 

$$
\mathcal{L}(y, \hat{y}) = \frac{1}{n}\sum_{i=1}^{n}(y_{i} - \hat{y}_{i})^{2}
$$
Used in a **LOT** of different contexts, and can have many different interpretations depending on the context but at its core, it is essentially a dissimilarity measure of just two tensors.  

Always convex and differentiable which means very stable when there are not extreme outliers. 

### MAE
---
Mean Absolute Error(MAE) is very similar to MSE, but is used in contexts where outliers are not super uncommon such as finance. 

$$
\mathcal{L}(y, \hat{y}) = \frac{1}{n}\sum_{i=1}^{n}|y_{i}-\hat{y}_{i}|
$$

Can struggle with convergence around minimums. 

## Classification
---
Losses used for classification tasks. 

### Binary Cross-Entropy
---
