## 1. Ranking Loss: General Concept
- **Definition**: A category of loss functions designed to train models that learn a similarity or distance metric.
- **Goal**: To ensure a correct *ordering* or *ranking* of data points based on their similarity or relevance.
- **Application**: Common in tasks like face verification, image retrieval, recommendation systems, where the relative similarity between items is more important than absolute classification.
- **Mechanism**: Typically works by penalizing the model if dissimilar items are closer in the embedding space than similar items, or if similar items are too far apart.

## 2. Contrastive Loss (Pairwise Ranking Loss)
- **Purpose**: Used with Siamese Networks (or similar architectures) that process pairs of inputs. It aims to learn an embedding space where:
	- **Similar (positive) pairs** have a small distance between their embeddings.
	- **Dissimilar (negative) pairs** have a large distance between their embeddings, separated by at least a predefined **margin `(m)`**.
- **Formula**:
  `L(Y, D) = (1 - Y) * D^2 + Y * max(0, m - D)^2`
  Where:
	- `Y`: Label for the pair. `Y = 0` if the pair is similar (positive), `Y = 1` if the pair is dissimilar (negative).
	- `D`: Euclidean distance (or other distance metric) between the embeddings of the two inputs in the pair. `D = ||f(x1) - f(x2)||_2`.
	- `m`: A predefined margin. This hyperparameter controls how far apart dissimilar pairs should be.
- **How it Works**:
	- **Case 1: Similar Pair (Y = 0)**
		- `L = (1 - 0) * D^2 + 0 * max(0, m - D)^2 = D^2`
		- The loss is simply the squared distance `D^2`.
		- To minimize this loss, the network tries to reduce `D`, pulling the embeddings of similar items closer together.
	- **Case 2: Dissimilar Pair (Y = 1)**
		- `L = (1 - 1) * D^2 + 1 * max(0, m - D)^2 = max(0, m - D)^2`
		- If `D >= m` (dissimilar pair is already further apart than the margin), then `m - D <= 0`, so `max(0, m - D)^2 = 0`. No loss is incurred, no update needed.
		- If `D < m` (dissimilar pair is closer than the margin), then `m - D > 0`, so `L = (m - D)^2`. The loss penalizes this small distance, forcing the network to increase `D` (push embeddings apart) until `D` is at least `m`.
- **Margin `(m)`**: Crucial. It defines the radius around an embedding within which no dissimilar embeddings should fall. It increases the separation between similar and dissimilar vectors.
- **Oral Q**: Why not use standard classification loss (e.g., cross-entropy) for Siamese networks?
	- Siamese networks aim to learn a *similarity/distance metric*, not to classify inputs into predefined categories. Contrastive loss directly optimizes this distance in the embedding space. Cross-entropy is designed for classification tasks with fixed output classes.

## 3. Triplet Loss (Relative Ranking Loss)
- **Purpose**: Used with Triplet Networks (which often use a Siamese-like architecture with three shared-weight branches or process three inputs sequentially). It aims to learn embeddings such that an **anchor** sample is closer to a **positive** sample (same class as anchor) than it is to a **negative** sample (different class from anchor), by at least a margin.
- **Input Triplet**:
	- **Anchor (A)**: A reference sample.
	- **Positive (P)**: A sample from the same class as the Anchor.
	- **Negative (N)**: A sample from a different class than the Anchor.
- **Goal**: `distance(A, P) + margin < distance(A, N)`
- **Formula**:
  `L(A, P, N) = max(0,  d(A, P)^2 - d(A, N)^2 + m)`
  or often `L(A, P, N) = max(0,  d(A, P) - d(A, N) + m)` (using non-squared distances)
  Where:
	- `d(A, P)`: Distance between the Anchor and Positive embeddings.
	- `d(A, N)`: Distance between the Anchor and Negative embeddings.
	- `m`: A predefined margin.
- **How it Works**:
	- The loss is zero if the negative sample is already farther from the anchor than the positive sample by at least the margin `m` (i.e., `d(A, N) > d(A, P) + m`).
	- If this condition is not met, the loss is positive, and the network is penalized. The optimization process will try to:
		- Decrease `d(A, P)` (pull Anchor and Positive closer).
		- Increase `d(A, N)` (push Anchor and Negative further apart).
- **Triplet Mining**: Selecting informative triplets (hard triplets where `d(A,P)` is large or `d(A,N)` is small) is crucial for efficient training. Training on easy triplets (where the condition is already met) provides no learning signal.
- **Comparison: Contrastive vs. Triplet Loss**:

	| Feature             | Siamese Network (Contrastive Loss)        | Triplet Network (Triplet Loss)                     |
	|---------------------|-------------------------------------------|----------------------------------------------------|
	| **Inputs/Training** | Pairs (Similar or Dissimilar)             | Triplets (Anchor, Positive, Negative)              |
	| **Optimization Goal**| Learn absolute similarity between two inputs| Learn *relative* similarity between three inputs   |
	| **Distance Calc.**  | Computes distance between a pair          | Computes relative distances (A-P vs. A-N)          |
	| **Training Efficiency**| Can be inefficient if trained on many easy pairs | More efficient with hard triplet mining            |
	| **Sensitivity**     | Can struggle with small intra-class variations | Handles variations better due to relative comparisons |
	| **Generalization**  | Good for binary verification (same/different) | Better for ranking-based tasks (e.g., best match)  |
	| **Applications**    | Signature verification, image retrieval   | Face recognition (FaceNet), speaker verification   |

## 4. How Loss Functions Help in Similarity Learning
- **Encourage Similarity for Positive Pairs/Triplets**: The network learns to reduce the distance between embeddings of similar items.
- **Encourage Dissimilarity for Negative Pairs/Triplets**: The network learns to increase the distance between embeddings of dissimilar items.
- **Optimize Feature Representation**: Helps the underlying CNN (feature extractor) learn discriminative features that are useful for distinguishing between classes based on similarity.
- **Improve Generalization**: Ensures the learned similarity metric can correctly compare unseen data during inference.