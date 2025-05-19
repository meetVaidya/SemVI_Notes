## Constituency Parsing (Syntactic Parsing)

*   **Definition**: Syntactic parsing (often referring to constituency parsing when CFGs are involved) is the task of assigning a syntactic structure (typically a parse tree) to a sentence, according to a given grammar.
*   The problem of mapping from a string of words to its parse tree is called **syntactic parsing**.

### Applications of Parse Trees

*   **Grammar Checking**: Sentences that cannot be parsed by a grammar may have grammatical errors or be hard to read.
*   **Semantic Analysis**: Parse trees can serve as an intermediate stage of representation for semantic analysis, helping to determine "who did what to whom."

## Ambiguity

A sentence is ambiguous if it can be assigned more than one syntactic structure (parse tree) by the grammar.

*   **Two types of ambiguity relevant to parsing**:
    1.  **POS Ambiguity**: A word can have multiple parts of speech (e.g., "book" as noun or verb). This is typically resolved by POS taggers before or during parsing.
    2.  **Structural Ambiguity**: Occurs when the grammar can assign more than one parse tree to a sentence, even if the POS tags are resolved. This means words can be legitimately combined in different ways.

### Example of Structural Ambiguity

Sentence: "I shot an elephant in my pajamas." (Groucho Marx)

This sentence has two common interpretations, leading to two different parse trees:
![[Pasted image 20250519204833.png]]

*   **Parse 1 (Left tree - humorous)**: The Prepositional Phrase "in my pajamas" modifies "elephant". (The elephant was wearing the pajamas).
    *   Structure: `NP → Nominal PP` (where Nominal is "elephant")
*   **Parse 2 (Right tree - intended/Captain Spaulding)**: The Prepositional Phrase "in my pajamas" modifies the action "shot an elephant". (The speaker, "I", was wearing the pajamas while shooting).
    *   Structure: `VP → VP PP` (where VP is "shot an elephant")

### Types of Structural Ambiguity

Two common kinds of structural ambiguity are attachment ambiguity and coordination ambiguity.

1.  **Attachment Ambiguity**:
    *   Occurs if a particular constituent (like a PP or adverbial phrase) can be attached to the parse tree at more than one place.
    *   The "elephant in my pajamas" sentence is an example of **PP-attachment ambiguity**.
    *   Adverbial phrases are also subject to this.
    *   Example: "We saw the Eiffel Tower flying to Paris."
        *   Does "flying to Paris" describe the Eiffel Tower (Eiffel Tower was flying)? (Attaches to NP "the Eiffel Tower")
        *   Or does it describe how "we saw" it (We were flying to Paris when we saw it)? (Attaches to VP "saw the Eiffel Tower")

2.  **Coordination Ambiguity**:
    *   Occurs when phrases are conjoined by a conjunction like "and", and the scope of the conjunction is unclear.
    *   Example: "old men and women"
        *   Can be bracketed as `[old [men and women]]`: refers to old men and old women. (Both men and women are old).
        *   Can be bracketed as `[[old men] and [women]]`: refers to old men and (any age) women. (Only the men are old).
    *   Example: "John and Mary or Bill"
        *   `(John and Mary) or Bill`
        *   `John and (Mary or Bill)`