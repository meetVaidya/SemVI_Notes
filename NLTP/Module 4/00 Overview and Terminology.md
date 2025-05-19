## What Is Semantic Analysis in NLP?
Semantic analysis is the study of how machines interpret meaning in human language. Its objectives include:
- **Mapping words to meaning**: Determining the relationship between linguistic forms (words, phrases) and their intended concepts or entities.
- **Disambiguation**: Resolving which sense of a word is intended in a given context.
- **Inference & reasoning**: Enabling downstream tasks (e.g., question answering, summarization) to leverage semantic representations. :contentReference[oaicite:0]{index=0}:contentReference[oaicite:1]{index=1}

Two dominant frameworks:
1. **Formal Semantics**  
   - Uses logic (predicate calculus, λ‑calculus) to build truth-conditional models.  
   - Strength: precise, supports theorem proving.  
   - Weakness: brittle; rules can be hard to craft for natural variability.
2. **Distributional Semantics**  
   - Statistical approach: derives meaning from patterns of word co‑occurrence in large corpora.  
   - “You shall know a word by the company it keeps.” (Firth, 1957) :contentReference[oaicite:2]{index=2}:contentReference[oaicite:3]{index=3}  
   - Strength: robust to noise, data‑driven.  
   - Weakness: captures similarity, not logical structure.

---

## Fundamental Units: Words, Lemmas, Wordforms
Understanding the difference is crucial when preprocessing text.

| Unit      | Description                                                                         | Example                          |
|-----------|-------------------------------------------------------------------------------------|----------------------------------|
| **Word**  | Any orthographic token in text.                                                     | *runs*, *running*, *ran*         |
| **Lemma** | Canonical dictionary headword. All inflected forms map here.                        | *run* (covers *runs, running*)   |
| **Wordform** | Surface forms as they appear.                                                     | *went* (lemma: *go*) :contentReference[oaicite:4]{index=4}:contentReference[oaicite:5]{index=5} |

- **Why it matters**:  
  - Lemmatization groups forms to reduce sparsity.  
  - Retaining wordforms preserves morphological nuance (e.g., tense, number).

---

## Sense, Denotation & Connotation
Words often carry multiple, related or unrelated meanings.

### Sense
- A distinct meaning of a lemma.
- Polysemous words have multiple senses; homonyms have unrelated senses. :contentReference[oaicite:6]{index=6}:contentReference[oaicite:7]{index=7}

### Denotation
- Core, dictionary‐listed meaning.
- Example:  
  > “**Rose**: A woody perennial with fragrant flowers.” :contentReference[oaicite:8]{index=8}:contentReference[oaicite:9]{index=9}

### Connotation
- Subjective, context‑driven associations.
- Example:  
  > Calling someone a “**rose**” to imply beauty or delicacy. :contentReference[oaicite:10]{index=10}:contentReference[oaicite:11]{index=11}

---

## Sense Relations at a Glance
Visual taxonomy of how word senses can relate:

| Relation     | Definition                                                                               | Example                                      |
|--------------|------------------------------------------------------------------------------------------|----------------------------------------------|
| **Polysemy** | One word, multiple related senses.                                                       | *bank* → financial institution & building.   |
| **Homonymy** | One form, unrelated meanings (distinct etymologies).                                     | *bat* (animal) vs. *bat* (baseball). :contentReference[oaicite:12]{index=12}:contentReference[oaicite:13]{index=13} |
| **Synonymy** | Different words or phrases, similar meaning in context.                                  | *big* and *large* (though register may differ). |
| **Antonymy** | Direct opposites.                                                                        | *hot* vs. *cold*; *enter* vs. *exit*.        |
| **Hyponymy** | “Is‑A” relationship: specific → general.                                                 | *sparrow* is a hyponym of *bird*.            |
| **Meronymy** | Part‑whole relationship.                                                                 | *wheel* is a meronym of *car*. :contentReference[oaicite:14]{index=14}:contentReference[oaicite:15]{index=15} |

### Illustrative Test: The Zeugma Anomaly
- Sentence: “Does United serve breakfast and San Jose?”  
- Why it fails: “serve” applies to *breakfast* (offer food) but not to *San Jose* (a city). This mismatch flags multiple senses of “serve.” :contentReference[oaicite:16]{index=16}:contentReference[oaicite:17]{index=17}

---

*Image context:*  
- Title slide often shows a diagram contrasting formal vs. distributional semantics (e.g., a logic tree vs. a word‑cloud matrix).
