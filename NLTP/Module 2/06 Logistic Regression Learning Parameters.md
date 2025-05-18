The core of logistic regression is learning the optimal weights `w` and bias `b` from the training data.

## Where Do the Weights `w` Come From?

This is a supervised classification problem.
*   We know the correct label `y` (either 0 or 1) for each training example `x`.
*   The system produces an estimate `ŷ` (a probability between 0 and 1).
*   We want to set `w` and `b` to minimize the **distance** (or error) between our estimate `ŷ^(i)` and the true `y^(i)` for all training instances.

To achieve this, we need two main components:
1.  A **loss function** (or cost function): A way to measure this distance/error for a single example or averaged over all examples.
2.  An **optimization algorithm:** A method to update `w` and `b` iteratively to minimize this loss.

## Learning Components

*   **Loss Function:** For logistic regression, the standard is **cross-entropy loss** (also known as negative log likelihood loss).
*   **Optimization Algorithm:** **Stochastic Gradient Descent (SGD)** or its variants (e.g., mini-batch gradient descent).

## The Distance Between `ŷ` and `y` (Loss Function)

We want to know how far the classifier output `ŷ = σ(w ⋅ x + b)` is from the true output `y` (which is either 0 or 1).
Let this difference be `L(ŷ, y) =` how much `ŷ` differs from the true `y`.

### Intuition of Negative Log Likelihood Loss (Cross-Entropy Loss)

*   This is a case of **conditional maximum likelihood estimation**.
*   We choose the parameters `w` and `b` (denoted collectively as `θ`) that **maximize the log probability** of observing the true `y` labels in our training data, given the observations `x`.
*   Maximizing likelihood is equivalent to minimizing negative log likelihood.

### Deriving Cross-Entropy Loss for a Single Observation `x`

**Goal:** Maximize the probability of the correct label `p(y|x)`.

1.  Since there are only two discrete outcomes (`y=0` or `y=1`), we can express `p(y|x)` from our classifier as:
    `p(y|x) = (ŷ)^y * (1-ŷ)^(1-y)`
    *   If `y=1`: `p(y=1|x) = (ŷ)^1 * (1-ŷ)^(1-1) = ŷ`
    *   If `y=0`: `p(y=0|x) = (ŷ)^0 * (1-ŷ)^(1-0) = 1-ŷ`

2.  **Maximize this `p(y|x)`**.

