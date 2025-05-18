Gated Recurrent Units (GRUs) are another type of gated RNN, similar to LSTMs, designed to handle sequential data and mitigate issues like the vanishing gradient problem. They were introduced by Cho et al. in 2014.

## Introduction to GRU

*   **Newer Generation RNNs:** GRUs are a more recent development compared to LSTMs.
*   **Simplified Architecture:** GRUs have a simpler architecture than LSTMs. They notably **do not have a separate cell state ($C_t$)** like LSTMs. Instead, they use only the hidden state ($h_t$) to transfer information.
*   **Fewer Gates:** GRUs have two gates: a Reset Gate and an Update Gate, compared to LSTM's three gates (Forget, Input, Output).
*   **Performance:**
    *   Often slightly faster to train than LSTMs due to fewer parameters and operations.
    *   Performance is generally comparable to LSTMs, and the choice between GRU and LSTM can depend on the specific dataset and task. Neither is universally superior.
### Key Gates in GRU
*   **Update Gate ($z_t$):**
    *   Decides how much of the past information (previous hidden state $h_{t-1}$) should be kept and how much of the new candidate information ($h̃_t$) should be added.
    *   Analogous to a combination of the forget and input gates in an LSTM. It determines what to throw away from $h_{t-1}$ and what new information to add from $h̃_t$.
*   **Reset Gate ($r_t$):**
    *   Decides how much of the past information ($h_{t-1}$) to forget when computing the candidate hidden state $h̃_t$.
    *   Allows the model to drop information that is irrelevant for the future.

## GRU: Mathematical Explanation and Diagram Components

A GRU cell consists of:
*   **Reset Gate ($r_t$):** Typically a sigmoid layer.
*   **Update Gate ($z_t$):** Typically a sigmoid layer.
*   **Candidate Hidden State ($h̃_t$):** Typically involves a tanh layer.
*   **New (Final) Hidden State ($h_t$):** The output of the GRU cell for the current time step.

### 1. Reset Gate ($r_t$)
*   **Purpose:** Controls how much of the past hidden state ($h_{t-1}$) should be "forgotten" or ignored before computing the candidate hidden state ($h̃_t$). It essentially decides how relevant the previous context is for generating the new candidate information.
*   **Computation:** $r_t = σ(W_r * x_t + U_r * h_{t-1} + b_r)$
    *   $W_r, U_r, b_r$ are learnable weight matrices and bias vector for the reset gate.
    *   $σ$ is the sigmoid activation function.
*   **Effect:**
    *   If $r_t$ is close to 0 (element-wise), the corresponding parts of $h_{t-1}$ are mostly ignored when computing $h̃_t$. The candidate state relies more on the current input $x_t$.
    *   If $r_t$ is close to 1, the corresponding parts of $h_{t-1}$ are preserved and significantly influence $h̃_t$.
*   **Example:** If $r_t = [0.42, 0.55]^T$, for the first hidden unit, about 42% of the previous hidden state is used in computing $h̃_t$ (58% ignored). For the second unit, 55% is used (45% ignored).
### 2. Candidate Hidden State ($h̃_t$)
*   **Purpose:** Computes a potential update for the hidden state. This is the "new" information that could be incorporated.
*   **Computation:** $h̃_t = tanh(W_h * x_t + U_h * (r_t ⊙ h_{t-1}) + b_h)$
    *   $W_h, U_h, b_h$ are learnable weight matrices and bias vector.
    *   $⊙$ denotes element-wise (Hadamard) product. The reset gate $r_t$ scales $h_{t-1}$.
    *   $tanh$ is the hyperbolic tangent activation function.
*   **Effect:** $h̃_t$ represents the new memory content, computed based on the current input $x_t$ and the *reset-filtered* previous hidden state $r_t ⊙ h_{t-1}$.

