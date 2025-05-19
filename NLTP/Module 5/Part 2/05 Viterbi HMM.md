The Viterbi algorithm is a dynamic programming algorithm used to find the most likely sequence of hidden states (e.g., POS tags) that results in a sequence of observed events (e.g., words). It efficiently solves the HMM decoding problem.

## The Problem: Finding the Correct Path

Given a sentence (sequence of words), there can be many possible combinations of POS tags.
Example: "Jane will spot Will"
*   Jane: Noun
*   will: Noun, Modal
*   spot: Noun, Verb
*   Will: Noun

We need to pick the combination of tags that generates the sentence with the highest probability, according to our HMM (transition and emission probabilities).

(Image context: A quiz asking "How many possibilities?" for "Jane will spot Will" with tags N, M, V. The next slide shows a trellis diagram with possible paths for the sentence, asking "How many paths do we have to check now?". The solution shows 4 possible paths.)

For "Jane will spot Will", considering possible tags:
*   Jane (N)
*   will (N or M)
*   spot (V) - assuming 'spot' is only a verb for simplicity here, or disambiguated.
*   Will (N)

Possible paths (simplified example):
1.  N - N - V - N
2.  N - M - V - N

If "spot" could also be N, and "will" could be N or M, the number of paths increases.
The Viterbi algorithm avoids exhaustively calculating the probability of every single path.

## Core Idea of Viterbi

For every possible state (tag) at each time step (word position), the Viterbi algorithm finds the highest probability path that *ends* in that state at that time step.

(Image context: A series of diagrams illustrating the Viterbi algorithm for "Jane will spot Will".
1.  Initial trellis showing all possible states (N, M, V) for each word (Jane, will, spot, Will) and connections.
2.  Emission and Transition probability matrices are provided.
3.  Step-by-step calculation:
    *   For "Jane": Probabilities for N, M, V are calculated based on <s> transition and emission P(Jane|Tag).
    *   For "will": For each current tag of "will" (e.g., N), it considers paths from all possible tags of "Jane", calculates `prev_prob * transition_prob * emission_prob`, and takes the max.
    *   This process continues for "spot" and "Will".
    *   At each step, for each state, the algorithm stores the maximum probability to reach that state and a backpointer to the previous state that yielded this maximum probability.
4.  Finally, it traces back from the end state with the highest probability to find the optimal path.)

## Viterbi Algorithm Steps (Conceptual)

Let `v_t(j)` be the maximum probability of any path ending at time `t` in state `j`, having generated the first `t` observations.
Let `ptr_t(j)` store the previous state `i` that led to this maximum probability for state `j` at time `t`.

1.  **Initialization (t=1, for the first word w1):**
    For each state `j`:
    `v_1(j) = P(t1=j | <s>) * P(w1 | t1=j)` (Initial transition prob * Emission prob)
    `ptr_1(j) = <s>` (or a special start symbol)

2.  **Recursion (t = 2 to T, for words w2 to wT):**
    For each state `j`:
    `v_t(j) = max_i [ v_{t-1}(i) * P(tj=j | ti=i) ] * P(wt | tj=j)`
    `ptr_t(j) = argmax_i [ v_{t-1}(i) * P(tj=j | ti=i) ]`
    (Here, `P(tj=j | ti=i)` is the transition probability from state `i` to state `j`, and `P(wt | tj=j)` is the emission probability of word `wt` given state `j`.)

3.  **Termination:**
    The probability of the most likely sequence is `max_j [ v_T(j) * P(<e> | tT=j) ]` (if an end state transition is used).
    The last state of the most likely sequence is `q_T_hat = argmax_j [ v_T(j) * P(<e> | tT=j) ]`.

4.  **Path (Tag Sequence) Backtracking:**
    Start with `q_T_hat`.
    For `t = T-1` down to `1`:
    `q_t_hat = ptr_{t+1}(q_{t+1}_hat)`
    The sequence `q_1_hat, ..., q_T_hat` is the most likely tag sequence.

### Example Walkthrough: "Jane will spot Will"

(Image context: The trellis diagram is populated with probabilities at each node (state for a word). For each node, the highest probability path to reach it is calculated. For example, for "will" as M, the probability is calculated by taking the max over paths coming from "Jane" as N, M, or V. The diagram shows the final chosen path highlighted.)

