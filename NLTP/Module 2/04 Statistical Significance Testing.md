## How Do We Know if One Classifier is Better Than Another?

*   **Given:**
    *   Classifier A and Classifier B.
    *   A performance metric M (e.g., accuracy, F1-score).
    *   `M(A,x)` is the performance of A on test set `x`.
    *   `δ(x) = M(A,x) – M(B,x)` is the performance difference between A and B on test set `x`.
*   We want to know if `δ(x) > 0`, meaning A is better than B.
*   `δ(x)` is called the **effect size**.
*   If we observe `δ(x)` is positive, are we done? No! This might be an accident of this one test set or experimental circumstance.

## Statistical Hypothesis Testing

We use hypothesis testing to address this:

1.  **Consider two hypotheses:**
    *   **Null Hypothesis (H₀):** Classifier A is *not* better than Classifier B (i.e., `δ(x) ≤ 0`). This is the default assumption we try to disprove.
    *   **Alternative Hypothesis (H₁):** Classifier A *is* better than Classifier B (i.e., `δ(x) > 0`).

2.  **Goal:** We want to rule out H₀.

3.  **Methodology:**
    *   We create a random variable `X` representing the range of possible test sets.
    *   We ask: If H₀ is true (A isn't better than B), how likely is it that we would observe the `δ(x)` (the effect size) that we did see, or an even larger one, just by chance?

4.  **The p-value:**
    *   This likelihood is formalized as the **p-value**.
    *   The p-value is the probability of observing a test statistic (like our `δ(x)`) at least as extreme as the one actually observed, *assuming the null hypothesis H₀ is true*.
    *   Example: If H₀ is true (A is not better than B), but we observe a huge `δ(x)`, this would be surprising.

5.  **Decision Rule:**
    *   A very small p-value means that the observed difference is very unlikely under the null hypothesis.
    *   If the p-value is below a predetermined **significance level** (alpha, α), typically .05 or .01, we **reject the null hypothesis H₀**.
    *   Rejecting H₀ means we conclude that the result (e.g., "A is better than B") is **statistically significant**.

**Example:**
*   Classifier A has an accuracy of 85%.
*   Classifier B has an accuracy of 82%.
*   The observed difference `δ = 85% - 82% = 3%`.
*   We need to determine if this 3% difference is real or just random noise.

## Computing the Probability (p-value)

*   In NLP, parametric tests (like t-tests) are not always suitable due to assumptions about data distribution.
*   Instead, **non-parametric tests based on sampling** are often used. These involve artificially creating many versions of the test setup.
    *   For example, imagine we created "zillions" of alternative test sets `x'`.
    *   We measure `δ(x')` on each of these test sets.
    *   This gives us a distribution of `δ` values.
    *   If our original observed `δ(x)` is very extreme in this distribution (e.g., larger than 99% of the `δ(x')` values when H₀ is assumed), we might conclude our original `δ(x)` was a real difference.

## Common Non-Parametric Approaches

*   **Approximate Randomization**
*   **Bootstrap Test**

### Paired Tests

*   Used when comparing two sets of observations where each observation in one set can be paired with an observation in another.
*   Example: When evaluating systems A and B on the *same test set*, we can compare their performance on each individual item `xi` in the test set.

## Example Scenario for Hypothesis Testing

*   You have two sentiment classifiers:
    *   Classifier A (Logistic Regression) with an F1 score of 0.76.
    *   Classifier B (Naive Bayes) with an F1 score of 0.72.
*   The difference in performance `δ(x) = 0.76 - 0.72 = 0.04` on a test set of 1000 movie reviews.

*   **The Problem:** Is this `δ(x) = 0.04` statistically significant? Can we confidently say A is better than B, or could this difference be due to chance?

*   **Hypothesis Testing Setup:**
    *   **Null Hypothesis (H₀):** The difference in performance `δ(x)` is less than or equal to zero (`δ(x) ≤ 0`). (Classifier A is not actually better than Classifier B).
    *   **Alternative Hypothesis (H₁):** The difference in performance `δ(x)` is greater than zero (`δ(x) > 0`). (Classifier A is better than Classifier B).

*   **Creating a Random Variable X:** Treat the test set as a random variable X representing all possible test sets. We want to know how likely it is, under H₀, to observe `δ(x) = 0.04` or larger.

*   **Understanding the p-Value:**
    *   The p-value answers: "If Classifier A isn’t really better than Classifier B (H₀ is true), how likely is it that we would see a difference of 0.04 or more by pure chance?"
    *   **Low p-value (e.g., < 0.01):** Such a large difference is unlikely under H₀. Reject H₀. Conclude A is significantly better.
    *   **High p-value:** The observed difference isn't surprising under H₀. Do not reject H₀. Not enough evidence to say A is better.

## The Paired Bootstrap Test

The bootstrap test is a resampling method that can be applied to any metric (accuracy, precision, F1, etc.).
*   **Bootstrap:** Repeatedly draw a large number of smaller samples *with replacement* (called bootstrap samples) from an original larger sample (our test set).

### Bootstrap Example Steps (Conceptual)

1.  **Original Test Set & Observed Difference:**
    *   We have an original test set `x` (e.g., 10 documents).
    *   We have the results of systems A and B on `x`.
    *   We calculate the observed performance difference `δ(x)`. Let's say `δ(x) = 0.2` for this example.
        *(Image context: A table showing results for 10 documents for Classifier A and B, indicating whether each classifier was correct (✅) or incorrect (❌) for each document.
        Doc 1: A✅ B✅; Doc 2: A✅ B❌; Doc 3: A❌ B✅; Doc 4: A✅ B✅; Doc 5: A✅ B❌;
        Doc 6: A❌ B✅; Doc 7: A✅ B✅; Doc 8: A❌ B❌; Doc 9: A✅ B❌; Doc 10: A❌ B✅ )*

2.  **Create Many "Fake" Bootstrap Test Sets (Resampling):**
    *   Create `b` (e.g., 10,000 or 100,000) virtual test sets `x(i)`.
    *   Each `x(i)` is the same size as the original test set `x` (e.g., 10 documents).
    *   To make each `x(i)`, randomly select documents from the original test set `x` *with replacement*, `n` times (where `n` is the size of `x`).
        *   "With replacement" means a document can be selected multiple times for the same bootstrap sample, and some original documents might not be selected at all.
        *(Image context: Three example bootstrapped test sets, each with 10 documents drawn from an original set of 10 documents. Document numbers are shown, illustrating that some documents are repeated within a set, and each set is different.)*

3.  **Measure Performance Difference for Each Bootstrap Set:**
    *   For each bootstrap sample `x(i)`, calculate the performance difference `δ(x(i))` between classifier A and B on that sample.
    *   This gives `b` different `δ'` values.

4.  **Build a Distribution of Differences:**
    *   These `b` values of `δ(x(i))` form a distribution. This distribution shows how `δ(x)` might vary if we were to test on slightly different (resampled) sets of documents.
    *   If most `δ(x(i))` values are close to 0, it suggests the original `δ(x)` could be due to chance.
    *   If very few `δ(x(i))` values exceed the original `δ(x)`, it means such a big difference is rare by chance alone.

5.  **Compute the p-Value:**
    The p-value is the proportion of bootstrap samples where the observed difference `δ(x(i))` is greater than or equal to the original observed difference `δ(x)`.
    *   **Slight Complication (Adjusting for Bias):** The bootstrap samples `x(i)` are drawn from the original test set `x`, which itself has an observed difference `δ(x)`. So, the distribution of `δ(x(i))` will be centered around `δ(x)`, not 0 (as H₀ would imply for the true difference).
    *   To account for this, the p-value is often calculated as the proportion of times `δ(x(i)) - δ(x)` (the difference from the mean of the bootstrap distribution) is greater than or equal to `δ(x)` (how far our observed value is from zero). Or, more simply, how often `δ(x(i))` is more extreme in the direction of H₁ than what H₀ would predict, considering the bias.
    *   A common formulation for a one-sided test (A is better than B, so `δ(x) > 0`):
        `p-value(x) = (1/b) * Σ_{i=1 to b} 1( δ(x(i)) ≥ 2 * δ(x) )`  (This is one way to center, assuming H0 implies δ(x) should be 0, and our samples are centered at δ(x))
        Alternatively, and more intuitively for H₀: `δ(true) = 0`:
        `p-value(x) = (1/b) * Σ_{i=1 to b} 1( δ(x(i)) ≥ δ(x) )` if we assume the bootstrap distribution under H0 would be centered at 0 but shifted by `δ(x)`.
        The slides use: `p-value(x) = (1/b) * Σ_{i=1 to b} 1( δ(x(i)) - δ(x) ≥ δ(x) )` which simplifies to `1( δ(x(i)) ≥ 2δ(x) )`.
        And also: `p-value(x) = (Number of times δ' ≥ δ) / (Total bootstrap samples)`
        Let's use the definition: "proportion of virtual test sets where the difference `δ(x')` is greater than or equal to the original difference `δ(x)`."
        `p-value = (Count of bootstrap samples where δ(x(i)) ≥ δ(x)) / b`
        *(Image context: A table showing 5 bootstrap samples.
        Original δ(x) = 0.2
        Sample 1: δ(x(1))=0.3, δ(x(1))-δ(x)=0.1. Indicator 1(0.1 ≥ 0) = 1.
        Sample 2: δ(x(2))=0.1, δ(x(2))-δ(x)=-0.1. Indicator 1(-0.1 ≥ 0) = 0.
        ... for 5 samples, indicator is 1 three times. Estimated p-value = 3/5 = 0.6.)*
        *The example table on slide 17 (image) calculates `δ(x(i)) - δ(x) ≥ 0`. This is checking if the bootstrap sample's difference is greater than or equal to the original observed difference. If the original difference `δ(x)` is positive, and we are testing if A is better than B, then H0 is `true_delta <= 0`. The p-value is `P(observed_delta or more extreme | H0 is true)`. The bootstrap distribution is centered around `observed_delta`. We want to see how often a value as large as `observed_delta` occurs if the true mean were 0. This is often done by shifting the bootstrap distribution: `δ*(i) = δ(x(i)) - δ(x)`. Then the p-value is `count(δ*(i) >= δ(x)) / b` or `count(δ(x(i)) >= 2*δ(x)) / b`. Or, more simply, `count(δ(x(i)) >= δ(x)) / b` is used to see how many times the resampled statistic exceeds the original statistic, which can be conservative if `δ(x)` is large.*
        The formula on slide 16 is `p-value(x) = (1/b) * Σ 1( δ(x(i)) - δ(x) ≥ 0 )` assuming `δ(x)` is the expected value under H0, which is not quite right. It should be `1( δ(x(i)) ≥ δ(x) )` when testing if the observed `δ(x)` is significantly greater than 0.
        The example on slide 27 uses: `p-value = (Number of times δ' ≥ δ) / (Total test sets (100,000))`
        Example: If original `δ(x) = 0.04`, and in only 47 out of 100,000 bootstrap samples, `δ(x(i)) ≥ 0.04`.
        Then, `p-value = 47 / 100,000 = 0.00047`.

6.  **Decide Whether A is Truly Better Than B:**
    *   If `p-value < α` (e.g., 0.01 or 0.05), reject H₀. Conclude A is significantly better than B.
    *   If `p-value > α`, do not reject H₀. The observed difference could be due to chance.

This bootstrap procedure provides an empirical way to estimate the p-value without making strong assumptions about the underlying data distribution.