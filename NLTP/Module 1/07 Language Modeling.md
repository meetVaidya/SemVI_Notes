## What is a Language Model?
*   **Purpose:** To find the probability of statements, words, or characters. A language model provides a way to compute these probabilities.
## Probabilistic Language Models
*   **Goal:** Assign a probability to a sentence or sequence of words.
    *   `P(W) = P(w₁, w₂, w₃, w₄, w₅…wₙ)`  (Joint Probability of a sequence of words)
*   **Function:** It is a probability distribution over word sequences.
*   **Prediction:** Models that assign a probability to each possible next word.
    *   `P(w₅ | w₁, w₂, w₃, w₄)` (Conditional Probability of an upcoming word given previous words)
*   **Outcome:** Such a model can predict that one sequence of words is much more likely to appear in a text than another.
*   **A model that computes either P(W) or P(wₙ | w₁, w₂…wₙ₋₁) is called a language model (LM).**
    *   While "grammar" might seem like a more intuitive term, "language model" or "LM" is the standard terminology.
## [[08 N-Gram Model|N-Gram Model]]

*   **Definition:** The simplest model that assigns probabilities to sentences and sequences of words.
*   **An n-gram is a sequence of n words:**
    *   **1-gram (Unigram):** A single word.
    *   **2-gram (Bigram):** A two-word sequence (e.g., "please turn", "turn your", "your homework").
    *   **3-gram (Trigram):** A three-word sequence (e.g., "please turn your", "turn your homework").