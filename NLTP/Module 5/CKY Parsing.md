## CKY (Cocke–Younger–Kasami) Parsing

### 1. What Is CKY Parsing?
- A **dynamic programming** algorithm for deciding whether a sentence belongs to the language of a CFG and, if so, recovering its parse.
- **Requirement:** The grammar **must** be in **Chomsky Normal Form (CNF)**, i.e., every rule is either:
  1. \( A \to BC \) (two non-terminals)  
  2. \( A \to a \) (a single terminal)

---

### 2. The CKY Table \( T \)
- For an \( n \)-word sentence \( w_1 \dots w_n \), build an \( n \times n \) **upper triangular table** \( T[i,j] \).
  - **Cell** \( T[i,j] \): Set of non-terminals that can derive the substring \( w_i \dots w_j \).
  - Fill **diagonals** (span length 1) first, then span length 2, 3, …, up to \( n \).

---

### 3. CKY Algorithm Steps

1. **Convert** the CFG to CNF.
2. **Initialize** the table:  
   For each position \( i = 1 \dots n \):  
   \[
   T[i,i] = \{ A \mid A \to w_i \in R \}
   \]
3. **Fill larger spans**:
   - For span length \( \ell = 2 \dots n \), for start \( i = 1 \dots n - \ell + 1 \), let \( j = i + \ell - 1 \):
     - For each split point \( k = i \dots j - 1 \):
       - For each rule \( A \to B\,C \):  
         If \( B \in T[i,k] \) and \( C \in T[k+1,j] \), then add \( A \) to \( T[i,j] \).
4. **Accept** if the start symbol \( S \in T[1,n] \). Otherwise, reject.

---

### 4. Worked Example

#### Grammar \( G \) in CNF:

```
Non-terminals: {S, B, C}
Terminals:     {a, flight}
Rules:
  S → B C
  B → a
  C → flight
Start symbol: S
```

#### Sentence:
```
a flight   (n = 2)
```

---

#### Step 1: Initialize Diagonal

- \( T[1,1] \): covers "a" → find \( A \to a \):  
  \( T[1,1] = \{ B \} \)

- \( T[2,2] \): covers "flight" → find \( A \to \texttt{flight} \):  
  \( T[2,2] = \{ C \} \)

---

#### Step 2: Fill Span of Length 2 (i = 1, j = 2)

- Only possible split: \( k = 1 \)
  - Rule \( S \to B\,C \)
  - \( B \in T[1,1] \), \( C \in T[2,2] \) ⇒ add \( S \) to \( T[1,2] \)

---

#### Final CKY Table

| **i\\j** | **1** ("a") | **2** ("flight") |
|:--------:|:-----------:|:----------------:|
| **1**    | {B}         | {S}              |
| **2**    | —           | {C}              |

✅ Since \( S \in T[1,2] \), the sentence **"a flight"** is **generated** by \( G \).

---

#### In Practice

- For longer sentences, continue filling spans of length 3, 4, etc.
- To **recover the parse tree**, store **back-pointers** whenever adding a non-terminal to \( T[i,j] \).

### 5. CKY Algorithm
![[CKY Algorithm.png]]