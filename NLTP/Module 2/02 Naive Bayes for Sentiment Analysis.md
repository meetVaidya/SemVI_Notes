## Worked Sentiment Example (Multinomial Naive Bayes)

Let's classify a test sentence for sentiment (e.g., positive `+` or negative `-`).

**Assumed Training Data Summary (for this example):**
*   Vocabulary `V` has been extracted.
*   Priors and Likelihoods have been pre-calculated with Add-1 smoothing.

**Step 1: Priors from Training**
Suppose our training data yielded:
*   `P(-) = 3/5`
*   `P(+) = 2/5`

**Step 2: Preprocessing the Test Document**
Test sentence: "predictable with no fun"
*   Assume "with" is an unknown word (not in training vocabulary). We drop it.
*   Processed test words: "predictable", "no", "fun".

**Step 3: Likelihoods from Training (Illustrative Values)**
Suppose these are the (log) likelihoods `log P(word|class)` from training (after Add-1 smoothing):

| Word        | `log P(word \| + )` | `log P(word \| - )` |
| :---------- | :------------------ | :------------------ |
| predictable | -2.5                | -1.0                |
| no          | -3.0                | -0.5                |
| fun         | -1.5                | -2.0                |
| ...         | ...                 | ...                 |

**Step 4: Scoring the Test Set**
We use the log-probability formula:
`score(class) = log P(class) + Σ_{word ∈ test_doc} log P(word|class)`

*   **Score for Positive (+):**
    `log P(+) = log(2/5) ≈ -0.916`
    `score(+) = log P(+) + log P("predictable"|+) + log P("no"|+) + log P("fun"|+)`
    `score(+) = -0.916 + (-2.5) + (-3.0) + (-1.5) = -7.916`

*   **Score for Negative (-):**
    `log P(-) = log(3/5) ≈ -0.511`
    `score(-) = log P(-) + log P("predictable"|-) + log P("no"|-) + log P("fun"|-)`
    `score(-) = -0.511 + (-1.0) + (-0.5) + (-2.0) = -4.011`

**Decision:**
Since `score(-) > score(+)` (`-4.011 > -7.916`), the classifier predicts **Negative (-)**.

## Optimizing for Sentiment Analysis: Binary Naive Bayes

For tasks like sentiment analysis, **word occurrence** often seems more important than **word frequency**.
*   The fact that "fantastic" appears tells us a lot.
*   The fact that it occurs 5 times might not add much more information than it occurring once.

This leads to **Binary Multinomial Naive Bayes** (also called **Binary NB** or Binarized Naive Bayes).
*   **Key Idea:** Clip word counts at 1 for each document. We only care if a word occurs in a document, not how many times.
*   *Note: This is different from Bernoulli Naive Bayes, which models the presence/absence of all words in the vocabulary for a document.*

### Learning for Binary Multinomial Naive Bayes

1.  **From training corpus, extract Vocabulary `V`**.
2.  **Calculate Prior `P(c_j)` terms** (same as standard Multinomial NB).
3.  **Calculate Likelihood `P(w_k|c_j)` terms:**
    *   For each class `c_j` in `C`:
        *   `docs_j ←` all documents in the training set with class `c_j`.
        *   **Modify `docs_j`**: For each document in `docs_j`, remove duplicate word occurrences (i.e., ensure each word type appears at most once per document).
        *   `Text_j ←` a single "mega-document" created by concatenating these modified (binarized) documents in `docs_j`.
        *   For each word `w_k` in Vocabulary `V`:
            *   `n_k ←` number of occurrences of `w_k` in `Text_j` (this `n_k` now effectively counts how many documents in class `c_j` contain `w_k` at least once).
            *   `P̂(w_k|c_j) = (n_k + 1) / (total_words_in_Text_j + |V|)` (using Add-1 smoothing).
            (Note: `total_words_in_Text_j` will be the sum of unique words across all documents in class `c_j`).

### Binary Multinomial Naive Bayes on a Test Document `d`

1.  **First, remove all duplicate words from the test document `d`**. (Make it a set of unique words).
2.  Then, compute the Naive Bayes score using the same equation as Multinomial NB, but with the binarized test document and the likelihoods learned from binarized training data.

`c_NB = argmax_{c ∈ C} [log P(c) + Σ_{word ∈ unique_words_in_d} log P(word|c)]`

**Example (Binary NB):**
Test sentence: "good good good bad"
Binarized test sentence: "good bad"

Priors: `P(+) = 0.5`, `P(-) = 0.5` => `log P(+) = -0.69`, `log P(-) = -0.69`
Likelihoods (illustrative, learned from binarized data):
`log P(good|+) = -0.7`
`log P(bad|+)  = -2.0`
`log P(good|-) = -1.5`
`log P(bad|-)  = -0.6`

`score(+) = -0.69 + (-0.7) + (-2.0) = -3.39`
`score(-) = -0.69 + (-1.5) + (-0.6) = -2.79`

Decision: Negative, as `-2.79 > -3.39`.

## Sentiment Classification: Dealing with Negation

Negation significantly impacts sentiment.
*   "I really **like** this movie." (Positive)
*   "I really **don't like** this movie." (Negative, "like" is negated)

Negation can also change negative words to positive-ish:
*   "**Don't** dismiss this film." (Suggests the film is good)
*   "**Doesn't** let us get bored." (Suggests engaging)

### How to Handle Negation?

Two main components:
1.  **Detect the scope of negation:** Identify which part of the sentence is affected by the negation word (e.g., "not", "don't").
2.  **Resolve negation:** Update the sentiment of the language within the scope of negation.

### Simple Baseline Method for Handling Negation

A common baseline approach (Pang et al., 2002; Das & Chen, 2001):
*   **Add a `NOT_` prefix to every word between a negation word (e.g., "not", "n't", "no") and the next punctuation mark.**

**Example:**
*   Original: `didn’t like this movie , but I`
*   With NOT_ prefix: `didn’t NOT_like NOT_this NOT_movie , but I`

The words `NOT_like`, `NOT_this`, `NOT_movie` would then be treated as distinct features in the vocabulary, and the model would learn their sentiment (e.g., `NOT_like` would likely be associated with negative sentiment).
This implies that if "good" has a positive score, "NOT_good" (or the effect of "not" on "good") would have a negative score.