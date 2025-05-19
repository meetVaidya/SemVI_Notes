## Computational Semantics vs. Distributional Semantics  
- **Computational Semantics** aims to build and reason with precise meaning representations (e.g., λ-calculus) so that sentences can be evaluated for truth or entailment.  
- **Distributional Semantics** derives word meaning statistically, by observing how words co-occur in large corpora. It forgoes explicit logic in favor of “meaning as usage” :contentReference[oaicite:0]{index=0}:contentReference[oaicite:1]{index=1}.  

## The Distributional Hypothesis  
- **Core idea:** “Words that occur in similar contexts tend to have similar meanings.”  
  - Wittgenstein (1953): “The meaning of a word is its use in language.”  
  - Firth (1957): “You shall know a word by the company it keeps.”  
  - Harris (1968): Difference in distribution correlates with difference in meaning. :contentReference[oaicite:2]{index=2}:contentReference[oaicite:3]{index=3}  

## Linguistic vs. Cognitive Perspectives  
- **Linguistic perspective:** Meaning distinctions emerge from measurable distributional differences—if words A and B have more similar distributions than A and C, A and B are semantically closer. :contentReference[oaicite:4]{index=4}:contentReference[oaicite:5]{index=5}  
- **Cognitive perspective:** Each word’s meaning is an abstract mental representation built over many contexts. Novel words (e.g., “wampimuk”) are learned via contextual cues. :contentReference[oaicite:6]{index=6}:contentReference[oaicite:7]{index=7}  

## Distributional Semantic Models (DSMs)  
1. **Define target vocabulary:** The words whose meanings we wish to model (e.g., “car,” “apple,” “bank”).  
2. **Choose context units:**  
   - **Documents** (Word × Document matrix)  
   - **Fixed windows** around each target (Word × Word within ±n words)  
   - **Syntactic relations** (e.g., subject–verb) :contentReference[oaicite:8]{index=8}:contentReference[oaicite:9]{index=9}  
3. **Count or weight co-occurrences:** Fill a matrix F where each cell f(w,c) is a raw count or a weighted score (e.g., PPMI, TF-IDF).  
4. **Optionally reduce dimensionality:** Using SVD, PCA, or neural embeddings (Word2Vec, GloVe).  

## Semantic Space and Vector Representations  
- **Semantic space:** A high-dimensional vector space whose axes correspond to context features.  
- **Word vectors:** Each word w is represented as a vector **v**₍w₎ = [f(w,c₁), f(w,c₂), …, f(w,cₖ)] :contentReference[oaicite:10]{index=10}:contentReference[oaicite:11]{index=11}.  
- **Similarity metrics:**  
  - **Dot product:** ⟨**u**,**v**⟩ sensitive to vector length.  
  - **Cosine similarity:** ⟨**u**,**v**⟩ / (‖**u**‖·‖**v**‖), normalizes magnitude, yields [0,1] for non-negative spaces. :contentReference[oaicite:12]{index=12}:contentReference[oaicite:13]{index=13}  

## Building a DSM: Step by Step  
1. **Select corpus** (size matters: millions of tokens for robust statistics).  
2. **Preprocess** (tokenization, lowercasing, stop‐word removal, optional lemmatization).  
3. **Extract contexts** per target word: sliding window or syntactic parses.  
4. **Populate co-occurrence matrix** with raw counts or smoothed counts (e.g., add-n) :contentReference[oaicite:14]{index=14}:contentReference[oaicite:15]{index=15}.  
5. **Transform weights** (PMI, PPMI, TF-IDF) to emphasize informative associations.  
6. **Compute similarities** or feed into downstream models (e.g., clustering, classification).

---

*Image context:*  
- Diagram illustrating a target word “bank” in the center, with surrounding context words “loan,” “river,” “money,” “water” placed in a 2-D semantic space according to cosine proximity.  
