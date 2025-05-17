## Challenges in Estimating Probabilities
*   **Can we just count and divide for entire sentences?**
    *   **No!** The number of possible sentences is too vast.
    *   We'll likely never see enough data to estimate probabilities for most full sentences directly.
*   **Using a large corpus (e.g., the web):**
    *   While helpful, even the web isn't big enough to provide good estimates for all possible sequences due to the creative nature of language.
    *   New sentences are created constantly, and many plausible sentences will have zero counts even in very large corpora.
    *   Example: "Walden Pond’s water is so transparent that the..." – even simple extensions might have zero counts.

## The Chain Rule of Probability
To compute the joint probability of a sequence of words `P(W)`, we use the Chain Rule of Probability.

*   **Recall Conditional Probability:**
    `P(B|A) = P(A,B) / P(A)`
    Rewriting: `P(A,B) = P(A)P(B|A)`
*   **For more variables:**
    `P(A,B,C,D) = P(A)P(B|A)P(C|A,B)P(D|A,B,C)`
*   **Chain Rule in General:**
    `P(x₁, x₂, x₃, …, xₙ) = P(x₁)P(x₂|x₁)P(x₃|x₁,x₂) … P(xₙ|x₁, …, xₙ₋₁)`

*   **Applied to a sentence (e.g., "its water is so transparent"):**
    `P(“its water is so transparent”) = P(its) × P(water|its) × P(is|its water) × P(so|its water is) × P(transparent|its water is so)`

The Chain Rule links the joint probability of an entire sequence to the product of several conditional probabilities (probability of a word given previous words).

## The N-gram Model Approximation (Markov Assumption)

The core idea of the N-gram model is to approximate the history (all preceding words) by only considering the last few words.

* Instead of computing `P(wₙ | w₁, w₂, …, wₙ₋₁)` (probability of a word given its *entire* history), we approximate it.
*   **Bigram Model (N=2):** Approximates the probability of a word given all previous words by using only the conditional probability of the *preceding one word*.
    `P(wₙ | w₁, …, wₙ₋₁) ≈ P(wₙ | wₙ₋₁)`
    *   **Example:** Instead of `P(the | Walden Pond’s water is so transparent that)`, we approximate with `P(the | that)`.
*   **Markov Assumption:** The assumption that the probability of a word depends only on a limited number of previous words (e.g., one previous word for bigrams, two for trigrams) is called a Markov assumption.
*   This simplifies the problem by approximating each conditional probability component in the Chain Rule product.

## Estimating N-gram Probabilities: Maximum Likelihood Estimate (MLE)

How do we estimate `P(wₙ | wₙ₋₁)` (for bigrams) or `P(wₙ | wₙ₋₂, wₙ₋₁)` (for trigrams)?
The standard method is Maximum Likelihood Estimation (MLE), which involves using counts from a corpus.

*   **For a bigram `P(wᵢ | wᵢ₋₁)`:**
    `P(wᵢ | wᵢ₋₁) = Count(wᵢ₋₁ wᵢ) / Count(wᵢ₋₁)`
    Where:
    *   `Count(wᵢ₋₁ wᵢ)` is the number of times the bigram (sequence of two words) `wᵢ₋₁ wᵢ` appears in the corpus.
    *   `Count(wᵢ₋₁)` is the number of times the unigram `wᵢ₋₁` appears in the corpus.

## N-gram Formulas

Let `P(w₁ⁿ)` denote `P(w₁, w₂, ..., wₙ)`.

*   **Unigrams:**
    `P(w₁ⁿ) ≈ Π P(wₖ)` for k=1 to n
    (Assumes words are independent)
*   **Bigrams:**
    `P(w₁ⁿ) ≈ Π P(wₖ | wₖ₋₁)` for k=1 to n (where `w₀` is a start-of-sentence marker like `<s>`)
*   **Trigrams:**
    `P(w₁ⁿ) ≈ Π P(wₖ | wₖ₋₂ wₖ₋₁)` for k=1 to n (where `w₋₁`, `w₀` are start-of-sentence markers)
*   **Quadrigrams (4-grams):**
    `P(w₁ⁿ) ≈ Π P(wₖ | wₖ₋₃ wₖ₋₂ wₖ₋₁)` for k=1 to n

## N-Gram Examples (Sentence Probability)

Sentence: "the man from jupiter" (assuming `<s>` start and `</s>` end markers for full sentence probability)

*   **Unigram:**
    `P(<s> the man from jupiter </s>) ≈ P(<s>)P(the)P(man)P(from)P(jupiter)P(</s>)`
*   **Bigram:**
    `P(<s> the man from jupiter </s>) ≈ P(the|<s>)P(man|the)P(from|man)P(jupiter|from)P(</s>|jupiter)`
*   **Trigram:**
    `P(<s> the man from jupiter </s>) ≈ P(the|<s><s>)P(man|<s>the)P(from|the man)P(jupiter|man from)P(</s>|from jupiter)`

## Simple Corpus Example
**Corpus:**
1.  `<s> I am Sam </s>`
2.  `<s> Sam I am </s>`
3.  `<s> I do not like green eggs and ham </s>`

**Example Bigram Probabilities (MLE):**
*   `P(I | <s>) = Count(<s> I) / Count(<s>) = 2 / 3 = 0.67`
*   `P(Sam | <s>) = Count(<s> Sam) / Count(<s>) = 1 / 3 = 0.33`
*   `P(am | I) = Count(I am) / Count(I) = 2 / 3 = 0.67` (Count(I) = 3: "I am", "I am", "I do")
*   `P(</s> | Sam) = Count(Sam </s>) / Count(Sam) = 1 / 2 = 0.5` (Count(Sam) = 2: "Sam </s>", "Sam I")
*   `P(Sam | am) = Count(am Sam) / Count(am) = 1 / 2 = 0.5` (Count(am) = 2: "am Sam", "am </s>")
*   `P(do | I) = Count(I do) / Count(I) = 1 / 3 = 0.33`