## Stemming

*   **Definition:** A process of reducing inflected (or sometimes derived) words to their word stem, base, or root form—generally a written word form.
*   **Method:** Typically involves crudely chopping off affixes (mostly suffixes) from the word's end based on a list of common affixes and rules.
*   **Output:** The "stem" may not be a real word or a linguistically correct root.
*   **Example:** `studies` → `studi`, `giving` → `giv`.
*   **Popular Algorithm:** Porter Stemmer.

(Image context slide 119: Disadvantages of stemming - indiscriminate cutting, `studies`->`studi`, `giving`->`giv`, `intelligence`->`intelligen`. Produced word may not have meaning.)

### Porter Stemmer Algorithm

A rule-based algorithm for stemming English words, involving five main steps applied sequentially. Within each step, if multiple rules match, the one with the longest suffix (S1) is applied.

**(Detailed Porter Stemmer rules are on slides 108-118 in PDF1 and slides 4-24 in PDF2. A summary is provided here.)**

**Key Definitions for Porter Stemmer:**
*   **Consonant (c), Vowel (v):** Standard definitions, with 'y' treated specially.
*   **C, V:** Sequences of one or more consonants/vowels.
*   **Measure (m):** In the form `[C](VC)^m[V]`, `m` is the count of `(VC)` pairs.
    *   `m=0`: TR, EE, TREE
    *   `m=1`: TROUBLE, OATS, TREES
    *   `m=2`: TROUBLES, PRIVATE
*   **Rule Format:** `(condition) S1 -> S2` (If stem meets condition, replace suffix S1 with S2).
*   **Condition Codes:** `*S` (ends in S), `*v*` (contains vowel), `*d` (ends in double consonant), `*o` (ends `cvc`, 2nd `c` not W,X,Y).

**Porter Stemmer Steps (Highly Abridged Summary):**

*   **Step 1a:** Handles plurals and `-s` endings (e.g., `caresses`→`caress`, `cats`→`cat`).
*   **Step 1b:** Handles `-eed`, `-ed`, `-ing`. Includes "cleaning" sub-steps if `-ed`/`-ing` removed (e.g., `agreed`→`agree`, `plastered`→`plaster`, then `conflat(ed)`→`conflate`).
*   **Step 1c:** Changes `y` to `i` if there's a vowel in the stem (e.g., `happy`→`happi`).
*   **Step 2:** Deals with a list of derivational suffixes, changing them if `m>0` (e.g., `ational`→`ate` as in `relational`→`relate`).
*   **Step 3:** Deals with another list of suffixes if `m>0` (e.g., `icate`→`ic` as in `triplicate`→`triplic`; `ness`→` ` as in `goodness`→`good`).
*   **Step 4:** Deals with a further list of suffixes, often if `m>1` (e.g., `ance`→` ` as in `allowance`→`allow`; `ive`→` ` as in `effective`→`effect`).
*   **Step 5a & 5b:** Tidying up, e.g., removing final `-e` if `m>1` or if `m=1` and not `*o` (e.g., `probate`→`probat`). Removes second `l` from `-ll` if `m>1` (e.g., `controll`→`control`).

**Advantage of Porter Stemmer:** Easy to understand and implement.
**Disadvantage:** Crude, can lead to non-words, over-stems or under-stems.

## Lemmatization

*   **Definition:** The process of grouping together the inflected forms of a word so they can be analyzed as a single item, identified by the word's **lemma** (dictionary form).
*   **Method:** Uses vocabulary and morphological analysis, often requiring Part-of-Speech (POS) tagging to resolve ambiguities.
*   **Output:** A real, dictionary word (the lemma).
*   **Example:** `studies` (verb) → `study`, `studies` (noun) → `study`. `better` → `good`.

## Stemming vs. Lemmatization Comparison

(Image context slide 120 & 121: Tables comparing Stemming and Lemmatization.)

| Feature                       | Stemming                                                              | Lemmatization                                                                    |
| :---------------------------- | :-------------------------------------------------------------------- | :------------------------------------------------------------------------------- |
| **Goal**                      | Reduce word to a "stem" (often by suffix stripping)                   | Reduce word to its dictionary form (lemma)                                       |
| **Output**                    | Stem (may not be a real word)                                         | Lemma (a real dictionary word)                                                   |
| **Example: `studies`**        | `studi`                                                               | `study`                                                                          |
| **Example: `giving`**         | `giv`                                                                 | `give`                                                                           |
| **Example: `caring`**         | `car`                                                                 | `care`                                                                           |
| **POS Tagging**               | Typically not required.                                               | Often requires POS tagging for accuracy.                                         |
| **Context Knowledge**         | Does not require context.                                             | May require sentence context.                                                    |
| **Complexity/Computational Power** | Simpler, less computationally intensive.                              | More complex, more computationally intensive (dictionary lookups, analysis).   |
| **Use for Dictionary**        | Stems not used for dictionaries.                                      | Lemmas are dictionary forms.                                                     |
| **Applications**              | Information Retrieval, Document Clustering, simpler NLP tasks.        | Machine Translation, Question Answering, more advanced NLP tasks.                |