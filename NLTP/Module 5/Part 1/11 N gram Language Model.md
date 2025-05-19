# N-Gram Language Models

## Introduction

An N-gram language model is a type of probabilistic language model that predicts the (N)<sup>th</sup> word in a sequence based on the **history** of the preceding `N-1` words.

*   **N-gram:** A contiguous sequence of N items (words, characters) from a given sample of text or speech.
*   **Goal:** To assign a probability to a sequence of words, or to predict the next word.

*   **Unigram Model (N=1):** Probability of a word is independent of context. P(w)
*   **Bigram Model (N=2):** Probability of a word depends on the single preceding word. P(w<sub>i</sub> | w<sub>i-1</sub>)
*   **Trigram Model (N=3):** Probability of a word depends on the two preceding words. P(w<sub>i</sub> | w<sub>i-2</sub>, w<sub>i-1</sub>)

**Examples:**
1.  "He is going to _____"
    *   Predicting the 5<sup>th</sup> word based on "He is going to" uses a **5-gram** model.
2.  "going to _____"
    *   Predicting the 3<sup>rd</sup> word based on "going to" uses a **trigram** model.

## Applications of N-Grams

N-gram models are fundamental in many NLP applications:

1.  **Optical Character Recognition (OCR):**
    *   Helps predict or correct missing/unclear words based on context.
2.  **Grammar and Spelling Correction:**
    *   Suggests corrections for misspelled words based on contextual probability.
    *   Identifies correctly spelled but contextually wrong words (e.g., "Deer sir" vs. "Dear sir").
3.  **Speech to Text (Automatic Speech Recognition - ASR):**
    *   Disambiguates homophones (e.g., "Eye am Fine" vs. "I am Fine"; N-grams favor the latter).
4.  **Machine Translation:**
    *   Helps choose appropriate synonyms to improve fluency by considering word sequences.
    *   E.g., "He is **biggest** minister of Pakistan" → "He is **Prime** minister..."
5.  **Text Prediction/Suggestion:**
    *   Used in mobile keyboards, search engines for suggesting the next word(s).

## Probability in N-gram Models

Language models aim to determine the probability of a sequence of words.
*   A meaningful sentence like "He is going to school" should have a higher probability than a nonsensical one like "He school is to going".

**Chain Rule of Probability:**
The joint probability of a sequence of words P(w<sub>1</sub>, w<sub>2</sub>, ..., w<sub>k</sub>) can be decomposed as:
P(w<sub>1</sub>, ..., w<sub>k</sub>) = P(w<sub>1</sub>) * P(w<sub>2</sub>|w<sub>1</sub>) * P(w<sub>3</sub>|w<sub>1</sub>,w<sub>2</sub>) * ... * P(w<sub>k</sub>|w<sub>1</sub>, ..., w<sub>k-1</sub>)

**Example:**
P(He is going to school) = P(He) * P(is|He) * P(going|He is) * P(to|He is going) * P(school|He is going to)

**Markov Assumption:**
Calculating probabilities based on the entire preceding history is computationally complex and suffers from data sparsity (many long sequences will never have been observed).
N-gram models simplify this by making a **Markov assumption**: the probability of a word depends only on a fixed number (N-1) of preceding words.

*   For a **bigram model (N=2)**:
    P(w<sub>i</sub> | w<sub>1</sub>, ..., w<sub>i-1</sub>) ≈ P(w<sub>i</sub> | w<sub>i-1</sub>)
*   For a **trigram model (N=3)**:
    P(w<sub>i</sub> | w<sub>1</sub>, ..., w<sub>i-1</sub>) ≈ P(w<sub>i</sub> | w<sub>i-2</sub>, w<sub>i-1</sub>)

This approximation makes the model tractable by reducing the length of the context ("Looking back so much" - slide 124) considered for prediction.