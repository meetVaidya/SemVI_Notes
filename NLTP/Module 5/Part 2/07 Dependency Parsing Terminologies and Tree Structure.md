Sentence: ‘I prefer the morning flight through Denver’

"prefer" is the root.
- "I" is `nsubj` (nominal subject) of "prefer".
- "flight" is `dobj` (direct object) of "prefer".
- "the" is `det` (determiner) of "flight".
- "morning" is `nmod` (nominal modifier) of "flight".
- "Denver" is `nmod` (nominal modifier) of "flight" (or "prefer" depending on attachment, here shown modifying flight via "through").
- "through" is `case` (case marker) for "Denver" in relation to "flight".)

## Key Terminologies

1.  **Head-Dependent**:
    *   In the arrows representing a relationship, the origin word is the **Head** and the destination word is the **Dependent**.
    *   The arrow points from the Head to the Dependent.
    *   Example: In `(I, ‘nsubj’, prefer)`, ‘prefer’ is the Head & ‘I’ is the Dependent. (Note: Conventionally, arrows often point from head to dependent, but some visualizations might differ. The example implies 'prefer' governs 'I'). The provided image for "I prefer..." shows arrows from head to dependent.

2.  **Root**:
    *   The word which is the root of the parse tree. It is the ultimate head of the sentence and does not depend on any other word.
    *   In the example ‘I prefer the morning flight through Denver’, ‘prefer’ is the Root.

3.  **Grammar Functions and Arcs (Dependency Relations/Labels)**:
    *   The **tags** (labels) on the arcs between each Head-Dependent pair are grammar functions that determine the type of relationship.
    *   The **arrowhead carrying the tag** is called an Arc.

### Examples of Grammar Functions (Dependency Relations)

(Image context: A table listing "Clausal Argument Relations", "Nominal Modifier Relations", and "Other Notable Relations" with their descriptions.)

| Category                    | Relation | Description                                      |
|-----------------------------|----------|--------------------------------------------------|
| **Clausal Argument Relations** | NSUBJ    | Nominal subject                                  |
|                             | DOBJ     | Direct object                                    |
|                             | IOBJ     | Indirect object                                  |
|                             | CCOMP    | Clausal complement                               |
|                             | XCOMP    | Open clausal complement                          |
| **Nominal Modifier Relations**| NMOD     | Nominal modifier                                 |
|                             | AMOD     | Adjectival modifier                              |
|                             | NUMMOD   | Numeric modifier                                 |
|                             | APPOS    | Appositional modifier                            |
|                             | DET      | Determiner                                       |
|                             | CASE     | Prepositions, postpositions and other case markers |
| **Other Notable Relations**   | CONJ     | Conjunct                                         |
|                             | CC       | Coordinating conjunction                         |

(Image context: A table showing examples for various relations, highlighting the head and dependent words in example sentences.)
Examples:
*   **NSUBJ**: United **canceled** the *flight*. (canceled -> United)
*   **DOBJ**: United diverted the **flight** to *Reno*. (flight -> Reno, or diverted -> flight) - The example shows "United diverted the **flight** to Reno." with flight as dependent. A better example: "She reads **books**." (reads -> books)
*   **IOBJ**: We booked **her** the *flight* to Miami. (booked -> her)
*   **NMOD**: We took the **morning** *flight*. (flight -> morning)
*   **AMOD**: Book the **cheapest** *flight*. (flight -> cheapest)
*   **DET**: **The** *flight* was canceled. (flight -> The)
*   **CASE**: Book the flight **through** *Houston*. (Houston -> through, or flight -> through depending on what "through Houston" modifies)

## Understanding the Dependency Parse Tree

*   Dependencies are represented as a **directed graph G = (V, A)**.
    *   **V (set of vertices)**: Represents words (and punctuation marks) in the sentence.
    *   **A (set of arcs)**: Represents the grammar relationships (dependencies) between elements of V.

### Features of a Dependency Parse Tree

A dependency parse tree (as a directed graph) has the following features:
1.  **Root has no Incoming arcs**: The Root can only be a Head in a Head-Dependent pair. It does not depend on any other word.
2.  **Single Head/Parent**: Vertices (except the Root) should have only one incoming arc. This means each word (except the root) has exactly one head.
3.  **Unique Path from Root**: A unique path should exist between the Root and each vertex (word) in the tree.
4.  **Acyclicity**: The graph must be acyclic.

## Projectivity

*   **Projective Arc**: An arc/arrow (with its tag) is projective if the 'Head' associated with the arc has a path to reach *every word that lies linearly between the Head and the Dependent* in the sentence.

(Image context: A dependency parse tree for "United canceled the morning flights to Houston".
`canceled` is root.
`canceled` -> `United` (nsubj)
`canceled` -> `flights` (dobj)
`flights` -> `the` (det)
`flights` -> `morning` (nmod)
`flights` -> `Houston` (nmod)
`Houston` -> `to` (case)
)

### Explanation of Projectivity

*   **Example 1**: Arc between ‘the’ & ‘flights’ (`flights` -> `the`).
    *   Head: ‘flights’, Dependent: ‘the’.
    *   Word(s) between them: ‘morning’.
    *   Path from ‘flights’ to ‘morning’: `flights` -> `morning`.
    *   Since ‘flights’ (Head) can reach ‘morning’ (word between Head & Dependent), the arc (`flights` -> `the`) is **projective**.

*   **Example 2**: Arc between ‘canceled’ & ‘flights’ (`canceled` -> `flights`).
    *   Head: ‘canceled’, Dependent: ‘flights’.
    *   Words between them: ‘the’, ‘morning’.
    *   Path from ‘canceled’ to ‘the’: `canceled` -> `flights` -> `the`.
    *   Path from ‘canceled’ to ‘morning’: `canceled` -> `flights` -> `morning`.
    *   Since ‘canceled’ (Head) can reach both ‘the’ and ‘morning’, the arc (`canceled` -> `flights`) is **projective**.

### Projective and Non-Projective Parse Trees

*   **Projective Parse Tree**: A parse tree where all its arcs are projective. The example tree "United canceled the morning flights to Houston" is projective.
*   **Non-Projective Parse Tree**: A tree with at least one non-projective arc. These often occur with long-distance dependencies or certain constructions like relative clauses.