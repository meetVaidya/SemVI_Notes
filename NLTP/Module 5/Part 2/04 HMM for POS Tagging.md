Hidden Markov Models (HMMs) are widely used for POS tagging. In this context:
*   **Hidden States (Q)**: Represent the POS tags (e.g., Noun, Verb, Adjective).
*   **Observations (O)**: Represent the words in the sentence.

## Generative Model Perspective

(Image context: A diagram of a generative model where a central class 'c' generates data points 'd1' to 'd5'. Text indicates "Example are Hidden Markov Model, Naive Bayes Classifier".)

*   In a generative model, we assume that a class (hidden state/tag) is there and it generates data (observed word).
*   For POS Tagging: POS tags are the hidden states, and words are generated from these tags.
    *   Example: A 'Noun' tag might generate words like 'girl', 'boy', 'man', 'woman', 'water', etc.
*   The flow is downward: Classes (tags) generate Data (words).

(Image context: A diagram illustrating the generative process for "The girl is intelligent". Classes (Determiner, Noun (NN), Verb (VBZ), Adjective(JJ)) are at the top. Arrows point down to Data (The, girl, Is, Intelligent). "State transition probability" is shown between classes, and "Emission probability" is shown from classes to data.)

*   Statement: "The girl is intelligent."
    *   Determiner class generates "The".
    *   NN class generates "girl".
    *   VBZ class generates "is".
    *   JJ class generates "adjective" (should be "intelligent").

## Key Probabilities in HMM for POS Tagging

(Image context: A sequence of tags N -> M -> V -> N above words Jane -> will -> spot -> Will. Arrows between tags represent transition probabilities. Arrows from tags down to words represent emission probabilities.)

1.  **Transition Probability (A matrix: P(ti | ti-1))**
    *   The likelihood of a particular sequence of tags.
    *   Example: How likely is it that a Noun (N) is followed by a Modal (M), a Modal by a Verb (V), and a Verb by a Noun.
    *   This probability should be high for a grammatically common sequence.
    *   Calculated as: `P(ti | ti-1) = C(ti-1, ti) / C(ti-1)`
        *   `C(ti-1, ti)`: Count of tag `ti-1` followed by tag `ti`.
        *   `C(ti-1)`: Count of tag `ti-1`.

2.  **Emission Probability (B matrix: P(wi | ti))**
    *   The probability that a given tag `ti` will be associated with a given word `wi`.
    *   Example: The probability that the word "Jane" is a Noun, "will" is a Modal, "spot" is a Verb.
    *   These probabilities should be high for the correct tagging.
    *   Calculated as: `P(wi | ti) = C(ti, wi) / C(ti)`
        *   `C(ti, wi)`: Count of word `wi` associated with tag `ti`.
        *   `C(ti)`: Count of tag `ti`.

(Image context: Emission Probabilities table for words like Mary, Jane, Will, Spot, Can, See, Pat and tags N, M, V. Example sentences with tag sequences: Mary Jane can see Will (<s> N N M V N <e>), Spot will see Mary (<s> N M V N <e>), etc.)
(Image context: Emission Probabilities shown as a table and also as tree diagrams where each tag (N, M, V) is a root with branches to words and their probabilities.)
(Image context: Transition Probabilities table for tags <s>, N, M, V, <e>. Example sentences with tag sequences.)
(Image context: A full HMM state diagram showing states <s> (start), N, M, V, <e> (end) with directed edges labeled with transition probabilities.)
(Image context: An abstract HMM diagram showing "Hidden States" (N, M, V) above "Observations" (Mary, Will, Spot, Jane, etc.).)
(Image context: The full HMM diagram combining transition probabilities between hidden states and emission probabilities from hidden states to observations.)

## HMM Tagging as Decoding

The task of determining the sequence of hidden variables (tags) corresponding to a sequence of observations (words) is called **decoding**.

*   **Goal**: Given an HMM `λ = (A, B)` and a sequence of observations `O = o1, o2, ..., oT` (words), find the most probable sequence of states `Q = q1, q2, ..., qT` (tags).

For part-of-speech tagging, the goal of HMM decoding is to choose the tag sequence `t1...tn` that is most probable given the observation sequence of `n` words `w1...wn`:
`t_hat (1:n) = argmax (over t1...tn) P(t1...tn | w1...wn)`

### Using Bayes' Rule

We use Bayes' rule to transform the problem:
`P(t1...tn | w1...wn) = [P(w1...wn | t1...tn) * P(t1...tn)] / P(w1...wn)`

(Image context: Bayes' rule formula P(A|B) = (P(B|A) * P(A)) / P(B).)

Since `P(w1...wn)` is constant for a given sentence, we can simplify the argmax:
`t_hat (1:n) = argmax (over t1...tn) [P(w1...wn | t1...tn) * P(t1...tn)]`

### Simplifying Assumptions for HMM Taggers

1.  **Probability of a word appearing depends only on its own tag** (independent of neighboring words and tags):
    `P(w1...wn | t1...tn) ≈ Π (from i=1 to n) P(wi | ti)` (This is the product of emission probabilities)

2.  **Bigram assumption for tags**: The probability of a tag depends only on the previous tag (not the entire tag sequence):
    `P(t1...tn) ≈ Π (from i=1 to n) P(ti | ti-1)` (This is the product of transition probabilities, often including P(t1 | <s>) for the first tag)

### Final Equation for Most Probable Tag Sequence

Plugging these assumptions into the simplified argmax equation:
`t_hat (1:n) ≈ argmax (over t1...tn) [ Π (from i=1 to n) P(wi | ti) * P(ti | ti-1) ]`
(Image context: The formula showing argmax over the product of emission and transition probabilities.)

This means we want to find the sequence of tags that maximizes the product of the relevant emission and transition probabilities. The Viterbi algorithm is commonly used to find this optimal sequence efficiently.