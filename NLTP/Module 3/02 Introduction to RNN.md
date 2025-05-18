Recurrent Neural Networks (RNNs) are a class of neural networks well-suited for processing sequential data, such as natural language, time series, and speech.

## Why RNNs for Sequential Data?
*   **Handling Sequences:** Traditional machine learning models and feedforward networks often struggle with sequential data because they assume inputs are independent and typically require fixed-size inputs.
*   **Sequence Information:** In many NLP tasks (e.g., language modeling, machine translation), the order of words (sequence information) is crucial. Converting text to vectors using methods like Bag-of-Words or TF-IDF can discard this vital sequence information, potentially affecting accuracy.
*   **RNNs Maintain Context:** RNNs are designed to retain information from previous steps in the sequence to inform current and future predictions.

## Core Concepts of RNNs
*   **Recurrent Connection:** The defining feature of an RNN is its recurrent connection, where the output from a previous time step is fed as input to the current time step. This creates a "loop" in the network.
*   **Hidden State (Memory):**
    *   The most important feature of an RNN is its **hidden state (`h_t`)**.
    *   The hidden state acts as the network's memory, summarizing information about the sequence processed so far.
    *   It remembers some information about a sequence, allowing past context to influence current predictions.
*   **Parameter Sharing:** RNNs use the same set of weights (parameters) for each input at every time step. This means the network performs the same task on all inputs or hidden layers to produce the output, making it efficient for variable-length sequences.

## Architecture of an RNN
![[Pasted image 20250518165335.png]]
*   **Notation:**
    *   `x_t`: Input at time step `t`.
    *   `h_t`: Hidden state (current state) at time step `t`.
    *   `h_{t-1}`: Hidden state (previous state) from time step `t-1`.
    *   `y_t`: Output at time step `t`.

### Backpropagation Through Time (BPTT)

BPTT is the algorithm used to train RNNs. It's an extension of standard backpropagation applied to the unrolled network.

*   **Challenge:** The hidden state `h_t` at time `t` influences not only the output `y_t` but also all subsequent hidden states and outputs (`h_{t+1}, y_{t+1}, h_{t+2}, y_{t+2}, ...`). Therefore, the loss at any time step `t` depends on computations from previous time steps.
*   **Two-Pass Algorithm:**
    1.  **Forward Pass:**
        *   Process the input sequence from start to end.
        *   At each time step `t`, compute the hidden state `h_t` and output `y_t`.
        *   Accumulate the loss at each time step.
        *   Save the values of the hidden layers at each step for use in the backward pass.
    2.  **Backward Pass:**
        *   Process the sequence in reverse (from end to start).
        *   Compute the required gradients for weights `W`, `U`, and `V` by propagating the error backward through time.
        *   The error at `h_t` depends on its influence on the current output and all future outputs it affected.

This general approach is commonly referred to as Backpropagation Through Time.