## Generalization and Zeros
*   **N-gram Model Dependency:** N-gram models, like many statistical models, are highly dependent on the training corpus. Probabilities often encode specific facts about that corpus.
*   **Test vs. Training Corpus:** N-grams work well for word prediction if the test corpus looks very similar to the training corpus. In real life, this is often not the case.
*   **Need for Robust Models:** We need to train robust models that **generalize** well to unseen data.
*   **The Problem of Zeros:**
    *   A critical aspect of generalization is handling **zeros**: N-grams (sequences of words) that don't ever occur in the training set but appear in the test set.
    *   If any N-gram in a test sentence has a probability of 0 (due to MLE on training data), the entire probability of the sentence becomes 0.
    *   This also leads to underestimating the probability of many other plausible (but unseen) N-grams.

## Unknown Words (`<UNK>`)
*   **Issue:** Language models must deal with words encountered in the test data that were not present in the training vocabulary (Out-Of-Vocabulary or OOV words). These are **unknown words**.
*   **Solution: Pseudo-word `<UNK>`**
    *   Model potential unknown words by adding a special pseudo-word token, `<UNK>`, to the training vocabulary.
*   **Handling Unknown Words in Training:**
    1.  **Frequency-based replacement:** Replace words in the training data with `<UNK>` if they occur fewer than `n` times (where `n` is a small threshold).
    2.  **Fixed vocabulary:**
        *   Select a vocabulary of size `V` in advance (e.g., the 50,000 most frequent words).
        *   Replace all other words in the training data (and test data) with `<UNK>`.
    3.  Train the language model as usual, treating `<UNK>` like any other regular word. This allows the model to learn probabilities for `<UNK>` (e.g., `P(<UNK> | preceding_word)`).

## Smoothing (Discounting)
*   **Goal:** To prevent zero probabilities for unseen events and improve generalization.
*   **Method:** "Shave off" a bit of probability mass from more frequent (seen) events and redistribute it to infrequent or never-seen events.
*   **Alternative Term:** Discounting.
*   **Common Techniques:**
    *   **Add-1 Smoothing (Laplace Smoothing)**
    *   **Add-k Smoothing**
    *   Good-Turing Discounting
    *   Kneser-Ney Smoothing (more advanced)

### 1. Laplace Smoothing (Add-1 Smoothing)
*   **Concept:** The simplest way to do smoothing. Add one to all N-gram counts before normalizing them into probabilities.
*   **Effect:**
    *   Counts that were zero now become 1.
    *   Counts that were 1 become 2, and so on.
    *   It's like pretending we saw each N-gram one more time than we actually did.

*   **Laplace Smoothing for Unigrams:**
    *   Unsmoothed MLE: `P(wᵢ) = cᵢ / N`
        (where `cᵢ` is the count of word `wᵢ`, `N` is the total number of word tokens)
    *   Smoothed: `P_Laplace(wᵢ) = (cᵢ + 1) / (N + V)`
        (where `V` is the vocabulary size – the number of unique word types. We add `V` to the denominator because we added 1 to the count of each of the `V` word types.)

*   **Laplace Smoothing for Bigrams:**
    *   Unsmoothed MLE: `P(wₙ | wₙ₋₁) = C(wₙ₋₁ wₙ) / C(wₙ₋₁)`
    *   Smoothed: `P*_Laplace(wₙ | wₙ₋₁) = (C(wₙ₋₁ wₙ) + 1) / (C(wₙ₋₁) + V)`
        (where `V` is the vocabulary size. We add `V` to the denominator because there are `V` possible words `wₙ` that could follow `wₙ₋₁`, and we've added 1 to each of those `V` bigram counts `C(wₙ₋₁ w_any)`).
*   **Adjusted Counts (Effective Counts) for Laplace Smoothing:**
    The smoothed probability `P* = (C+1)/(N+V)` can be thought of as using an adjusted count `c* = (C+1) * N / (N+V)`.
*   **Drawback of Add-1 Smoothing:**
    Add-1 smoothing can significantly alter the probabilities, especially for frequent N-grams. It often "steals" too much probability mass from observed events to give to unobserved ones. For large vocabularies, it can assign too much total probability mass to unseen events.

### 2. Add-k Smoothing (Lidstone Smoothing)
*   **Motivation:** Add-1 smoothing makes a very big change to the counts (e.g., `C(want to)` changed from 608 to an effective count of 238). `P(to|want)` decreases from .66 (unsmoothed) to .26 (smoothed). This is because too much probability mass is moved to all the zeros.
    *   The discount `d` (how much counts for a prefix word have been reduced) for the bigram `want to` is .39, while for `Chinese food` it is .10, a factor of 10.
*   **Concept:** One alternative to add-one smoothing is to move a bit less of the probability mass from the seen to the unseen events. Instead of adding 1 to each count, add a smaller fractional count `k` (e.g., `k=0.5`, `k=0.05`, `k=0.01`).
*   **Formula for Bigrams:**
    `P*_Add-k(wₙ | wₙ₋₁) = (C(wₙ₋₁ wₙ) + k) / (C(wₙ₋₁) + kV)`
    Where:
    *   `k` is the smoothing parameter (a positive fractional value, typically < 1).
    *   `V` is the vocabulary size.