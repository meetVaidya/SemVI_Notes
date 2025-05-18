## Neural Network Unit
A neural network unit (or neuron) is the fundamental processing unit of a neural network. It's a simplified model and not a direct representation of a biological neuron in the brain.

### Core Operations of a Neural Unit
1.  **Weighted Sum of Inputs:** The unit takes multiple input values, and each input is multiplied by a corresponding weight.
    *   `z = (w1*x1 + w2*x2 + ... + wn*xn) + b`
    *   or `z = w · x + b` (dot product of weight vector `w` and input vector `x`, plus bias `b`)
2.  **Non-linear Activation Function:** The weighted sum `z` is then passed through a non-linear activation function `f`.
    *   Output `a = f(z)`

### Example Calculation
Suppose a unit has:
*   Weights `w = [0.2, 0.3, 0.9]`
*   Bias `b = 0.5`
And receives input `x = [0.5, 0.6, 0.1]`

1.  **Weighted Sum (z):**
    `z = (0.2 * 0.5) + (0.3 * 0.6) + (0.9 * 0.1) + 0.5`
    `z = 0.10 + 0.18 + 0.09 + 0.5`
    `z = 0.87`
2.  **Activation (e.g., using Sigmoid):**
    `a = sigmoid(0.87) = 1 / (1 + e^-0.87) ≈ 0.705`


## Common Non-Linear Activation Functions

*   **Sigmoid:**
    *   Formula: `y = 1 / (1 + e^-z)`
    *   Outputs values between 0 and 1.
    *   Historically used, especially in output layers for binary classification.
*   **Tanh (Hyperbolic Tangent):**
    *   Formula: `y = tanh(z) = (e^z - e^-z) / (e^z + e^-z)`
    *   Outputs values between -1 and 1.
    *   Often preferred over sigmoid in hidden layers as it's zero-centered.
*   **ReLU (Rectified Linear Unit):**
    *   Formula: `y = max(0, z)`
    *   Outputs `z` if `z` is positive, and 0 otherwise.
    *   Most common activation function in modern deep learning due to its simplicity and efficiency in combating vanishing gradients.
## Feedforward Neural Networks (FFNs)
Feedforward Neural Networks, also known as Multi-Layer Perceptrons (MLPs), are networks where connections between nodes do not form a cycle. Information moves in only one direction—forward—from the input nodes, through the hidden layers, to the output nodes.

### Single-Layer Networks

*   **Binary Logistic Regression as a 1-Layer Network:**
    *   Input layer (vector `x` and a bias term `+1`).
    *   Output layer consists of a single sigmoid node (`σ`).
    *   Computation: `y = σ(w · x + b)` where `y` is a scalar probability.
	- ![[Pasted image 20250518154727.png]]
    *Note: The input layer is typically not counted when determining the number of layers.*

*   **Multinomial Logistic Regression as a 1-Layer Network:**
    *   Input layer (scalars `x1...xn` and a bias term `+1`).
    *   Output layer consists of multiple softmax nodes (`s`), one for each class.
    *   Computation: `y = softmax(Wx + b)` where `y` is a vector of probabilities. `W` is a weight matrix, `b` is a bias vector.

    *   **Softmax Function:** A generalization of the sigmoid function for multi-class classification.
        *   For a vector `z` of dimensionality `k`, the softmax is: `softmax(z_i) = e^(z_i) / Σ(e^(z_j))` for `j=1 to k`.
        *   It converts a vector of raw scores into a probability distribution.

### Multi-Layer Networks (e.g., Two-Layer Network)

*   **Structure:**
    *   Input Layer (vector `x`).
    *   Hidden Layer: Composed of units (e.g., using sigmoid, tanh, or ReLU activation).
        *   `h = σ(Wx + b)` or `h = f(W_h * x + b_h)` (where `h` is the vector of hidden unit activations).
    *   Output Layer:
        *   For scalar output (e.g., regression or binary classification): `z_out = U · h`, `y = σ(z_out)`.
        *   For vector output (e.g., multi-class classification): `z_out = U * h`, `y = softmax(z_out)`.
## Training Neural Networks

Training involves adjusting the network's weights and biases to minimize a loss function, which measures the difference between the network's predictions and the actual target values.
### Intuition for Training a 2-Layer Network
For every training example `(x, y)`:
1.  **Forward Pass:**
    *   Run the computation forward through the network to get an estimate $\hat{y}$.
2.  **Backward Pass (Backpropagation):**
    *   Compute the loss `L` between the true `y` and the estimated $\hat{y}$
    *   **For every output node:**
        *   Calculate how much each weight `w` connecting the hidden layer to the output layer contributed to the error.
        *   Update these weights.
    *   **For every hidden node:**
        *   Assess how much "blame" it deserves for the current error (propagating the error backward).
        *   Calculate how much each weight `w` connecting the input layer to the hidden layer contributed to this "blame".
        *   Update these weights.

### Loss Function
A measure of how far off the current prediction is from the correct answer.
*   Example: **Cross-entropy loss** for logistic regression (binary classification):
    `L(y_hat, y) = - [y * log(y_hat) + (1 - y) * log(1 - y_hat)]`

### Gradient Descent
An optimization algorithm used to update weights.
*   Use the derivative (gradient) of the loss function with respect to the weights: `dL/dw`.
*   Adjust weights in the opposite direction of the gradient to minimize the loss.
    `w_new = w_old - α * (dL/dw)` (where `α` is the learning rate).
   `∂z/∂w_i`: Derivative of the weighted sum with respect to the weight.
