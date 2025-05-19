## Problem Definition
Word Sense Disambiguation (WSD) is the task of automatically assigning the correct sense (meaning) to an ambiguous word in context.

- **Objective:** Given a target word \(w\) in a sentence or document, select the intended sense \(s \in S(w)\) from a predefined sense inventory.  
- **Example:**  
  - *bass* in “He played the bass at the concert.” → musical instrument sense.  
  - *bass* in “We caught a large bass.” → fish sense. :contentReference[oaicite:0]{index=0}:contentReference[oaicite:1]{index=1}  

### Why WSD Matters
- **Improves NLP tasks**: Machine translation, information retrieval, question answering.  
- **Reduces ambiguity**: Enables precise semantic representation.  

---

## Sense Inventories
Structured resources listing possible senses for each word.

- **Machine-Readable Dictionaries (MRDs):**  
  - Glosses and example sentences.  
  - Often limited coverage for modern usage.  
- **WordNet:**  
  - Synsets (sets of cognitive synonyms) grouped by meaning.  
  - Relations: hypernymy, hyponymy, meronymy.  
- **Custom Inventories:** Curated for domain-specific terms. :contentReference[oaicite:2]{index=2}:contentReference[oaicite:3]{index=3}  

---

## Core Approaches to WSD
1. **Knowledge-Based Methods**  
   - Rely on MRDs/ontologies, overlap & graph-based algorithms.  
2. **Supervised Methods**  
   - Train classifiers on sense-annotated corpora (SVMs, neural).  
3. **Unsupervised Methods**  
   - Induce senses by clustering contextual instances.  
4. **Semi-Supervised / Bootstrapping**  
   - Seed classifiers with small labeled data; iteratively expand.  
5. **Hybrid Methods**  
   - Combine knowledge-based and corpus-based signals for robustness.  

---

*Image context:*  
- Slide shows an ambiguous word “plant” with arrows pointing to senses “industrial facility” and “living organism,” illustrating the disambiguation decision.
