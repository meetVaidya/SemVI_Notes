Dependency parsing is a method used to analyze the grammatical structure of a sentence by establishing relationships between "head" words and words which modify or depend on them.
## What is Dependency Parsing?
*   Dependency parsing helps build a parsing tree where **directed arcs** represent the grammatical relationships (dependencies) between words.
*   It determines the relationship between words using **tags** (dependency labels) on these arcs.
*   It focuses on the relationships *in the sentence* rather than relying heavily on predefined grammar rules like traditional syntactic parsing (constituency parsing).
*   This approach offers flexibility, especially when the order of words changes (e.g., ‘boy handsome’ vs. ‘handsome boy’).
*   **Example Structure**:
    *   `sees` (root)
        *   `subject` -> `John`
        *   `object` -> `Bill`