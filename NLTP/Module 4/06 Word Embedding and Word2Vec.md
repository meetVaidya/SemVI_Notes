# Word Embeddings and Word2Vec

## From Count Vectors to Dense Embeddings  
Traditional DSMs produce high‑dimensional, sparse vectors. Neural embeddings condense semantics into low‑dimensional, dense vectors:

- **Goal:** Capture semantic similarity and analogical relations in compact form.  
- **Advantages:**  
  - Reduced storage and computation.  
  - Improved performance on similarity and downstream tasks. :contentReference[oaicite:0]{index=0}:contentReference[oaicite:1]{index=1}  

---

## Similarity Metrics Refresher
- **Dot Product:**  
  \[
    \langle \mathbf{u}, \mathbf{v} \rangle = \sum_i u_i\,v_i
  \]  
  - Sensitive to vector norms; longer vectors yield larger values.  
- **Cosine Similarity:**  
  \[
    \cos(\mathbf{u}, \mathbf{v}) = \frac{\langle \mathbf{u}, \mathbf{v} \rangle}{\|\mathbf{u}\|\;\|\mathbf{v}\|},
  \]  
  - Normalizes for length; returns value in \([-1,1]\) for signed spaces or \([0,1]\) for non‑negative.  
  - Preferred for comparing semantic closeness. :contentReference[oaicite:2]{index=2}:contentReference[oaicite:3]{index=3}  

---

## Word2Vec Overview
Word2Vec (Mikolov et al., 2013) learns embeddings by predicting context words from targets (or vice versa) using a shallow neural network.

### Objectives
- **CBOW (Continuous Bag‑of‑Words):**  
  - Predicts the target word given its surrounding context words.  
  - Aggregates context (summing or averaging embeddings) before prediction.  
- **Skip‑Gram:**  
  - Predicts each context word given the target.  
  - Maximizes the probability of observing context words conditioned on target embedding. :contentReference[oaicite:4]{index=4}:contentReference[oaicite:5]{index=5}  

### Architecture Details
#### CBOW  
1. **Input layer:** One‑hot vectors for each context word.  
2. **Hidden layer:** Shared weight matrix \(W\in\mathbb{R}^{|V|\times d}\).  
   - Embedding lookup: \( \mathbf{e}_c = W^\top \mathbf{x}_c \).  
   - Aggregate context embeddings: \( \mathbf{h} = \frac{1}{|C|}\sum_{c\in C}\mathbf{e}_c \).  
3. **Output layer:** Softmax over vocabulary using weights \(W'\in\mathbb{R}^{d\times|V|}\).  
4. **Loss:** Negative log likelihood of true target. :contentReference[oaicite:6]{index=6}:contentReference[oaicite:7]{index=7}  

*(Image context: CBOW network diagram showing context inputs, embedding layer, hidden average, and softmax output.)*

#### Skip‑Gram  
1. **Input layer:** One‑hot vector for target word.  
2. **Hidden layer:** Embedding lookup: \( \mathbf{h} = W^\top \mathbf{x}_w \).  
3. **Output layer:** Softmax over vocabulary for each context position using \(W'\).  
4. **Loss:** Sum of negative log likelihoods over all context positions.  
5. **Optimization:** Hierarchical softmax or negative sampling for efficiency. :contentReference[oaicite:8]{index=8}:contentReference[oaicite:9]{index=9}  

*(Image context: Skip‑Gram diagram with target input, embedding layer, and multiple context word outputs.)*

---

## Training Details
- **Window size:** Context window width (e.g., ±5).  
- **Negative Sampling:**  
  - Sample \(k\) noise words per training instance.  
  - Simplifies softmax computation by turning it into binary logistic tasks.  
- **Subsampling of frequent words:**  
  - Discards high‐frequency words with probability \(P(w) = 1 - \sqrt{\frac{t}{f(w)}}\) to balance training. :contentReference[oaicite:10]{index=10}:contentReference[oaicite:11]{index=11}  

---

## Properties of Learned Embeddings
- **Semantic Similarity:** Similar words cluster (e.g., *king* near *queen*).  
- **Linear Analogies:** Vector arithmetic captures analogies:  
  \[
    \mathbf{v}(\text{king}) - \mathbf{v}(\text{man}) + \mathbf{v}(\text{woman}) \approx \mathbf{v}(\text{queen}).
  \]
- **Applications:**  
  - Similarity measurement, clustering, classification.  
  - Initialization for downstream neural models (e.g., RNNs, Transformers).

---

## Practical Tips
- **Dimensionality \(d\):** 100–300 dimensions commonly used.  
- **Corpus size:** Millions of tokens for robust embeddings.  
- **Hyperparameters:** Window size, negative samples \(k\), learning rate, subsampling threshold.  
