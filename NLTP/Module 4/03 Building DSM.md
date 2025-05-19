## Vector Space Model Overview
Distributional Semantic Models (DSMs) embed words into a high‑dimensional **semantic space**, where each dimension corresponds to a context feature.

- **Semantic space**  
  - Dimensions = context units (e.g., words, documents, syntactic roles).  
  - Each target word \(w\) → vector \(\mathbf{v}_w = [f(w,c_1), f(w,c_2), \dots, f(w,c_k)]\). :contentReference[oaicite:0]{index=0}:contentReference[oaicite:1]{index=1}  
- **Interpretation:** Closer vectors → more similar distributional profiles → more semantically similar.  

---

## Defining Contexts
Choice of context critically shapes the resulting space.

1. **Document-level**  
   - Context = entire document.  
   - Word×Document co‑occurrence matrix.  
   - Captures topical similarity.  
2. **Window-based**  
   - Context = fixed window of ± n words around target.  
   - Word×Word matrix within window.  
   - Captures syntagmatic relations (collocations). :contentReference[oaicite:2]{index=2}:contentReference[oaicite:3]{index=3}  
3. **Syntactic relations**  
   - Context = grammatical roles (subject, object).  
   - More precise relation modeling (e.g., subject–verb).  
   - Requires parsed corpus.

---

## Constructing the Co‑occurrence Matrix
Step‐by‐step guide to raw count matrix construction:

1. **Select target vocabulary**  
   - Often top \(V\) most frequent words to control dimensionality.  
2. **Select context vocabulary**  
   - May mirror target set or include function words if informative.  
3. **Define window shape & size**  
   - E.g., symmetric window of size 5 (± 5 tokens).  
4. **Count co‑occurrences**  
   - For each occurrence of target \(w\), increment count for each context \(c\) within window.  
5. **Result:** Raw count matrix \(M\in\mathbb{R}^{|V|\times|C|}\) where  
   \[
     M_{w,c} = \text{Number of times }c\text{ occurs near }w.
   \]

---

## Weighting & Smoothing
Raw counts often skewed by high‐frequency words; weighting and smoothing mitigate this.

- **Weighting schemes**  
  - **PPMI (Positive PMI):** Emphasizes informative co‑occurrences, zeros out negative association strengths.  
  - **TF‑IDF:** Balances term frequency in context vs. global rarity.  
- **Smoothing**  
  - **Add‑n smoothing:** Add constant \(n\) to counts to avoid zeros.  
  - **Row/column normalization:** Scales vectors to unit length or unit sum. :contentReference[oaicite:4]{index=4}:contentReference[oaicite:5]{index=5}  

---

## Dimensionality Reduction
High dimensionality can be computationally expensive and noisy.

- **Singular Value Decomposition (SVD)**  
  - Factorize \(M\approx U\Sigma V^\top\); retain top \(k\) singular values.  
  - Yields dense, lower‑dimensional embeddings (e.g., Latent Semantic Analysis).  
- **Neural Embeddings**  
  - Word2Vec, GloVe learn low‑dimensional vectors directly via prediction or reconstruction objectives.  
  - Often yield superior semantic clusters.

---

## Example Workflow
1. **Corpus selection:** 100 million token news corpus.  
2. **Preprocessing:**  
   - Tokenize, lowercase, remove punctuation, optional lemmatize.  
3. **Context extraction:** ± 4 token window.  
4. **Matrix build:** Raw counts → apply PPMI.  
5. **Dimensionality reduction:** SVD to 300 dimensions.  
6. **Evaluation:**  
   - Compute cosine similarity for known pairs (e.g., *king* vs. *queen*).  
   - Use in downstream tasks (clustering, classification).

---

*Image context:*  
- Slide diagram showing co‑occurrence matrix heatmap (rows = target words, columns = context words), with bright cells indicating high counts.
