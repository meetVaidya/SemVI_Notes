Morphological analysis is the first stage in many NLP pipelines, focusing on the internal structure of words. It studies how words are formed from smaller meaningful units called morphemes.

*   **Level of Analysis:** Word-Level Analysis.
*   **Focus:** Studies the structure of words or the formation of words. It examines how words are built from smaller pieces (morphemes).
*   **Key Tasks:**
    *   Identification and analysis of root words (stems).
    *   Identification and analysis of affixes (prefixes and suffixes).

## Examples of Morphological Decomposition
*   **Washing:** `wash` (root) + `ing` (suffix)
*   **Browser:** `Browse` (root) + `er` (suffix)
*   **Incomplete:** `In` (prefix) + `Complete` (root)

## Key Sub-Tasks in Morphological Analysis

### 1. Tokenization
Tokenization is the process of breaking down a stream of text into smaller units called tokens (usually words or punctuation marks).

*   **Example:**
    > John ate the pizza!!
    Tokens: `John`, `ate`, `the`, `pizza`, `!`, `!`

### 2. Stop Word Removal
This process involves removing common words (stop words) that occur frequently across documents but typically do not carry significant meaning for analysis. Articles (a, an, the), prepositions (in, on, at), and pronouns (he, she, it) are often classified as stop words.

*   **Example (after tokenization of "John ate the pizza!!"):**
    *   Tokens: `John`, `ate`, `the`, `pizza`, `!`, `!`
    *   After Stop Word Removal (assuming 'the', '!' are stop words for this context): `John`, `ate`, `pizza`
    *(Image context: The tokens "John", "ate", "the", "pizza", "!", "!" are shown. An arrow points down from this set to a smaller set of tokens: "John", "ate", "pizza", indicating removal of "the" and "!!")*

### 3. Stemming
Stemming is a process of reducing inflected (or sometimes derived) words to their word stem, base, or root form. It's often a heuristic process that chops off the ends of words.

*   **Definition:** A process of reducing words into its base form (Root form/stem form).
*   **Process:** Converting an inflected word to its word stem.
*   **Examples:**
    *   `John` -> `John`
    *   `Ate` -> `eat` (Note: This example shows a more sophisticated stemming or lemmatization, as simple Porter stemmer might give 'ate')
    *   `Pizza` -> `Pizza`
    *   `car`, `cars` -> `car`
    *   `run`, `ran`, `running` -> `run`
    *   `stemmer`, `stemming`, `stemmed` -> `stem`

### 4. Lemmatization
Lemmatization is the process of grouping together the inflected forms of a word so they can be analyzed as a single item, identified by the word's lemma (dictionary form). It typically requires a dictionary and morphological analysis of words.

*   **Definition:** A text normalization technique used for Natural Language Processing (NLP).
*   **Function:** It can convert any word's inflections to its base root form (lemma).
*   **Example:**
    *   `Playing`, `Plays`, `Played` -------> `Play` (Common root form "play")

### Stemming vs. Lemmatization

*(Image context for Slide 19: A diagram visually contrasts stemming and lemmatization.
Stemming: "studies", "studying" -> (remove suffixes) -> "studi", "study".
Lemmatization: "studies", "studying" -> (Grammatical information) -> "study", "study".)*

| S.No | Feature         | Stemming                                                                    | Lemmatization                                                                    |
| :--- | :-------------- | :-------------------------------------------------------------------------- | :------------------------------------------------------------------------------- |
| 1    | **Speed/Context** | Faster; chops words without knowing the context in given sentences.         | Slower; knows the context of the word before proceeding.                         |
| 2    | **Approach**    | Rule-based approach.                                                        | Dictionary-based approach.                                                       |
| 3    | **Accuracy**    | Accuracy is less.                                                           | Accuracy is more as compared to Stemming.                                        |
| 4    | **Meaning**     | May create non-existent words or incorrect meanings when converting to root. | Always gives a dictionary-meaningful word while converting into root form.       |
| 5    | **Use Case**    | Preferred when the meaning of the word is not important (e.g., Spam Detection). | Recommended when the meaning of the word is important (e.g., Question Answering). |
| 6    | **Example**     | "Studies" => "Studi"                                                        | "Studies" => "Study"                                                             |

### 5. N-Gram Language Model (as part of Morphological/Lexical Analysis)
While N-gram models are more broadly language models, their generation involves breaking text into sequences of N items (words/tokens), which is a lexical-level operation.

*   **Definition:** An N-gram is a contiguous sequence of N items from a given sample of text or speech. The items can be phonemes, syllables, letters, words, or base pairs according to the application.
*   **Examples (for "John Ate the Pizza"):**
    *   **1-gram (Unigram):** `John`, `Ate`, `the`, `Pizza`
    *   **Bigram (2-gram):** `John Ate`, `Ate the`, `the Pizza`
    *   **Trigram (3-gram):** `John Ate the`, `Ate the Pizza`
    *   **4-Gram:** `John Ate the Pizza`
*   **Application Example (Prediction):**
    > John Ate the _?_
    N-gram models can help predict the next word.