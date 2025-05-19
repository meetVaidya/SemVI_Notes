Rule-based POS tagging is one of the oldest approaches. It relies on a dictionary (or lexicon) and a set of handwritten rules to assign POS tags to words.

## Core Components:
![[Pasted image 20250519183912.png]]
1.  **Input**: A sentence.
2.  **Tag Dictionary/Lexicon**:
    *   Used to assign all possible POS tags to the words in the given sentence.
    *   Example: For the word "play", the dictionary might list both Noun and Verb as possible tags.
        *   "I play cricket everyday" (Play is Verb)
        *   "I want to perform a play" (Play is Noun)
3.  **Handwritten Rules (Disambiguation Rules)**:
    *   These rules are crafted by language experts to resolve ambiguities when a word has multiple possible tags.
    *   They analyze linguistic features of the word, its preceding word, following word, and other contextual aspects.
    *   Example Rule: An ambiguous word is a noun if it follows a determiner (e.g., "a book" - 'book' is a noun because it follows 'a').

## Two-Stage Process

The rule-based approach typically involves two main stages:

*   **Stage 1: Dictionary Lookup**
    1.  Start with a dictionary containing words and their possible POS tags.
    2.  Assign all possible tags to each word in the input sentence based on the dictionary.

*   **Stage 2: Rule Application**
    1.  Write rules by hand to selectively remove incorrect tags.
    2.  The process stops when each word has exactly one (correct) tag.

### Example of Rule-Based Tagging Stages

Consider the sentence: **"He had a fly."**

*   **The first stage (Dictionary Lookup):**
    *   he  -> Pronoun
    *   had -> Verb
    *   a   -> Article
    *   fly -> Verb, Noun (ambiguous)

*   **The second stage (Rule Application):**
    *   Apply rule: `if (the previous tag is an article) then eliminate all verb tags`
    *   Result:
        *   he  -> Pronoun
        *   had -> Verb
        *   a   -> Article
        *   fly -> Noun (Verb tag eliminated)

## Limitations of Rule-Based Approach
*   **Hard-coded rules are required**: This is labor-intensive and requires significant linguistic expertise.
*   **Rules need updates**: Rules have to be updated based on language change and evolution.
*   **Inefficiency**: It needs to check the lexicon every time, which can be inefficient for large texts.
*   **Expert team required**: A strong team of language experts is necessary to develop and maintain the rules.
*   Difficult to cover all linguistic nuances and exceptions.