3.  **Take the log of both sides** (mathematically handy, doesn't change the argmax):
    `log p(y|x) = log [ (ŷ)^y * (1-ŷ)^(1-y) ]`
    `log p(y|x) = y * log(ŷ) + (1-y) * log(1-ŷ)`
    **Maximize this log likelihood.**

4.  **Turn this into a loss function by flipping the sign** (minimizing loss is maximizing likelihood):
    **Cross-Entropy Loss `L_CE(y, ŷ)`:**
    `L_CE(y, ŷ) = - [ y * log(ŷ) + (1-y) * log(1-ŷ) ]`

    Plugging in `ŷ = σ(w ⋅ x + b)`:
    `L_CE(y, x; w, b) = - [ y * log(σ(w ⋅ x + b)) + (1-y) * log(1 - σ(w ⋅ x + b)) ]`

### Example: How Cross-Entropy Loss Works

We want the loss to be:
*   Smaller if the model estimate `ŷ` is close to the correct `y`.
*   Bigger if the model is confused ( `ŷ` is far from `y`).

Consider a sentiment example. Let `ŷ = P(y=1|x)`.
*   **Case 1: True label `y=1` (positive sentiment)**
    *   Loss = `- [1 * log(ŷ) + (1-1) * log(1-ŷ)] = -log(ŷ)`
    *   If model predicts `ŷ = 0.9` (confident and correct): Loss = `-log(0.9) ≈ 0.105` (low loss)
    *   If model predicts `ŷ = 0.1` (confident but incorrect): Loss = `-log(0.1) ≈ 2.302` (high loss)

*   **Case 2: True label `y=0` (negative sentiment)**
    *   Loss = `- [0 * log(ŷ) + (1-0) * log(1-ŷ)] = -log(1-ŷ)`
    *   If model predicts `ŷ = 0.1` (meaning `P(y=0|x) = 0.9`, confident and correct): Loss = `-log(1-0.1) = -log(0.9) ≈ 0.105` (low loss)
    *   If model predicts `ŷ = 0.9` (meaning `P(y=0|x) = 0.1`, confident but incorrect): Loss = `-log(1-0.9) = -log(0.1) ≈ 2.302` (high loss)

The loss function behaves as desired.

## Our Goal: Minimize the Loss

Let `θ = (w, b)` represent all parameters. The loss function `L_CE(y, x; θ)` depends on these parameters.
We want to find the `θ` that minimizes the total loss, averaged over all `m` training examples:
`J(θ) = (1/m) * Σ_{i=1 to m} L_CE(y^(i), x^(i); θ)`
(Often, the `(1/m)` is omitted as it doesn't change the argmin).

## Optimization: Gradient Descent

**Intuition:**
Imagine you are in a river canyon and want to get to the bottom (minimum point).
1.  Look around you 360°.
2.  Find the direction of the steepest slope downwards.
3.  Take a small step in that direction.
4.  Repeat.
*(Image context: A topographic map showing a river canyon with contour lines. An 'X' marks a starting point on a slope.)*

**For Logistic Regression:**
*   The loss function `J(θ)` is **convex**.
*   A convex function has only one minimum.
*   Gradient descent, starting from any point, is guaranteed to find this global minimum.
    *(Note: Loss for neural networks is generally non-convex, having multiple local minima.)*

### Gradients

*   The **gradient** of a function of many variables (like `J(θ)`) is a vector pointing in the direction of the **greatest increase** in the function.
*   **Gradient Descent:** Find the gradient of the loss function at the current point `θ_t` and move in the **opposite** direction to decrease the loss.

*(Image context: Two diagrams of a 1D convex loss function L(w).
    1. If current w is on the left slope (negative slope), the gradient is negative. Moving opposite to gradient means increasing w (moving right).
    2. If current w is on the right slope (positive slope), the gradient is positive. Moving opposite to gradient means decreasing w (moving left).)*

### Update Rule

For a single parameter `w`:
`w^(t+1) = w^(t) - η * (dL/dw)`
Where:
*   `w^(t)` is the current value of the weight.
*   `η` (eta) is the **learning rate**, a hyperparameter that controls the step size.
    *   Too high `η`: learner might take big steps and overshoot the minimum.
    *   Too low `η`: learner will take too long to converge.
*   `dL/dw` is the derivative (gradient for one variable) of the loss `L` with respect to `w`.

### N-Dimensional Case (Vector `θ`)

The gradient `∇J(θ)` is a vector of partial derivatives:
`∇J(θ) = [∂J/∂w₁, ∂J/∂w₂, ..., ∂J/∂wn, ∂J/∂b]`
Each component `∂J/∂wj` tells us how much a small change in `wj` would influence the total loss `J`.

The update rule for the entire parameter vector `θ` is:
`θ^(t+1) = θ^(t) - η * ∇_θ J(θ^(t))`

The partial derivative of the cross-entropy loss `L_CE(y, ŷ)` with respect to a single weight `wj` (for one training example `(x,y)`) can be shown to be:
`∂L_CE/∂wj = (ŷ - y) * xj`
Where `ŷ = σ(w ⋅ x + b)` and `xj` is the j-th feature of input `x`.
The derivative with respect to the bias `b` is `(ŷ - y)`.

So, the update for `wj` is: `wj^(t+1) = wj^(t) - η * (ŷ - y) * xj`
And for `b`: `b^(t+1) = b^(t) - η * (ŷ - y)`

These updates are typically performed for each training example (Stochastic Gradient Descent) or a small batch of examples (Mini-batch Gradient Descent).

### Hyperparameters

*   The **learning rate `η`** is a crucial hyperparameter.
*   **Hyperparameters** are parameters of the learning algorithm itself (not learned from data). They are chosen by the algorithm designer, often through experimentation on a devset.

## Working Through a Gradient Descent Example (One Step)

A mini-sentiment example, true `y=1` (positive).
*   **Two features:**
    *   `x₁ = 3` (count of positive lexicon words)
    *   `x₂ = 2` (count of negative lexicon words)
*   **Initial parameters `θ^0`:** `w₁=0, w₂=0, b=0`
*   **Learning rate `η = 0.1`**

1.  **Calculate `z` and `ŷ` with current `θ^0`:**
    `z = w₁x₁ + w₂x₂ + b = (0*3) + (0*2) + 0 = 0`
    `ŷ = σ(z) = σ(0) = 1 / (1 + e^0) = 1/2 = 0.5`

2.  **Calculate error term `(ŷ - y)`:**
    `ŷ - y = 0.5 - 1 = -0.5`

3.  **Calculate gradients (partial derivatives):**
    *   `∂L/∂w₁ = (ŷ - y) * x₁ = (-0.5) * 3 = -1.5`
    *   `∂L/∂w₂ = (ŷ - y) * x₂ = (-0.5) * 2 = -1.0`
    *   `∂L/∂b  = (ŷ - y)       = -0.5`
    Gradient vector `∇L = [-1.5, -1.0, -0.5]`

4.  **Update parameters `θ^1 = θ^0 - η * ∇L`:**
    *   `w₁^1 = w₁^0 - η * (-1.5) = 0 - 0.1 * (-1.5) = 0 + 0.15 = 0.15`
    *   `w₂^1 = w₂^0 - η * (-1.0) = 0 - 0.1 * (-1.0) = 0 + 0.10 = 0.10`
    *   `b^1  = b^0  - η * (-0.5) = 0 - 0.1 * (-0.5) = 0 + 0.05 = 0.05`

New parameters: `w₁=0.15, w₂=0.10, b=0.05`.
*   The weights moved in a direction that will increase the probability of `y=1` for this example in the next iteration.
*   Note that `w₂` (for negative words) also became positive. With enough negative examples where `y=0`, `w₂` would eventually become negative.

## Mini-Batch Training

*   **Stochastic Gradient Descent (SGD):** Computes gradient and updates parameters using a single random training example at a time. Can result in "choppy" movements towards the minimum.
*   **Batch Gradient Descent:** Computes gradient over the *entire* dataset before updating. Can be slow for large datasets.
*   **Mini-Batch Gradient Descent:** A compromise. Computes gradient over a small batch of `m` training instances (e.g., `m = 32, 64, 128, ..., 1024`). This is the most common approach.
    *   Provides a more stable gradient estimate than SGD.
    *   More computationally efficient than batch GD.