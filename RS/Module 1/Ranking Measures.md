### 1. NDPM (Normalized Distance-based Performance Measure)
- It measures how well its predict ratings align with actual user ratings
- It gives more weight to highly rated items and penalizing for incorrect predicts on highly rated items
- It also considers the position of the item within the recommended list.

### 2. Spearman's Correlation
- Evaluates "ranking accuracy" by checking "if our ranking is similar to the true ranking".
- It measures the strength and similarity between monotonic relationships between 2 ranked variables.
- It value ranges from -1 to +1
$$
\rho = 1 - \frac{6 \sum d_i^2}{n(n^2 - 1)}
$$

where:
- $d_i$ is the difference between 2 ranks
- $n$ is the number of observations


### 3. R - Score