### 3. Update Gate ($z_t$)
*   **Purpose:** Controls how much of the previous hidden state $h_{t-1}$ should be kept and how much of the newly computed candidate hidden state $h̃_t$ should be used to form the final $h_t$. It acts like a gatekeeper deciding the balance between old and new information.
*   **Computation:** $z_t = σ(W_z * x_t + U_z * h_{t-1} + b_z)$
    *   $W_z, U_z, b_z$ are learnable weight matrices and bias vector for the update gate.
*   **Effect:** $z_t$ values (between 0 and 1) determine the proportion of $h̃_t$ to include.
### 4. Final Hidden State ($h_t$)
*   **Purpose:** Computes the new hidden state for the current time step $t$ as a mix (interpolation) of the previous hidden state $h_{t-1}$ and the candidate state $h̃_t$.
*   **Computation:** $h_t = (1 - z_t) ⊙ h_{t-1} + z_t ⊙ h̃_t$
*   **Understanding $(1 - z_t)$ and $z_t$:**
    *   $z_t$ controls how much of the **new memory** ($h̃_t$) is retained/incorporated.
    *   $(1 - z_t)$ controls how much of the **old memory** ($h_{t-1}$) is kept/preserved.
    *   If $z_t$ is close to 1, $h_t$ is mostly $h̃_t$ (network updates knowledge rapidly).
    *   If $z_t$ is close to 0, $h_t$ is mostly $h_{t-1}$ (network relies on past memory, preventing unnecessary updates).
*   This mechanism makes GRUs effective at handling long-term dependencies.

### Summary of GRU Equations (Alternative Formulation)
Sometimes, the equations are presented with concatenated inputs:
*   $r_t = σ(W_r * [h_{t-1}, x_t] + b_r)$
*   $z_t = σ(W_z * [h_{t-1}, x_t] + b_z)$
*   $h̃_t = tanh(W_h * [r_t ⊙ h_{t-1}, x_t] + b_h)$ (Note: $x_t$ is combined *after* $h_{t-1}$ is reset)
*   $h_t = (1 - z_t) ⊙ h_{t-1} + z_t ⊙ h̃_t$

### Working of a GRU (Step-by-Step from another perspective)
1.  Take current input $x_t$ and previous hidden state $h_{t-1}$ as vectors.
2.  Calculate $r_t$ and $z_t$ using their respective weights and sigmoid activation.
3.  Calculate $h̃_t$ (Current Memory Gate / Candidate Hidden State) using its weights, $x_t$, and the reset $h_{t-1}$ (i.e., $r_t ⊙ h_{t-1}$), followed by tanh activation.
4.  Calculate $h_t$ by interpolating between $h_{t-1}$ and $h̃_t$ using the update gate $z_t$.

### Training GRUs
The training process for a GRU network is similar to that of a basic RNN or LSTM, typically using Backpropagation Through Time (BPTT).

### GRU vs. LSTM Comparison

| Feature        | LSTM                           | GRU                                          |
| :------------- | :----------------------------- | :------------------------------------------- |
| Gates          | 3: Input, Output, Forget       | 2: Reset, Update                             |
| Cell State     | Separate cell state ($C_t$)    | No separate cell state (uses $h_t$ only)     |
| Complexity     | More complex, more parameters  | Simpler, fewer parameters                    |
| Efficiency     | Less computationally efficient | More computationally efficient               |
| Popularity     | Widely used, established       | Gaining popularity, often performs similarly |
| Invention Year | 1995-1997                      | 2014                                         |
### Example Scenario for GRU
*   When processing "Dhaval eats samosa...", the hidden state $h_t$ accumulates information about Indian cuisine.
*   When "His brother Bhavin... pasta and cheese" appears:
    *   The **reset gate ($r_t$)** might activate to "forget" or reduce the influence of the "samosa/Indian" context when calculating the candidate hidden state for "pasta".
    *   The **update gate ($z_t$)** would then allow the new information related to "pasta/Italian" (from $h̃_t$) to largely form the new hidden state $h_t$, effectively updating the context.