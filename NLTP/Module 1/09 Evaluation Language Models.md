### Training and Test Sets
*   We train the parameters of our model on a **training set**.
*   We test the model's performance on data it hasn't seen before, called a **test set** (or held-out set).
    *   A test set is an unseen dataset that is different from our training set, totally unused during training.
*   An **evaluation metric** tells us how well our model performs on the test set.

## Types of Evaluation
There are two main types of evaluation for language models:
### 1. Extrinsic Evaluation
*   **Definition:** Extrinsic evaluation of an N-gram language model involves using it in a downstream application and measuring how much the application improves.
*   **Process to compare two language models (A and B):**
    1.  Integrate each language model (A and B separately) into a task-specific application (e.g., spelling corrector, Machine Translation (MT) system, speech recognizer).
    2.  Measure the performance (accuracy) of the application with model A and with model B.
        *   Examples:
            *   Spelling corrector: How many misspelled words were corrected properly?
            *   MT system: How many words were translated correctly? (e.g., BLEU score)
    3.  Compare the accuracies. The model that results in better application performance is considered the better language model for that task.
*   **Drawback:** Extrinsic evaluation can be **time-consuming** as it requires running full application experiments.

### 2. Intrinsic Evaluation
*   **Definition:** An intrinsic evaluation metric measures the quality of a model independent of any specific application. It directly assesses how well the model fits the data.
*   **Process to compare two different N-gram models:**
    1.  Divide the available corpus into a **training set** and a **test set**.
    2.  Train the parameters of both models on the training set.
    3.  Compare how well the two trained models "fit" the test set.
        *   The model that assigns a **higher probability** to the test set is considered better.
*   **Perplexity:** In practice, instead of using raw probability, a probability-based metric called **perplexity** is commonly used for intrinsic evaluation of language models.

## Perplexity
*   **Concept:** The best language model is one that best predicts an unseen test set, meaning it gives the highest probability `P(testset)`.
*   **Definition:** The perplexity (PP) of a language model on a test set is the **inverse probability of the test set, normalized by the number of words.**
    `PP(W) = P(w₁w₂...wₙ)^(-1/N)`
    Where `W = w₁w₂...wₙ` is the test set and `N` is the number of words in the test set.
*   This can also be written using the 2nd root:
    `PP(W) = N√(1 / P(w₁w₂...wₙ))`
*   **Relationship to Probability:** Minimizing perplexity is the same as maximizing the test set probability.
*   **Using Chain Rule:**
    `P(w₁w₂...wₙ) = Π P(wᵢ | w₁...wᵢ₋₁)` for i=1 to N
    So, `PP(W) = N√(1 / Π P(wᵢ | w₁...wᵢ₋₁))`
    Or, using log probability for easier computation:
    `PP(W) = exp(-1/N * Σ log P(wᵢ | w₁...wᵢ₋₁))`
    `PP(W) = 2^(-1/N * Σ log₂ P(wᵢ | w₁...wᵢ₋₁))` (if using log base 2)

*   **Perplexity for Bigrams (approximation):**
    If using a bigram model, `P(wᵢ | w₁...wᵢ₋₁) ≈ P(wᵢ | wᵢ₋₁)`.
    `PP(W) = N√(1 / Π P(wᵢ | wᵢ₋₁))` for i=1 to N

### Perplexity as Branching Factor
*   Perplexity can be intuitively understood as the **weighted average branching factor** of a language.
*   The branching factor is the number of possible next words that can follow any given word.
*   **Example:**
    *   Consider a sentence consisting of random digits (0-9).
    *   A model assigns `P = 1/10` to each digit.
    *   `PP(W) = ((1/10) * (1/10) * ... * (1/10)) ^ (-1/N)` (N times)
    *   `PP(W) = ((1/10)ᴺ) ^ (-1/N)`
    *   `PP(W) = (1/10) ^ (-1) = 10`
    *   The perplexity is 10, which is the number of choices for each position.

### Interpreting Perplexity
*   **Lower perplexity = better model.** A lower perplexity indicates that the language model is less "surprised" by the test set, meaning it assigns higher probabilities to the observed sequences.