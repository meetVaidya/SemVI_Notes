### Markov Assumption
*   If we want to predict the future in the sequence, all that matters is the **current state**.
*   All states before the current state have no impact on the future *except via the current state*.

### Components of a Markov Chain

A Markov chain is specified by the following components:
(Image context: A table defining Markov chain components.)
*   **Q = q1, q2, ..., qN**: A set of N states.
*   **A = a11, a12, ..., aNN**: A transition probability matrix A, where each `aij` represents the probability of moving from state `i` to state `j`.
    *   Constraint: Σ (from j=1 to N) `aij` = 1 for all `i`.
*   **π = π1, π2, ..., πN**: An initial probability distribution over states. `πi` is the probability that the Markov chain will start in state `i`.
    *   Some states `j` may have `πj` = 0, meaning they cannot be initial states.
    *   Constraint: Σ (from i=1 to N) `πi` = 1.

## The Hidden Markov Model (HMM)

*   A Markov chain is useful when we need to compute a probability for a sequence of **observable events**.
*   However, in many cases, the events we are interested in are **hidden** – we don’t observe them directly.
*   **Example**: We don’t normally observe part-of-speech tags in a text. Instead, we see words and must infer the tags from the word sequence. The tags are "hidden" because they are not directly observed.

### HMM Definition

An HMM allows us to model both:
*   **Observed events**: Like words that we see in the input.
*   **Hidden events**: Like part-of-speech tags, which are considered causal factors in the probabilistic model.

### Components of an HMM

An HMM is specified by the following components:
(Image context: A table defining HMM components.)
*   **Q = q1, q2, ..., qN**: A set of N hidden states.
*   **A = a11, a12, ..., aNN**: A transition probability matrix A, where `aij` is the probability of moving from hidden state `i` to hidden state `j`.
    *   P(qt = sj | qt-1 = si)
    *   Constraint: Σ (from j=1 to N) `aij` = 1 for all `i`.
*   **O = o1, o2, ..., oT**: A sequence of T observations, each drawn from a vocabulary V = {v1, v2, ..., vV}.
*   **B = bi(ot)**: A sequence of observation likelihoods, also called **emission probabilities**. `bi(ot)` is the probability of an observation `ot` being generated from hidden state `qi`.
    *   P(ot | qt = si)
*   **π = π1, π2, ..., πN**: An initial probability distribution over hidden states. `πi` is the probability that the Markov chain will start in hidden state `qi`.
    *   Constraint: Σ (from i=1 to N) `πi` = 1.

### First-Order HMM Simplifying Assumptions

A first-order HMM instantiates two simplifying assumptions:

1.  **Markov Assumption (State Transition)**: The probability of a particular hidden state depends *only* on the *previous* hidden state.
    `P(qi | q1, ..., qi-1) = P(qi | qi-1)`

2.  **Output Independence (Emission)**: The probability of an output observation `oi` depends *only* on the hidden state `qi` that produced the observation, and not on any other states or any other observations.
    `P(oi | q1, ..., qT, o1, ..., oT) = P(oi | qi)`