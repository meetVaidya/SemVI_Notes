Rule-based POS tagging is one of the oldest approaches. It relies on a dictionary (or lexicon) and a set of handwritten rules to assign POS tags to words.

## Core Components

(Image context: A handwritten diagram showing the flow: Input -> Tag Dictionary or Lexicon -> Handwritten rules -> output (Word,tag).)

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

## Rules Based on Context

Rules often rely on the context of the ambiguous word.

(Image context: Two diagrams. First shows "Book" (Wn) with arrows from a preceding word (Wn-1) and to a following word (Wn+1). Second shows "Book" with arrows from a preceding tag (Tn-1) and to a following tag (Tn+1).)

*   **Example 1: "Please book that flight"**
    *   Rule-1: `if (the previous word is “to”) then eliminate all Noun tags` (e.g., for "to book").
*   **Example 2: "I bought a Book."**
    *   Rule-2: `if (the previous tag is an article) then eliminate all verb tags`.

### Applying Rules - Eliminating Some POS

(Image context: A sentence "She promised to back the bill" with potential tags. An arrow points from JJ to VB for "back", indicating JJ is eliminated. The rule "Eliminate VBN if VBD is an option when VBN|VBD follows “<start> PRP”" is mentioned.)

Example: "She promised to back the bill"
Initial tags might be:
*   She: PRP
*   promised: VBD
*   to: TO
*   back: VB, NN, RB, JJ (ambiguous)
*   the: DT
*   bill: NN

A rule like "If 'back' follows 'to' (infinitival 'to'), prefer VB" would help disambiguate 'back'.

## Summary of Rule-Based Tagger Characteristics

*   It is the oldest approach and uses handwritten rules for tagging.
*   Depends on a dictionary or lexicon to get possible tags for each word.
*   Language experts create rules based on symbol patterns and linguistic features.
*   Handwritten rules are used to identify the correct tag when a word has more than one possible tag.
*   Disambiguation is done by analyzing the linguistic features of the word, its preceding word, following word, and other aspects.

## Example: University Corpus

*   Sentence: "I want to read a **book**."
*   "Book" can be Noun or Verb.
*   Rule: "Before **book**, determiner (a) is there, therefore it is a noun."

## Limitations of Rule-Based Approach

*   **Hard-coded rules are required**: This is labor-intensive and requires significant linguistic expertise.
*   **Rules need updates**: Rules have to be updated based on language change and evolution.
*   **Inefficiency**: It needs to check the lexicon every time, which can be inefficient for large texts.
*   **Expert team required**: A strong team of language experts is necessary to develop and maintain the rules.
*   Difficult to cover all linguistic nuances and exceptions.