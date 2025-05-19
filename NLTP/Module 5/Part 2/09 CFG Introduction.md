Context-Free Grammars (CFGs) are fundamental in modeling the syntax of natural languages and computer languages. They form the backbone of many formal models of syntax.

## Role of CFGs

CFGs play a role in many computational applications, including:
*   Grammar checking
*   Semantic interpretation
*   Dialogue understanding
*   Machine translation

They can express sophisticated relations among words in a sentence and are computationally tractable enough for efficient parsing algorithms.

## Constituency

*   **Syntactic Constituency**: The idea that **groups of words can behave as single units**, or constituents.
    *   Example: A group of words can come together to form a Noun Phrase (NP).
*   Developing a grammar involves building an inventory of the constituents in the language.

### How Words Group Together in English

*   **Noun Phrase (NP)**: A sequence of words surrounding at least one noun.
    (Image context: A blue box with examples of Noun Phrases: "Harry the Horse", "the Broadway coppers", "they", "a high-class spot such as Mindy's", "the reason he comes into the Hot Box", "three parties from Brooklyn".)
    Examples of Noun Phrases:
    *   "Harry the Horse"
    *   "the Broadway coppers"
    *   "they"
    *   "a high-class spot such as Mindy's"
    *   "the reason he comes into the Hot Box"
    *   "three parties from Brooklyn"

*   **Evidence for Constituents**: One piece of evidence that these groups form constituents is that they can all appear in similar syntactic environments.
    *   For example, Noun Phrases can often appear before a verb:
        (Image context: A blue box showing NP examples followed by verbs: "three parties from Brooklyn *arrive*...", "a high-class spot such as Mindy's *attracts*...", "the Broadway coppers *love*...", "they *sit*")
        *   "three parties from Brooklyn *arrive*..."
        *   "a high-class spot such as Mindy's *attracts*..."
        *   "the Broadway coppers *love*..."
        *   "they *sit*"

*   **Individual words vs. Whole Phrase**: While the whole noun phrase can occur before a verb, this is not necessarily true for each individual word within the noun phrase if taken out of context.
    (Image context: A blue box showing ungrammatical fragments marked with an asterisk: "*from arrive...", "*as attracts...", "*the is...", "*spot sat...")
    Ungrammatical examples (if parts of NPs are used alone):
    *   `*from arrive...` (from "three parties *from* Brooklyn")
    *   `*as attracts...` (from "a high-class spot such *as* Mindy's")

### Pre-posed or Post-posed Constructions

Constituents can often be moved within a sentence.
*   Example: The prepositional phrase "on September seventeenth" can be placed in different locations:
    (Image context: Examples showing the PP "on September seventeenth" in different positions in the sentence "I'd like to fly from Atlanta to Denver".)
    *   **On September seventeenth**, I’d like to fly from Atlanta to Denver. (preposed)
    *   I’d like to fly **on September seventeenth** from Atlanta to Denver.
    *   I’d like to fly from Atlanta to Denver **on September seventeenth**. (postposed)

*   However, the individual words making up the phrase cannot be arbitrarily moved:
    *   `*On September, I’d like to fly seventeenth from Atlanta to Denver`
    *   `*I’d like to fly on September from Atlanta to Denver seventeenth`

## Common Phrase Types

*   **Verb Phrase (VP)**: In English, consists of a verb followed by assorted other things.
    *   Verb followed by a Noun Phrase (NP): e.g., "prefer a morning flight" (verb NP)
    *   Verb followed by a Prepositional Phrase (PP): e.g., "leaving on Thursday" (verb PP)
    *   Verb followed by an NP and a PP: e.g., "leave Boston in the morning" (verb NP PP)

*   **Adjective Phrase (AP)**:
    *   Adjectives can be grouped into an Adjective Phrase.
    *   APs can have an adverb before the adjective.
        *   Example: "the **least expensive** fare" (Adverb + Adjective)

## Context-Free Grammars (CFG)

*   A **formal system** for modeling constituent structure in English and other natural languages.
*   Also called **Phrase-Structure Grammars**.
*   A CFG consists of a set of **rules or productions**.
    *   These rules express the ways that symbols of the language can be grouped and ordered together.
    *   It also includes a **lexicon** of words and symbols.

*   **Example of production rules for CFG**:
    ```
    NP → Det Nominal
    NP → ProperNoun
    Nominal → Noun | Nominal Noun  // '|' means OR
    ```
    (The `| Nominal Noun` part is often `Nominal -> Noun Nominal` or `Nominal -> Adjective Nominal` etc. The slide shows `Nominal -> Noun | Nominal Noun` which might mean `Nominal -> Noun` OR `Nominal -> Nominal Noun` for recursion like "Noun Noun Noun" or it's a typo for `Nominal -> Noun Nominal`.)
    The slide's example `Nominal → Noun | Nominal Noun` is likely intended to be two rules:
    `Nominal → Noun`
    `Nominal → Nominal Noun` (for sequences like "air fare") or `Nominal → Noun Nominal`.
    A more standard representation for a nominal modified by another noun would be `Nominal → Noun Nominal`.

*   **Hierarchical Embedding**: CFG rules can be hierarchically embedded. We can combine phrasal rules with lexical rules (rules that introduce words).
    *   **Lexical rules (part of the lexicon expressed as rules)**:
        (Image context: Lexical rules: Det -> a, Det -> the, Noun -> flight)
        ```
        Det → a
        Det → the
        Noun → flight
        ```