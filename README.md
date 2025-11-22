# MSCS_634_Lab_5
## Purpose of the Lab

The goal of this lab is to practice unsupervised learning techniques using the Wine dataset from
`sklearn.datasets`. I focus on two clustering algorithms:

- Agglomerative Hierarchical Clustering  
- DBSCAN (Density-Based Spatial Clustering of Applications with Noise)

The lab walks through loading and standardizing the data, applying both clustering methods, visualizing
the resulting clusters, and evaluating them with several metrics. This helps build intuition for how
different clustering approaches behave on the same dataset.

## Key Insights from the Clustering Results

- After standardizing the features, the Wine samples form fairly well-separated groups in PCA space.  
- Agglomerative Hierarchical Clustering works well when the number of clusters is chosen close to the
  true number of wine classes (for example, three clusters). In that case, silhouette, homogeneity, and
  completeness scores are reasonably high, and the clusters look compact in the 2D PCA projection.
- The dendrogram gives a useful visual summary of how clusters merge as the distance threshold increases
  and helps identify a reasonable cut level for selecting `n_clusters`.
- DBSCAN provides a very different view of the data. Rather than specifying the number of clusters, it
  discovers dense regions based on `eps` and `min_samples`. With well-chosen parameters, DBSCAN can
  identify clusters and naturally treat outliers as noise points.
- Parameter tuning has a big impact on DBSCAN. If `eps` is too small, many points are labeled as noise.
  If `eps` is too large, most samples collapse into one or two large clusters. The metrics table in the
  notebook helps compare different settings.

Overall, the lab shows that there is no single “best” clustering algorithm. Hierarchical clustering is
great for interpretability and exploring the hierarchy of clusters, while DBSCAN shines when you care
about dense regions and want to explicitly mark potential outliers.

## Challenges and Decisions

- One of the main challenges was selecting meaningful parameter values for DBSCAN. I had to experiment
  with several combinations of `eps` and `min_samples` to avoid extreme cases where almost everything
  became noise or everything merged into a single cluster.
- For Agglomerative Clustering, I compared different values of `n_clusters` and relied on both the
  evaluation metrics and the PCA plots to decide which setting best matched the underlying structure
  of the Wine data.
- Another small design decision was to use PCA to reduce the data to two dimensions for visualization.
  This does not affect the clustering itself (which is done on the full standardized feature space),
  but it makes the clusters much easier to interpret visually in the notebook.
