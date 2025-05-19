## Bag‑of‑Words (BoW) Representation
BoW converts text into fixed‑length vectors by counting term occurrences, ignoring word order and syntax.

### How It Works
1. **Build Vocabulary:** List unique words across all documents (after preprocessing).  
2. **Vector Construction:** For each document, create a vector of length |V| where each entry is the raw count of the corresponding vocabulary word in that document.  
3. **Result:** Document represented as frequency vector.  

### Properties
- **Simplicity:** Easy to implement; useful baseline.  
- **High Dimensionality & Sparsity:** Large vocabulary → many zero entries.  
- **Context Ignorance:** Loses syntax and word order information. :contentReference[oaicite:0]{index=0}:contentReference[oaicite:1]{index=1}  

### Example
Documents:
- D1: “Welcome to Great Learning, now start learning.”  
- D2: “Learning is a good practice.”  

Vocabulary → [welcome, to, great, learning, now, start, is, a, good, practice]  

| Term      | D1 Count | D2 Count |
|-----------|----------|----------|
| welcome   | 1        | 0        |
| to        | 1        | 0        |
| great     | 1        | 0        |
| learning  | 2        | 1        |
| now       | 1        | 0        |
| start     | 1        | 0        |
| is        | 0        | 1        |
| a         | 0        | 1        |
| good      | 0        | 1        |
| practice  | 0        | 1        |

Matrix:
D1: [1,1,1,2,1,1,0,0,0,0]  
D2: [0,0,0,1,0,0,1,1,1,1]

---

## Term Frequency (TF)
- **Definition:** \(\mathrm{TF}(t,d) = \frac{\text{count of term }t\text{ in }d}{\text{total terms in }d}\).  
- **Purpose:** Normalizes raw counts by document length, reducing bias toward longer documents.

## Inverse Document Frequency (IDF)
- **Definition:**  
  \[
    \mathrm{IDF}(t) = \log\!\Biggl(\frac{N}{|\{d: t\in d\}|}\Biggr),
  \]  
  where \(N\) is total number of documents, and the denominator is number of documents containing term \(t\).  
- **Purpose:** Penalizes terms that appear in many documents (stop words), highlighting discriminative words.  

---

## Computing TF‑IDF
\[
  \mathrm{TF\text{-}IDF}(t,d) = \mathrm{TF}(t,d) \times \mathrm{IDF}(t).
\]

### Step‑by‑Step
1. Compute TF for each term in each document.  
2. Compute IDF for each term across the corpus.  
3. Multiply TF and IDF values to obtain TF‑IDF weight matrix.  

---

## TF‑IDF Example
Corpus of 3 documents:
1. “The cat sat on the mat.”  
2. “The dog sat on the log.”  
3. “The cat and the dog played.”  

| Term | TF in D1 | DF (#docs containing term) | IDF = log(3/DF) | TF‑IDF in D1 |
|------|----------|-----------------------------|------------------|--------------|
| the  | 2/6      | 3                           | log(3/3)=0      | 0            |
| cat  | 1/6      | 2                           | log(3/2)=0.176  | 0.029        |
| sat  | 1/6      | 2                           | 0.176           | 0.029        |
| on   | 1/6      | 2                           | 0.176           | 0.029        |
| mat  | 1/6      | 1                           | log(3/1)=1.099  | 0.183        |
| …    | …        | …                           | …                | …            |

- **Interpretation:** “mat” receives highest weight in D1 due to rarity; “the” gets zero weight.  

---

## Advantages & Limitations

| Aspect                 | BoW                             | TF‑IDF                            |
|------------------------|---------------------------------|-----------------------------------|
| Captures Term Frequency| ✔                               | ✔                                 |
| Accounts for Term Rarity| ✘                              | ✔                                 |
| High Dimensionality    | ✔ (sparse)                      | ✔ (sparse)                        |
| Semantic Context       | ✘                               | ✘                                 |
| Document Length Bias   | Yes (mitigated by TF normalization) | Yes (but lessened by TF and IDF) |

---

*Image context:*  
- Slide shows side‑by‑side matrices: raw count BoW vs. TF‑IDF weighted, illustrating how high-frequency terms shrink after weighting.
