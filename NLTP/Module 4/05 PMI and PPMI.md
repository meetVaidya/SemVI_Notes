## Pointwise Mutual Information (PMI)
PMI measures how much the actual co‑occurrence of a word \(w\) and context \(c\) deviates from what would be expected if they were independent.

- **Formula:**  
  \[
    \mathrm{PMI}(w,c) = \log \frac{P(w,c)}{P(w)\,P(c)}
  \]
  where  
  - \(P(w,c) = \frac{\text{count}(w,c)}{N}\)  
  - \(P(w) = \frac{\sum_{c'} \text{count}(w,c')}{N}\)  
  - \(P(c) = \frac{\sum_{w'} \text{count}(w',c)}{N}\)  
- **Interpretation:**  
  - PMI > 0 → \(w\) and \(c\) co‑occur more than chance → strong association.  
  - PMI < 0 → co‑occurrence less than chance → unlikely association.  
  - PMI = 0 → independence.  
- **Drawback:** Rare events can yield very high PMI, even if noise. :contentReference[oaicite:0]{index=0}:contentReference[oaicite:1]{index=1}  

---

## Positive PMI (PPMI)
To focus on informative, positive associations and avoid negative/low‑frequency noise, we define:

\[
  \mathrm{PPMI}(w,c) = \max\bigl(\mathrm{PMI}(w,c),\,0\bigr)
\]

- **Benefits:**  
  - Discards negative PMI values (no evidence of repulsion).  
  - Emphasizes meaningful co‑occurrences.  
- **Smoothing:**  
  - Add‑k smoothing (e.g., add‑1) on raw counts can prevent zero probabilities and dampen extreme PMI for extremely rare events.  
  - Column normalization or row normalization can further stabilize vector magnitudes. :contentReference[oaicite:2]{index=2}:contentReference[oaicite:3]{index=3}  

---

## PPMI vs. TF‑IDF Comparison

| Aspect                 | PPMI                                    | TF‑IDF                              |
|------------------------|-----------------------------------------|-------------------------------------|
| Basis                  | Probability ratios (word–context)       | Frequency × inverse document freq.  |
| Emphasis               | Strong local associations               | Globally rare but frequent in docs  |
| Handles negative info  | Negative values truncated to zero       | Doesn’t produce negative weights    |
| Sensitivity to rare   | High (mitigated via smoothing)          | Moderate (inversely down‑weights)   |
| Interpretability       | Direct measure of association strength  | Heuristic weight combining two factors |

---

## Example Calculation

Assume a small corpus with total \(N=1000\) tokens and counts:
- count(“cat”, “meow”) = 20  
- count(“cat”, *) total = 100  
- count(*, “meow”) total = 50  

1. \(P(\text{cat}, \text{meow}) = 20/1000 = 0.02\)  
2. \(P(\text{cat}) = 100/1000 = 0.10\)  
3. \(P(\text{meow}) = 50/1000 = 0.05\)  
4. \(\mathrm{PMI} = \log\frac{0.02}{0.10\times0.05} = \log(4) = 1.386\)  
5. \(\mathrm{PPMI} = \max(1.386,0) = 1.386\)  

---

## Practical Notes
- **When to use PPMI:** As input to SVD or clustering to obtain more discriminative low‑dimensional embeddings.  
- **Alternatives:** Shifted PPMI (SPPMI) subtracts a constant before truncation to curb the dominance of extremely frequent co‑occurrences.  
- **Implementation tips:**  
  - Compute probabilities from smoothed counts.  
  - Use sparse representations to handle large vocabularies efficiently.  
