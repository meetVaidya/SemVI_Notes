## Generative vs. Discriminative Classifiers

Classifiers can be broadly categorized into generative and discriminative types.

*   **Naive Bayes** is a **generative** classifier.
*   **Logistic Regression** is a **discriminative** classifier.

| Feature               | Generative Classifiers                                                                                                                                                                                                            | Discriminative Classifiers                                                                                                                                    |
| :-------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Models**            | The joint probability distribution `P(X,Y)`, where X is input data and Y is the class label.                                                                                                                                      | The conditional probability `P(Y \| X)` directly                                                                                                              |
| **Mechanism**         | Models how the data was generated. For example, to distinguish cats and dogs, it would build a model of what a cat looks like (whiskers, ears, eyes) and a separate model for dogs, then see which model better fits a new image. | Focuses on the boundary between classes rather than modeling data generation. It learns what features distinguish dogs from cats (e.g., "dogs have collars"). |
| **Example Algorithm** | **Naive Bayes:** Assumes features are conditionally independent given the class label.                                                                                                                                            | **Logistic Regression:** Models the probability of the class label directly as a function of input features.                                                  |
| **Data Generation**   | Explicitly models how data is generated.                                                                                                                                                                                          | Does not model how data is generated; directly maps input X to output Y.                                                                                      |

## Naive Bayes Intuition

*   A simple ("naive") classification method based on **Bayes' rule**.
*   Relies on a very simple representation of the document: the **Bag of Words**.

### The Bag of Words (BoW) Representation

*   Represents text by an unordered collection (a "bag") of its words, disregarding grammar and even word order but keeping multiplicity.
*   Each document is typically represented as a vector of word counts or frequencies.
    *(Image context: A diagram showing a document (represented by a document icon) being processed by a function γ, which outputs a feature vector (table with words like "seen", "sweet", "whimsical" and their counts) that is then classified into a class 'c' (thumbs up/down icons indicating positive/negative class).)*

## Bayes' Rule Applied to Documents and Classes

For a document `d` and a class `c`, Bayes' rule states:
`P(c|d) = (P(d|c) * P(c)) / P(d)`
Where:
*   `P(c|d)`: Posterior probability of class `c` given document `d`.
*   `P(d|c)`: Likelihood of document `d` given class `c`.
*   `P(c)`: Prior probability of class `c`.
*   `P(d)`: Probability of document `d` (evidence).

## Naive Bayes Classifier Steps

1.  **Goal:** Find the most probable class `c_MAP` (Maximum A Posteriori) for a given document `d`.
    `c_MAP = argmax_{c ∈ C} P(c|d)`

2.  **Apply Bayes' Rule:**
    `c_MAP = argmax_{c ∈ C} (P(d|c) * P(c)) / P(d)`

3.  **Drop the Denominator `P(d)`:** Since `P(d)` is constant for all classes for a given document, it doesn't affect the argmax.
    `c_MAP = argmax_{c ∈ C} P(d|c) * P(c)`

4.  **Represent Document `d` as Features:** Let `d` be represented by a set of features `x₁, x₂, ..., xn` (e.g., words in the document).
    `c_MAP = argmax_{c ∈ C} P(x₁, x₂, ..., xn | c) * P(c)`
    *   `P(x₁, x₂, ..., xn | c)` is the **likelihood**.
    *   `P(c)` is the **prior**.

    *Note: Without assumptions, estimating `P(x₁, x₂, ..., xn | c)` directly requires a huge number of parameters (O(|X|^n * |C|)), making it impractical.*

5.  **Apply Naive Bayes Independence Assumptions:**
    *   **Bag of Words Assumption:** The position of words doesn't matter.
    *   **Conditional Independence Assumption:** The feature probabilities `P(xi|c)` are independent of each other, given the class `c`.
        This simplifies the likelihood term:
        `P(x₁, x₂, ..., xn | c) = P(x₁|c) * P(x₂|c) * ... * P(xn|c) = Π_{i} P(xi|c)`

6.  **Final Naive Bayes Classifier Formula (Multinomial Naive Bayes):**
    `c_NB = argmax_{c ∈ C} P(c) * Π_{i ∈ positions} P(x_i|c)`
    Where `positions` refers to all word positions in the test document.

## Working in Log Space

Multiplying many small probabilities (e.g., `0.0006 * 0.0007 * ...`) can lead to floating-point underflow.
*   **Solution:** Use logarithms, because `log(ab) = log(a) + log(b)`.
    We sum logs of probabilities instead of multiplying probabilities.

`c_NB = argmax_{c ∈ C} [log P(c) + Σ_{i ∈ positions} log P(x_i|c)]`

