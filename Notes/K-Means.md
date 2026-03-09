---
created: 2025-03-06T09:36
updated: 2025-03-13T09:07
tags:
  - ml
  - "#algorithms"
featured_image: imgs/K-means_convergence.gif
thumbnail: imgs/resized/db2a898dab9168e4b06bba2983c634b8_86cf658e.webp
---
---
Classic, elegant, simple algorithm for clustering of data points. The idea is perfectly summed up by the name, *K-means*, we essentially find $k$ mean points, called centroids to cluster our data around. 

Algorithm is as follows:

```python
data = list(points)

centroids = [Centroid() for _ in range(k)]#randomly set to point from dataset

while not converged:
	for point in data:
		nearest_centroid = closest in centroids
		nearest_centroid.add(point)
	
	for centroid in centroids:
		centroid = mean(points in centroid)	

```

---
Here's a nice gif of what is going on above:

![[K-means_convergence.gif]]

Our choices of hyperparameters are distance metric, $k$, and metric for convergence. 

There is another variant called $k$-medoids, where we just make our centroids one of the data points instead of some mean point. 

