## Stacked RNNs (Deep RNNs)

Stacked RNNs involve using multiple recurrent hidden layers.
*   **Architecture:** The output sequence of a lower-level RNN serves as the input sequence to a higher-level RNN. The output of the final (topmost) RNN layer is then used for the task (e.g., prediction or classification).
*   **Benefit:** Deeper architectures can potentially learn more complex representations and hierarchical features from the sequence data.
*   **Considerations:**
    *   The optimal number of stacked layers is application-specific and often determined empirically.
    *   Training costs (computational resources and time) increase significantly as the number of stacks (layers) increases.
## Vanishing and Exploding Gradients

These are common problems encountered during the training of deep neural networks, especially RNNs, due to the nature of backpropagation through many layers (or time steps in unrolled RNNs).

### Vanishing Gradient Problem
*   **Cause:** During backpropagation, gradients are multiplied by weights at each layer. If these weights (or more accurately, the derivatives of activation functions like tanh or sigmoid, which are <1 in many regions) are consistently small (less than 1), the gradient signal can shrink exponentially as it propagates backward through many layers/time steps.
*   **Effect:** Gradients for earlier layers/time steps become extremely small (vanish), meaning the weights for these layers learn very slowly or not at all. This makes it difficult for the RNN to capture long-range dependencies in the sequence, as the influence of distant past inputs on the current output is lost.
    *   Example: Product of many derivatives of tanh functions (<1) will lead to exponentially small values (~0).

### Exploding Gradient Problem
*   **Cause:** If the weights (or derivatives) are consistently large (greater than 1), the gradient signal can grow exponentially as it propagates backward.
*   **Effect:** Gradients become excessively large, leading to unstable training. The weight updates can be so large that they overshoot the optimal values, causing the model to diverge.
    *   Example: Product of many derivatives of tanh functions (>1) will lead to exponentially large values.

### Solutions and Mitigations

*   **Exploding Gradients:**
    *   **Gradient Clipping:** A common technique where gradients are capped at a predefined threshold if they exceed it. This prevents them from becoming too large.

*   **Vanishing Gradients (more complex to solve):**
    *   **Proper Weight Initialization:** Carefully initializing weights (e.g., Xavier or He initialization) can help maintain a reasonable gradient magnitude.
    *   **Use ReLU Activation Function:** The derivative of ReLU is either 0 or 1, which can help prevent gradients from shrinking as much as sigmoid or tanh.
    *   **Gated Architectures (LSTMs and GRUs):** Long Short-Term Memory (LSTM) and Gated Recurrent Unit (GRU) networks are specifically designed with gating mechanisms to better control the flow of information and gradients, making them more effective at learning long-range dependencies and mitigating the vanishing gradient problem. These are the most common solutions.