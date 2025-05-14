### 2.1 Overview
- **Goal**: Leverage both **past** and **future** context when processing a sequence, rather than only past context as in a standard RNN.
- **Key Idea**: Run two RNNs in parallel—one reading the sequence **forward**, the other **backward**—and combine their outputs for each position.

### 2.2 Architecture
- **Two Hidden Layers**:
  - **Forward RNN** computes hidden states $\overrightarrow{h}_t$ using inputs $x_1\to x_T$.
  - **Backward RNN** computes hidden states $\overleftarrow{h}_t$ using inputs $x_T\to x_1$.
- **Concatenation**: At each time $t$, the combined state $[\overrightarrow{h}_t;\,\overleftarrow{h}_t]$ feeds into the final prediction layer (e.g., a SoftMax classifier).
- **Flexibility**: Any recurrent cell (Simple RNN, LSTM, GRU) may be used in each direction.



### 2.3 BRNN Functions
- **Forward pass** (like a unidirectional RNN):
  $$
    \overrightarrow{h}_t = f\bigl(\overrightarrow{h}_{t-1},\,x_t\bigr)
  $$
- **Backward pass**:
  $$
    \overleftarrow{h}_t = f\bigl(\overleftarrow{h}_{t+1},\,x_t\bigr)
  $$
- **Output layer** at each $t$:
  $$
    o_t = g\bigl([\overrightarrow{h}_t;\,\overleftarrow{h}_t]\bigr)
  $$
  where $g$ might be a feed-forward network plus SoftMax.



### 2.4 Gradient Updating
- Training uses **Backpropagation Through Time** on both directions:
  1. **Forward RNN** unrolled from $t=1$ to $T$.
  2. **Backward RNN** unrolled from $t=T$ down to $1$.
- Gradients from both are aggregated to update shared parameters in each directional RNN.



### 2.5 Working (Step-by-Step)
1. **Inputting a sequence** $\{x_1,\dots,x_T\}$.
2. **Dual processing**:
   - Forward RNN: $\overrightarrow{h}_t$ depends on $\overrightarrow{h}_{t-1}$ and $x_t$.
   - Backward RNN: $\overleftarrow{h}_t$ depends on $\overleftarrow{h}_{t+1}$ and $x_t$.
3. **Hidden‐state computation** at each $t$ via a non-linear activation of a weighted sum.
4. **Output determination** by applying $g$ to $[\overrightarrow{h}_t;\,\overleftarrow{h}_t]$.
5. **Training** by minimizing the discrepancy between each $o_t$ and the true target(s), updating parameters via combined BPTT.


### 2.8 Applications of Bidirectional RNNs

- **Sentiment Analysis**: By incorporating both preceding and following context, BRNNs can more accurately determine whether a sentence expresses positive or negative sentiment.
- **Named Entity Recognition (NER)**: Forward and backward passes allow the model to use context on both sides of a token to decide if it names a person, location, organization, etc.
- **Part-of-Speech Tagging**: Word categories (noun, verb, adjective…) benefit from knowing both earlier and later words for disambiguation.
- **Machine Translation**: In encoder–decoder setups, a bidirectional encoder captures full context before generating each target word.
- **Speech Recognition**: Audio frames are interpreted with knowledge of both past and future sound patterns, improving phoneme and word decoding.



### 2.9 Advantages of BRNNs

- **Full Contextual Awareness**: Processes sequences in both directions, giving each prediction access to past and future information.
- **Improved Accuracy**: Often outperforms unidirectional RNNs on tasks where future context is informative.
- **Robust to Noise**: Dual passes can compensate for noisy or missing data in one direction by leveraging the other.
- **Flexible Length Handling**: Naturally accommodates variable-length inputs without needing positional padding tricks.



### 2.10 Disadvantages of BRNNs

- **Increased Computation**: Requires roughly double the recurrent computations (forward + backward) per sequence.
- **Longer Training Time**: More parameters and sequential dependency in two directions slow down both forward and backward passes.
- **Parallelization Challenges**: Bi-directionality prevents fully streaming inputs in real-time applications where future data isn’t yet available.
- **Risk of Overfitting**: Additional parameters can lead to over-specialization on small datasets if not regularized properly.

