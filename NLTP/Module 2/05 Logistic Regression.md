## Overview of Logistic Regression

*   An important analytic tool in natural and social sciences.
*   A baseline supervised machine learning tool for classification.
*   Forms the foundation of neural networks.

## Two Phases of Logistic Regression

1.  **Training Phase:**
    *   Learn weights `w` and bias `b` using an optimization algorithm like **stochastic gradient descent (SGD)**.
    *   The learning process aims to minimize a **loss function**, typically **cross-entropy loss**.
2.  **Test Phase:**
    *   Given a new test example `x`, compute the probability `p(y|x)` using the learned weights `w` and bias `b`.
    *   Return whichever label (`y=1` or `y=0` for binary classification) has a higher probability.

## Classification Reminder

Logistic regression can be used for various classification tasks:
*   Positive/negative sentiment.
*   Spam/not spam.
*   Authorship attribution (e.g., Hamilton or Madison).
    *(Image context: A portrait of Alexander Hamilton.)*

## Text Classification: Formal Definition

*   **Input:**
    *   A document `x` (or `d`)
    *   A fixed set of classes `C = {c₁, c₂, ..., cJ}`
*   **Output:**
    *   A predicted class `ŷ ∈ C`

## Binary Classification in Logistic Regression

*   Given a series of input/output pairs: `(x^(i), y^(i))`, where `y^(i)` is the true label.
*   For each observation `x^(i)`:
    *   We represent `x^(i)` by a **feature vector** `[x₁, x₂, ..., xn]`.
    *   We compute an output: a predicted class `ŷ^(i) ∈ {0, 1}`.

### Features in Logistic Regression

*   For each feature `xi`, an associated weight `wi` tells us how important that feature is for the classification.
*   **Examples (Sentiment Analysis):**
    *   `xi = "review contains 'awesome'"`: `wi = +10` (strong positive indicator)
    *   `xj = "review contains 'abysmal'"`: `wj = -10` (strong negative indicator)
    *   `xk = "review contains 'mediocre'"`: `wk = -2` (weak negative indicator)

## Logistic Regression for One Observation `x`

*   **Input observation:** vector `x = [x₁, x₂, ..., xn]`
*   **Weights:** one per feature, `W = [w₁, w₂, ..., wn]` (sometimes denoted as `θ`)
*   **Bias:** a scalar `b` (sometimes included in `W` by adding a feature `x₀=1`)
*   **Output (binary):** a predicted class `ŷ ∈ {0, 1}`
*   **Output (multinomial):** `ŷ ∈ {0, 1, 2, ..., K-1}` for K classes.

## How to Do Classification (Intuition)

1.  For each feature `xi`, its weight `wi` indicates its importance.
2.  We compute a linear combination: `z = w ⋅ x + b = Σ(wi * xi) + b`.
3.  If this sum `z` is high, we predict `y=1`; if low, then `y=0`.

### Towards a Probabilistic Classifier

We need to formalize "sum is high" and obtain a probability.
Like Naive Bayes, we want a principled classifier that gives us:
*   `p(y=1 | x; θ)`
*   `p(y=0 | x; θ)`
(where `θ` represents the parameters `w` and `b`).

The linear combination `z = w ⋅ x + b` is just a number (can range from -∞ to +∞), not a probability (which must be between 0 and 1).

**Solution:** Use a function that maps `z` to the range [0, 1]. This is the **sigmoid** or **logistic function**.

## The Sigmoid (Logistic) Function

The sigmoid function, denoted `σ(z)`, is defined as:
`σ(z) = 1 / (1 + e^(-z))`

*   It takes any real-valued number `z` and squashes it to a value between 0 and 1.
*   If `z` is large and positive, `σ(z)` approaches 1.
*   If `z` is large and negative, `σ(z)` approaches 0.
*   If `z = 0`, `σ(z) = 0.5`.

*(Image context: A graph of the sigmoid function, S-shaped, ranging from 0 to 1 on the y-axis, with z on the x-axis. A dashed line at P(y=1)=0.5 intersects the curve where wx+b=0.)*

## Idea of Logistic Regression

1.  Compute the linear sum: `z = w ⋅ x + b`
2.  Pass `z` through the sigmoid function: `σ(z) = σ(w ⋅ x + b)`
3.  Treat this output as a probability:
    *   `P(y=1 | x; w, b) = σ(w ⋅ x + b)`
    *   Since probabilities must sum to 1 for binary classification:
        `P(y=0 | x; w, b) = 1 - P(y=1 | x; w, b) = 1 - σ(w ⋅ x + b)`

    *   **Note:** `1 - σ(z) = 1 - [1 / (1 + e^(-z))] = e^(-z) / (1 + e^(-z)) = 1 / (e^z + 1) = σ(-z)`.
        So, `P(y=0 | x; w, b) = σ(-(w ⋅ x + b))`.

## Turning a Probability into a Classifier

To make a hard classification decision:
*   If `P(y=1 | x; w, b) > 0.5`, predict `ŷ = 1`.
*   If `P(y=1 | x; w, b) ≤ 0.5`, predict `ŷ = 0`.

The threshold `0.5` is called the **decision boundary**.
Since `σ(z) > 0.5` when `z > 0`, and `σ(z) ≤ 0.5` when `z ≤ 0`:
*   Predict `ŷ = 1` if `w ⋅ x + b > 0`.
*   Predict `ŷ = 0` if `w ⋅ x + b ≤ 0`.

## Sentiment Example

Consider the review:
> "It's hokey. There are virtually no surprises, and the writing is second-rate. So why was it so enjoyable? For one thing, the cast is great. Another nice touch is the music. I was overcome with the urge to get off the couch and start dancing. It sucked me in, and it'll do the same to you."

Suppose we have learned weights `w` and bias `b`.
Let `x` be the feature vector for this review.
We calculate `z = w ⋅ x + b`.
Then `P(positive) = σ(z)`.
If `σ(z) = 0.9`, we classify as positive. If `σ(z) = 0.2`, we classify as negative.

## Features for Any Classification Task

We can build features for logistic regression for various tasks.
**Example: Period Disambiguation**
Task: Determine if a period `.` marks the end of a sentence or is part of an abbreviation.
*   "This ends in a period." (Period is end of sentence)
*   "The house at 465 Main St. is new." (Period in "St." is not end of sentence)
*(Image context: Arrows pointing to the period in "period." labeled "End of sentence" and to the period in "St." labeled "Not end".)*
Features could include: word preceding period, capitalization of next word, length of word before period, etc.

## Summary: Classification in (Binary) Logistic Regression

*   **Given:**
    *   A set of classes (e.g., {+sentiment, -sentiment}).
    *   A vector `x` of features for an input, e.g.:
        *   `x₁ = count("awesome")`
        *   `x₂ = log(number of words in review)`
    *   A vector `w` of weights `[w₁, w₂, ..., wn]`, one `wi` for each feature `fi`.
    *   A bias term `b`.
*   **Prediction:**
    *   `z = w ⋅ x + b`
    *   `P(y=1|x) = σ(z)`
    *   `ŷ = 1` if `z > 0`, else `ŷ = 0`.