*   **Notes:**
    1.  Taking the log doesn't change the ranking of classes (the class with the highest probability also has the highest log probability).
    2.  Naive Bayes is a **linear classifier** because the decision is based on a sum of weighted inputs (log probabilities act as weights).

## Parameter Estimation (Learning the Model)

We need to estimate two sets of parameters from the training data:
1.  **Priors `P(c)`:** The probability of each class.
    `P̂(cj) = N_cj / N_total`
    Where `N_cj` is the number of documents in class `cj`, and `N_total` is the total number of documents.

2.  **Likelihoods `P(w_k|c_j)`:** The probability of word `w_k` occurring given class `cj`.
    *   **Maximum Likelihood Estimate (MLE) - First attempt:**
        `P̂(w_k|c_j) = count(w_k, c_j) / Σ_{w'} count(w', c_j)`
        Where `count(w_k, c_j)` is the total count of word `w_k` in all documents belonging to class `c_j`. This is often calculated by creating a "mega-document" for each class `c_j` by concatenating all documents in that class, and then using word frequencies from this mega-document.

### Problem with Maximum Likelihood Estimates (MLE)

*   If a word `w_k` (e.g., "fantastic") has not been seen in any training document of a particular class (e.g., positive), then `count(w_k, positive) = 0`.
*   This leads to `P̂(w_k|positive) = 0`.
*   A zero probability for any word in the test document will make the entire product `Π P(x_i|c)` zero for that class, regardless of other evidence.

### Laplace (Add-1) Smoothing

To solve the zero probability problem, we use smoothing. Add-1 smoothing is a common technique:
`P̂(w_k|c_j) = (count(w_k, c_j) + 1) / (Σ_{w'} count(w', c_j) + |V|)`
Where:
*   `|V|` is the size of the vocabulary (total number of unique words in the training set).
*   We add 1 to each word count in the numerator.
*   We add `|V|` to the denominator (effectively adding 1 for each word type in the vocabulary).

## Learning Algorithm for Multinomial Naïve Bayes

1.  **From training corpus, extract Vocabulary `V`** (all unique words).
2.  **Calculate Prior `P(c_j)` terms:**
    *   For each class `c_j` in `C`:
        *   `docs_j ←` all documents in the training set with class `c_j`.
        *   `P̂(c_j) = |docs_j| / N_total_docs`.
3.  **Calculate Likelihood `P(w_k|c_j)` terms (with Add-1 smoothing):**
    *   For each class `c_j` in `C`:
        *   `Text_j ←` a single "mega-document" created by concatenating all documents in `docs_j`.
        *   For each word `w_k` in Vocabulary `V`:
            *   `n_k ←` number of occurrences of `w_k` in `Text_j`.
            *   `P̂(w_k|c_j) = (n_k + 1) / (total_words_in_Text_j + |V|)`.

## Handling Unknown Words (at Test Time)

*   **Problem:** Words appear in the test data that were not in the training data (and thus not in the vocabulary `V`).
*   **Solution:** **Ignore them.**
    *   Remove these unknown words from the test document before classification.
    *   Pretend they weren't there; don't include any probability for them.
*   **Why not build an "unknown word" model?** It generally doesn't help, as knowing which class has more unknown words is not usually informative.

## Stop Words

*   **Stop words:** Very frequent words like "the", "a", "is".
*   Some systems ignore stop words:
    *   Sort vocabulary by word frequency in the training set.
    *   Identify the top N (e.g., 10 or 50) words as the stopword list.
    *   Remove these stop words from both training and test sets.
*   **Effectiveness:** Removing stop words **doesn't usually help** for Naive Bayes classification.
*   **Practice:** Most Naive Bayes algorithms use all words and **do not** use stopword lists.

## Example Problem

Consider the following dataset:

| Set          | Document ID | Keywords in the document | Class h |
| :----------- | :---------- | :----------------------- | :------ |
| Training Set | 1           | Love Happy Joy Joy Happy | Yes     |
| Training Set | 2           | Happy Love Kick Joy Happy| Yes     |
| Training Set | 3           | Love Move Joy Good       | Yes     |
| Training Set | 4           | Love Happy Joy Love Pain | Yes     |
| Training Set | 5           | Joy Love Pain Kick Pain  | No      |
| Training Set | 6           | Pain Pain Love kick      | No      |
| Testing Set  | 7           | Love Pain Joy Love Kick  | ?       |

**Task:** Classify document 7 using Multinomial Naive Bayes with Add-1 smoothing.

![[Multinomial_Naive_Bayes_Sum.pdf]]