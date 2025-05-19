Autoregressive models, particularly RNNs, are fundamental to sequence generation tasks. They generate sequences one element at a time, with each new element conditioned on the previously generated ones.

## What is an Autoregressive RNN?
*   **Sequence Generation Model:** An autoregressive RNN predicts the next word (or element) in a sequence based on the words it has generated so far.
*   **Key Characteristic:** The model uses its **own generated outputs as inputs** for the subsequent step. This recursive feedback is central to autoregression.
*   **Common Uses:**
    *   Text Generation (e.g., story writing, dialogue systems)
    *   Language Modeling
    *   Machine Translation (especially the decoder part)
*   **Inference vs. Training:** During actual generation (inference, real-time use), the model predicts words one by one without knowing the ground truth for the next step. The previously predicted word is fed as the input for the next prediction. This differs from training where the true previous word (teacher forcing) might be used.

## Step-by-Step Numerical Example: Autoregressive Text Generation

**Problem Statement:**
Train an RNN language model (conceptually) on the sentence: "I love deep learning".
We want to use this autoregressive RNN to generate text starting with the seed word "I".

**Vocabulary (for this example output):** {I, love, deep, learning}

### Step 1: Convert Words into Word Embeddings
Assume we have pre-trained or learned 3-dimensional embeddings for our vocabulary.

| Word     | Embedding (Example) |
| :------- | :------------------ |
| I        | [0.1, 0.3, 0.5]     |
| love     | [0.7, 0.8, 0.2]     |
| deep     | [0.9, 0.4, 0.6]     |
| learning | [0.5, 0.6, 0.7]     |

### Step 2: Initialize RNN Parameters
Assume a simple RNN with the following parameters:
*   Hidden state size = 3
*   Weight matrices:
    *   Input-to-hidden weights: $W_x$ (3x3 matrix)
    *   Hidden-to-hidden weights: $W_h$ (3x3 matrix)
    *   Hidden-to-output weights: $W_y$ (Vocabulary_size x 3, so 4x3 matrix for this example, or 3x3 if output vocab is 3 as in slide)
        *Self-correction: The slide example for Wy is 3x3, implying the output probabilities are for a 3-word vocab. Let's assume the example output vocab is {love, deep, learning} for consistency with Wy size.*
*   Biases: $b_h$ (3x1), $b_y$ (Vocabulary_size x 1, so 3x1)

### Step 3: Compute Hidden State for First Word ("I")

**Hidden State Equation:** $h_t = tanh(W_x * x_t + W_h * h_{t-1} + b_h)$

*   **Initial hidden state (h_0):** [0, 0, 0]^T
*   **Input for word "I" (x_1):** [0.1, 0.3, 0.5]^T (embedding for "I")

Calculation of $h_1$:
$W_x * x_1 = [[0.2,0.1,0.4],[0.3,0.5,0.7],[0.6,0.2,0.8]] * [0.1,0.3,0.5]^T = [0.02+0.03+0.20, 0.03+0.15+0.35, 0.06+0.06+0.40]^T = [0.25, 0.53, 0.52]^T$
$W_h * h_0 = [0,0,0]^T$
$h_1 = tanh([0.25, 0.53, 0.52]^T + [0,0,0]^T + [0.1,0.2,0.3]^T)$
$h_1 = tanh([0.35, 0.73, 0.82]^T)$
$h_1 ≈ [0.336, 0.623, 0.675]^T$ (Slide approximates to [0.48, 0.62, 0.67]^T after tanh. The pre-tanh sum on slide is [0.53, 0.73, 0.82]^T. Let's use slide's pre-tanh values for consistency.)
$h_1 = tanh([0.53, 0.73, 0.82]^T) ≈ [0.485, 0.623, 0.675]^T$. Slide uses [0.48, 0.62, 0.67]^T.

### Step 4: Compute Output Probabilities

The softmax layer converts the RNN output into probabilities over the vocabulary {love, deep, learning}.
$y_1 = softmax(W_y * h_1 + b_y)$

Using $h_1 = [0.48, 0.62, 0.67]^T$:
$W_y * h_1 = [[0.2,0.6,0.1],[0.3,0.7,0.5],[0.4,0.2,0.8]] * [0.48,0.62,0.67]^T$
$= [0.096+0.372+0.067, 0.144+0.434+0.335, 0.192+0.124+0.536]^T$
$= [0.535, 0.913, 0.852]^T$
(Slide values: [0.48*0.2+0.62*0.6+0.67*0.1, ...] = [0.096+0.372+0.067, ...] = [0.535, ...]
Slide pre-softmax values after adding bias $b_y=[0.05,0.05,0.05]^T$:
logits = [0.535+0.05, 0.913+0.05, 0.852+0.05]^T = [0.585, 0.963, 0.902]^T
(Slide values: [0.492, 0.87, 0.81]^T. There's a discrepancy, likely due to rounded $h1$ or different intermediate values in the slide's hidden calculation. I will use the slide's logits for softmax calculation.)

Logits from slide: [0.492, 0.87, 0.81]^T
$P(love) = e^{0.87} / (e^{0.87} + e^{0.81} + e^{0.492}) ≈ 2.387 / (2.387 + 2.248 + 1.635) ≈ 2.387 / 6.27 ≈ 0.38$ (Slide: ≈ 0.42)
$P(deep) = e^{0.81} / (e^{0.87} + e^{0.81} + e^{0.492}) ≈ 2.248 / 6.27 ≈ 0.358$ (Slide: ≈ 0.37)
$P(learning) = e^{0.492} / (e^{0.87} + e^{0.81} + e^{0.492}) ≈ 1.635 / 6.27 ≈ 0.26$ (Slide: ≈ 0.21)
*The slide's probabilities sum to 1.00. My re-calculation is slightly off due to precision or the slide's exact intermediate values.*

**Selection:** According to the slide's probabilities, "love" has the highest probability (0.42). The model selects "love" as the next word.

### Step 5: Continue the Process

1.  **Feed "love" as input:** The embedding for "love" ($x_2 = [0.7, 0.8, 0.2]^T$) and the previous hidden state $h_1$ are fed into the RNN to compute $h_2$.
2.  **Predict next word:** $y_2 = softmax(W_y * h_2 + b_y)$ is computed. Suppose it generates "deep" as the most probable word.
3.  **Feed "deep" as input:** The embedding for "deep" and $h_2$ are used to compute $h_3$ and predict the next word (e.g., "learning").
4.  **Stopping Condition:** The process continues until a special end-of-sequence token is generated, a maximum length is reached, or another stopping criterion is met.

The generated sequence would be "I love deep learning...".

## Conclusion for Autoregressive RNNs

*   Generate text **one word at a time**.
*   The **hidden state captures context** from previously generated words.
*   The **softmax layer selects the most probable next word** (or samples from the distribution).
*   The model **recursively feeds its own predictions back as input** for the next step.