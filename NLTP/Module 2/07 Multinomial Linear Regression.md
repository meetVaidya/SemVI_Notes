Binary logistic regression handles two classes. When we need to classify among more than two classes, we use **Multinomial Logistic Regression**, also known as **Softmax Regression**.
(Older names include Maximum Entropy Modeling or MaxEnt).

"Logistic Regression" typically implies binary, while "Multinomial Logistic Regression" or "Softmax Regression" refers to the multi-class version.

## Use Cases for More Than 2 Classes

*   Sentiment analysis: Positive / Negative / Neutral.
*   Parts of speech tagging: Noun, Verb, Adjective, Adverb, Preposition, etc.
*   Classifying emergency SMSs into different actionable classes (e.g., Fire, Medical, Police).

## Key Idea: Probabilities Must Sum to 1

For `K` classes, the probabilities of an input `x` belonging to each class must sum to 1:
`P(class₁|x) + P(class₂|x) + ... + P(class_K|x) = 1`

We need a generalization of the sigmoid function for this, called the **softmax function**.

## The Softmax Function

The softmax function takes a vector `z = [z₁, z₂, ..., z_K]` of `K` arbitrary real-valued scores (one for each class) and transforms them into a probability distribution.

For each class `j` (from 1 to `K`):
`softmax(z_j) = P(y=j | x) = e^(z_j) / Σ_{k=1 to K} e^(z_k)`

*   **Output Properties:**
    *   Each output value `softmax(z_j)` is in the range [0, 1].
    *   All output values sum to 1: `Σ_{j=1 to K} softmax(z_j) = 1`.

## Softmax in Multinomial Logistic Regression

1.  **Input Scores (`z_j`):**
    Similar to binary logistic regression, the input score for each class `j` is a linear combination of features and weights.
    **Crucially, we now need a separate weight vector `w_j` and bias `b_j` for each class `j`.**
    `z_j = w_j ⋅ x + b_j`

2.  **Probabilities:**
    The probability of input `x` belonging to class `j` is:
    `P(y=j | x; W, B) = softmax(z_j) = e^(w_j ⋅ x + b_j) / Σ_{k=1 to K} e^(w_k ⋅ x + b_k)`
    Where `W` represents all weight vectors `[w₁, ..., w_K]` and `B` represents all biases `[b₁, ..., b_K]`.

3.  **Prediction:**
    The predicted class `ŷ` is the one with the highest probability:
    `ŷ = argmax_j P(y=j | x)`

## Features in Binary vs. Multinomial Logistic Regression

*   **Binary Logistic Regression:**
    *   A single weight vector `w`.
    *   A positive weight `wi` for feature `xi` pushes towards `y=1`.
    *   A negative weight `wi` for feature `xi` pushes towards `y=0`.
    *   Example: `w_awesome = +3.0` (feature "awesome" strongly suggests positive class).

*   **Multinomial Logistic Regression:**
    *   Separate weight vectors for each class: `w_class1, w_class2, ..., w_classK`.
    *   For a feature `xi` (e.g., the word "excellent"), its weight will be different for each class's weight vector.
        *   `w_positive,i` might be high.
        *   `w_negative,i` might be low (or negative if formulation allows).
        *   `w_neutral,i` might be close to zero.
    *   The weight `w_j,i` indicates how much feature `xi` contributes to the score `z_j` for class `j`.

**Learning:** The parameters (all `w_j` and `b_j`) are learned similarly to binary logistic regression, typically by minimizing a multi-class cross-entropy loss function using gradient descent.