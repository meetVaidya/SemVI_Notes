## Symbols in CFG

Symbols used in a CFG are divided into two classes:

(Image context: A diagram showing "Terminal" on the left and "non-terminal" on the right. An arrow points from "Terminal" to a description: "The symbols terminal that correspond to words in the language (“the”, “nightclub”)". An arrow points from "non-terminal" to a description: "symbols that express abstractions over these terminals are called non-terminals." Below, it explains rule structure: "the item to the right of the arrow (→) is an ordered list of one or more terminals and non-terminals; to the left of the arrow is a single non-terminal symbol expressing some cluster or generalization.")

1.  **Terminal Symbols (Terminals)**:
    *   These are the actual words or tokens in the language (e.g., "the", "nightclub", "prefers").
    *   They cannot be broken down further by grammar rules.

2.  **Non-Terminal Symbols (Non-Terminals or Variables)**:
    *   These symbols represent abstractions or categories over terminals or other non-terminals (e.g., NP, VP, S, Det, Noun).
    *   They express clusters or generalizations and can be rewritten using grammar rules.

**Structure of a CFG Rule (Production)**:
*   `A → α`
    *   **Left-hand side (LHS - A)**: A single non-terminal symbol.
    *   **Arrow (→)**: Means "can be rewritten as", "consists of", or "can expand to".
    *   **Right-hand side (RHS - α)**: An ordered sequence of one or more terminal and/or non-terminal symbols.

## Two Ways to View a CFG

A CFG can be seen as:
1.  A device for **generating sentences**.
2.  A device for **assigning a structure** to a given sentence (parsing).

## CFG as a Generator

*   We can read the `→` arrow as “rewrite the symbol on the left with the string of symbols on the right”.
*   Starting from a non-terminal symbol (often a special start symbol like S or a specific phrase type like NP), we can apply rules to derive a string of terminal symbols (a sentence or phrase).

**Example Derivation for "a flight" from NP:**
(Image context: A derivation sequence:
So starting from the symbol: NP
we can use our first rule to rewrite NP as: Det Nominal
and then rewrite Nominal as: Det Noun
and finally rewrite these parts-of-speech as: a flight
"a flight can be derived from the non-terminal NP")

1.  Start with `NP`.
2.  Apply `NP → Det Nominal`  => `Det Nominal`
3.  Apply `Nominal → Noun` (assuming a simpler rule than `Det Noun` for Nominal directly) => `Det Noun`
4.  Apply `Det → a` => `a Noun`
5.  Apply `Noun → flight` => `a flight`

This sequence of rule expansions is called a **derivation** of the string of words.

### Parse Tree

*   It is common to represent a derivation by a **parse tree**.
*   Parse trees are commonly shown inverted, with the root at the top and terminal symbols (words) at the leaves.
*   The internal nodes are non-terminals, and the children of a node correspond to the RHS of a rule whose LHS is the parent node.

(Image context: A parse tree for "a flight".
NP (root)
  ├── Det -> a
  └── Nominal
        └── Noun -> flight
)
The figure above shows "A parse tree for 'a flight'", representing this derivation.

## Start Symbol

*   The formal language defined by a CFG is the set of all strings of terminal symbols that are derivable from a designated **start symbol**.
*   Each grammar must have one designated start symbol, often called **S**.
*   Since CFGs are often used to define sentences, S is usually interpreted as the "sentence" node. The set of strings derivable from S is the set of sentences in the language (or a simplified version of it) defined by the grammar.

## Example Grammar Rules (L0 - a sample grammar)

(Image context: A list of grammar rules for S, NP, VP, PP and example phrases for each rule.)
(Image context: A separate list of lexical rules for Noun, Verb, Adjective, etc.)

**Few additional phrasal rules:**
*   `S → NP VP` (A sentence can consist of a Noun Phrase followed by a Verb Phrase)
    *   Example: "I prefer a morning flight"
*   `VP → Verb NP` (A verb phrase can be a Verb followed by a Noun Phrase)
    *   Example: "prefer a morning flight"
*   `VP → Verb NP PP` (Verb followed by NP and Prepositional Phrase)
    *   Example: "leave Boston in the morning"
