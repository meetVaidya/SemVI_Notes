Language Modeling (LM) is the task of predicting the next word in a sequence or, more generally, assigning a probability to a piece of text. RNNs are particularly effective for this task due to their ability to handle sequential context.

### RNNs as Language Models

- **Processing:** RNNs process sequences one word at a time.
    
- **Prediction:** They attempt to predict the next word in a sequence by using the current input word and the previous hidden state as inputs.
    
- **Context:** Unlike N-gram models which have a limited context constraint, RNNs can theoretically capture long-range dependencies. The hidden state $h_t$ embodies information about all preceding words in the sequence.
    

#### Model Details

- **Input ($x_t$):** Word embeddings (e.g., from a pre-trained model or learned jointly) for the current word at time step $t$. Often, these are initially represented as one-hot vectors of size $|V|\times1$ (where $|V|$ is vocabulary size) which are then multiplied by an embedding matrix $E$ to get dense embeddings.
    
- **Hidden Layer ($h_t$):** Computed based on the current input embedding $E(x_t)$ and the previous hidden state $h_{t-1}$:
    
    $h_t = g(W\,E(x_t) + U\,h_{t-1} + b_h)$
- **Output Layer ($y_t$):** The hidden layer $h_t$ is used to generate an output layer, which is then passed through a Softmax function to produce a probability distribution over the entire vocabulary:
    
    $y_t = \mathrm{softmax}(V\,h_t + b_y)$
    
    This $y_t$ represents $P(\text{word}\mid \text{context so far})$.
    

---

## Numerical Example: RNN for Language Modeling

**Sentence:** "The cat sat on the mat."  
**Vocabulary:** ${\text{The},\text{cat},\text{sat},\text{on},\text{mat}}$ (Size $|V|=5$)

### Step 1: Assign Numerical Representation (One-Hot Vectors)

| Word | Index | One-Hot Vector |
| :--- | :---- | :------------- |
| The  | 0     | $[1,0,0,0,0]$  |
| cat  | 1     | $[0,1,0,0,0]$  |
| sat  | 2     | $[0,0,1,0,0]$  |
| on   | 3     | $[0,0,0,1,0]$  |
| mat  | 4     | $[0,0,0,0,1]$  |

### Training Data: Input–Output Pairs

|Input|Expected Output|
|:--|:--|
|The|cat|
|The cat|sat|
|The cat sat|on|
|The cat sat on|mat|

### Step 2: Forward Pass in RNN

The RNN updates its hidden state using:

$h_t = \tanh(W_h\,h_{t-1} + W_x\,x_t + b_h)$.

**Assumptions:**

- Hidden state size $=3$
    
- Initial state $h_0=[0,0,0]^T$
    
- Example parameters:
    
    $W_x=\begin{bmatrix}0.2&0.3&-0.4&0.1&-0.3\\0.4&-0.2&0.5&-0.1&0.2\\-0.5&0.1&0.3&0.2&-0.4\end{bmatrix}, W_h=\begin{bmatrix}0.2&0.4&-0.5\\0.3&-0.2&0.1\\-0.4&0.5&0.3\end{bmatrix}, b_h=\begin{bmatrix}0.01\\-0.02\\0.03\end{bmatrix}$.

#### Step 2.1: Compute $h_1$ for Input "The"

- $x_1=[1,0,0,0,0]^T$
    
- $h_0=[0,0,0]^T$
    

$\begin{aligned} W_h\,h_1 &= [0,0,0]^T,\\ W_x\,x_1 &= \text{first column of }W_x = [0.2,\,0.3,\,-0.4]^T,\\ h_1 &= \tanh\bigl([0,0,0]^T + [0.2,0.3,-0.4]^T + [0.01,-0.02,0.03]^T\bigr)\\ &= \tanh([0.21,0.28,-0.37]^T)\\ &\approx [0.207, 0.273, -0.354]^T. \end{aligned}$

### Step 3: Compute Softmax Output

Parameters:

$W_o=\begin{pmatrix}0.2&-0.1&0.4\\0.1&0.3&-0.2\\-0.3&0.2&0.5\\0.4&-0.3&0.1\\0.2&0.1&-0.1\end{pmatrix}, \quad b_o=\begin{pmatrix}0.01\\0.02\\-0.01\\0.03\\-0.02\end{pmatrix}$.

Using $h_1=[0.207,0.273,-0.354]^T$:

$z=W_o\,h_1+b_o = [0.07,0.04,-0.02,0.09,0.03]^T$,  
$y=\mathrm{softmax}(z)=[0.213,0.206,0.194,0.218,0.199]^T$.

Prediction: highest prob $0.218$ for "on". Target was "cat" ($P=0.206$).

### Step 4: Cross-Entropy Loss

Target index $1$ ("cat"); loss:

$L = -\log(0.206) \approx 1.58$.

### Step 5: Backpropagation Through Time (BPTT)

Compute gradients of all parameters via the chain rule over the unrolled network and update them accordingly.

---

## Using Word Embeddings Instead of One-Hot Vectors

### Step 1: Assign Word Embeddings

Assume 3D embeddings:

|Word|Embedding|
|:--|:--|
|The|$[0.4,0.1,0.7]$|
|cat|$[0.9,0.3,0.8]$|
|sat|$[0.5,0.2,0.6]$|
|on|$[0.2,0.7,0.3]$|
|mat|$[0.8,0.5,0.1]$|

### Step 2: Forward Pass with Embeddings

Use same RNN formula, but now $x_t$ is a dense vector and $W_x$ is $3\times3$.

#### Step 2.1: Compute $h_1$ for "The"

$W_x=\begin{bmatrix}0.2&0.4&-0.5\\0.3&-0.2&0.1\\-0.4&0.5&0.3\end{bmatrix}, \quad W_h=\begin{bmatrix}0.1&-0.2&0.3\\0.4&0.3&-0.1\\-0.2&0.5&0.2\end{bmatrix}, \quad b_h=\begin{bmatrix}0.01\\-0.02\\0.03\end{bmatrix}$.

With $x_1=[0.4,0.1,0.7]^T$ and $h_0=0$:

$W_xx_1=[-0.23,0.17,0.10]^T$,  
$h_1=\tanh([-0.23,0.17,0.10]^T+[0.01,-0.02,0.03]^T)\approx[-0.217,0.168,0.119]^T$.

### Step 3: Softmax Output with Embeddings

Using same $W_o,b_o$ and $h_1$: pre-softmax $z=[-0.033,0.053,0.035,-0.031,-0.001]^T$,  
$y=\mathrm{softmax}(z)=[0.193,0.213,0.209,0.194,0.191]^T$. Highest prob $0.213$ for "cat".

### Step 4: Cross-Entropy Loss

$L = -\log(0.213) \approx 1.55$.

Rest of training (BPTT) proceeds as before. Embeddings capture semantics and reduce dimensionality for large vocabularies.
