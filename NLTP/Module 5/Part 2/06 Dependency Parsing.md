Dependency parsing is a method used to analyze the grammatical structure of a sentence by establishing relationships between "head" words and words which modify or depend on them.

## Motivation

*   **Word Order Freedom**: In some languages, the same statement can be written with different word orders. A word-to-word translation into English might yield unusual structures (e.g., "He is standing wall behind" instead of "He is standing behind the wall"). This indicates that the word order is relatively free.
*   **Adjective Placement**: It isn't always necessary for an adjective to appear just before the noun it modifies (e.g., "Handsome boy" vs. "Boy handsome" might be possible in some languages or contexts).
*   **Problem with Rule-Based Parsing**: For languages with free word order, using strict rules (like those in some constituency grammars) for parsing can be problematic because the rules might be too rigid to handle variations.
*   **Need for Dependency Parsing**: Dependency parsing is required to handle these complexities by focusing on word-to-word dependencies rather than phrasal constituents.

## What is Dependency Parsing?

*   Dependency parsing helps build a parsing tree where **directed arcs** represent the grammatical relationships (dependencies) between words.
*   It determines the relationship between words using **tags** (dependency labels) on these arcs.
*   It focuses on the relationships *in the sentence* rather than relying heavily on predefined grammar rules like traditional syntactic parsing (constituency parsing).
*   This approach offers flexibility, especially when the order of words changes (e.g., ‘boy handsome’ vs. ‘handsome boy’).

(Image context: A simple dependency tree for "John sees Bill". "sees" is the root. "John" is the subject of "sees", and "Bill" is the object of "sees". Arrows point from "sees" to "John" and from "sees" to "Bill".)

*   **Example Structure**:
    *   `sees` (root)
        *   `subject` -> `John`
        *   `object` -> `Bill`