*   `VP → Verb PP` (Verb followed by Prepositional Phrase)
    *   Example: "leaving on Thursday"
*   `PP → Preposition NP` (A prepositional phrase is a Preposition followed by an NP)
    *   Example: "from Los Angeles"

**Example Lexicon (L0):**
(Image context: A table showing lexical rules (word -> POS category or POS category -> word).)
*   `Noun → flights | breeze | trip | morning`
*   `Verb → is | prefer | like | need | want | fly`
*   `Adjective → cheapest | non-stop | first | latest | other | direct`
*   `Pronoun → me | I | you | it`
*   `Proper-Noun → Alaska | Baltimore | Los Angeles | Chicago | United | American`
*   `Determiner → the | a | an | this | these | that`
*   `Preposition → from | to | on | near`
*   `Conjunction → and | or | but`

**Grammar L0 (combining phrasal and types of lexical entries):**
(Image context: A table summarizing Grammar L0 rules and example phrases.)
| Rule                      | Example Phrase                     |
|---------------------------|------------------------------------|
| `S → NP VP`               | I + want a morning flight          |
| `NP → Pronoun`            | I                                  |
| `NP → Proper-Noun`        | Los Angeles                        |
| `NP → Det Nominal`        | a + flight                         |
| `Nominal → Nominal Noun`  | morning + flight                   |
| `Nominal → Noun`          | flights                            |
| `VP → Verb`               | do                                 |
| `VP → Verb NP`            | want + a flight                    |
| `VP → Verb NP PP`         | leave + Boston + in the morning    |
| `VP → Verb PP`            | leaving + on Thursday              |
| `PP → Preposition NP`     | from + Los Angeles                 |

**Parse Tree Example using Grammar L0:**
Sentence: "I prefer a morning flight"
(Image context: A detailed parse tree for "I prefer a morning flight" according to grammar L0.
S
├── NP
│   └── Pro -> I
└── VP
    ├── Verb -> prefer
    └── NP
        ├── Det -> a
        └── Nom
            ├── Nom -> Noun -> morning
            └── Noun -> flight
(Note: The slide shows Nom -> Nom Noun, then Nom -> Noun (morning), Noun -> flight. A more standard way for "morning flight" might be Nom -> Adj Noun or Nom -> Noun Noun if "morning" is treated as a noun modifier. The tree reflects the grammar provided.)
The provided image actually shows:
Nom
├── Noun -> morning (as a Noun under a first Nom)
└── Noun -> flight (as a Noun under a second Nom, or the first Nom is `Nominal -> Noun Noun` where first Noun is morning, second is flight. The image shows `Nom -> Noun (morning)` and then this `Nom` has another child `Noun (flight)`. This is unusual. A more typical structure for "morning flight" would be `Nominal -> Noun Nominal` or `Nominal -> Adjective Nominal`. The slide's tree for "I prefer a morning flight" shows `Nom -> Nom Noun`, where the first `Nom` expands to `Noun (morning)` and the `Noun` expands to `flight`. This implies `morning` is a nominal modifier of `flight`.)
Let's represent the tree from the slide:
S
├── NP
│   └── Pro -> I
└── VP
    ├── Verb -> prefer
    └── NP
        ├── Det -> a
        └── Nominal
            ├── Nominal -> Noun -> morning
            └── Noun -> flight
This structure implies a rule like `Nominal -> Nominal Noun` was applied as `Nominal_A -> Nominal_B Noun_C`, then `Nominal_B -> Noun_D`.

## Formal Definition of Context-Free Grammar

A context-free grammar G is defined by four parameters (a 4-tuple): **N, Σ, R, S**.
(Image context: A blue box defining the 4-tuple for CFG.)
*   **N (or V)**: A set of **non-terminal symbols** (variables).
*   **Σ (Sigma)**: A set of **terminal symbols** (disjoint from N).
*   **R (or P)**: A set of **rules or productions**, each of the form `A → β`,
    *   where `A` is a non-terminal (`A ∈ N`).
    *   `β` (beta) is a string of symbols from the infinite set of strings `(Σ ∪ N)*` (i.e., a sequence of terminals and/or non-terminals, including the empty string ε in some definitions, though often restricted in CNF).
*   **S**: A designated **start symbol** (`S ∈ N`).