*   **Emission Probabilities (P(word|tag))**:
    *   P(Jane|N) = 2/9
    *   P(will|N) = 1/9, P(will|M) = 3/4
    *   P(spot|V) = 1/4 (assuming only V for simplicity in some diagrams, or P(spot|N) = 2/9)
    *   P(Will|N) = 1/9
    *   (Other P(word|tag) are 0 if not listed or if the tag is not possible for the word)

*   **Transition Probabilities (P(tag_curr | tag_prev))**:
    *   P(N|<s>) = 3/4, P(M|<s>) = 1/4
    *   P(N|N) = 1/9, P(M|N) = 1/3, P(V|N) = 1/9, P(<e>|N) = 4/9
    *   P(N|M) = 1/4, P(V|M) = 3/4
    *   P(N|V) = 1 (or 4/4)

**Step 1: Jane (t=1)**
*   `v1(N_Jane)` = P(N|<s>) * P(Jane|N) = (3/4) * (2/9) = 6/36 = 1/6
*   `v1(M_Jane)` = P(M|<s>) * P(Jane|M) = (1/4) * 0 = 0 (assuming P(Jane|M)=0)
*   `v1(V_Jane)` = P(V|<s>) * P(Jane|V) = 0 * 0 = 0

**Step 2: will (t=2)**
*   For `N_will`:
    *   Path from `N_Jane`: `v1(N_Jane) * P(N|N) * P(will|N) = (1/6) * (1/9) * (1/9) = 1/486`
    *   (Assume other paths to `N_will` are 0 if `M_Jane` or `V_Jane` had 0 prob)
    *   `v2(N_will) = 1/486`, `ptr2(N_will) = N_Jane`
*   For `M_will`:
    *   Path from `N_Jane`: `v1(N_Jane) * P(M|N) * P(will|M) = (1/6) * (1/3) * (3/4) = 3/72 = 1/24`
    *   `v2(M_will) = 1/24`, `ptr2(M_will) = N_Jane`
*   For `V_will`: (Assuming P(will|V)=0)
    *   `v2(V_will) = 0`

**Step 3: spot (t=3)**
*   For `V_spot`:
    *   Path from `N_will`: `v2(N_will) * P(V|N) * P(spot|V) = (1/486) * (1/9) * (1/4) = 1/17496`
    *   Path from `M_will`: `v2(M_will) * P(V|M) * P(spot|V) = (1/24) * (3/4) * (1/4) = 3/384 = 1/128`
    *   `v3(V_spot) = 1/128` (max), `ptr3(V_spot) = M_will`
*   (Other states for "spot" calculated similarly)

**Step 4: Will (t=4)**
*   For `N_Will`:
    *   Path from `V_spot`: `v3(V_spot) * P(N|V) * P(Will|N) = (1/128) * (1) * (1/9) = 1/1152`
    *   (Assume other paths to `N_Will` are smaller)
    *   `v4(N_Will) = 1/1152`, `ptr4(N_Will) = V_spot`

**Termination & Backtracking:**
*   Assume `N_Will` has the highest final probability (e.g., `v4(N_Will) * P(<e>|N)`).
*   `q4_hat = N_Will`
*   `q3_hat = ptr4(N_Will) = V_spot`
*   `q2_hat = ptr3(V_spot) = M_will`
*   `q1_hat = ptr2(M_will) = N_Jane`

**Most likely tag sequence: N - M - V - N** (Jane/N will/M spot/V Will/N)
The probability of this path is `(3/4)*(2/9) * (1/3)*(3/4) * (3/4)*(1/4) * (1)*(1/9) * (4/9)` (if including end state transition) or simply the final `v_T(q_T_hat)`. The example calculations in the slides show the product of probabilities along the chosen path. The final probability for N-M-V-N path was 0.000385 in one of the slide examples.

**Key takeaway:**
*   At each step, for each possible current tag, we only keep the path (and its probability) that has the highest probability of reaching that tag so far.
*   We store backpointers to reconstruct the best path once we reach the end of the sentence.
*   This dynamic programming approach avoids recomputing probabilities for subpaths and efficiently finds the global optimum.

(Image context: Final solution diagram showing the path N (Jane) -> M (will) -> V (spot) -> N (Will) with associated probabilities on edges and nodes, resulting in the highest overall probability.)