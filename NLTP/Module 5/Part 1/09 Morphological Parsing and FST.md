## Morphological Parsing

*   **Definition:** The process of analyzing a word's surface form (how it's written/spoken) to determine its underlying lexical form (base morphemes + grammatical information).
*   **Goal:** Given an input like `cats`, produce `cat +N +PL` (root: cat, Noun, Plural).
*   General structure: `Stem ----- Prefix + Stem + Suffix`.

## Two-Level Morphology

A common framework for morphological parsing that relates two levels:

1.  **Lexical Level:** Represents morphemes and features (e.g., `cat +N +PL`).
2.  **Surface Level:** Represents the actual spelling (e.g., `cats`).

(Image context slide 85: Lexical tape `|c|a|t|+N|+PL|` and Surface tape `|c|a|t|s|`.)
*   Mapping rules (often FSTs) connect these levels.

**Examples of Surface Form to Lexical Form Mapping (Slide 86):**

| Surface Form | Lexical Form     |
| :----------- | :--------------- |
| `cats`       | `cat +N +PLU`    |
| `cat`        | `cat +N +SG`     |
| `goose`      | `goose +N +SG`   |
| `geese`      | `goose +N +PLU`  |
| `catch`      | `catch +V`       |
| `caught`     | `catch +V +PAST` |

## Components of a Morphological Processor (Slide 87-91)

1.  **Lexicon (Slide 88):**
    *   A repository of stems and affixes.
    *   Contains information like part-of-speech (noun, verb) and sub-categories (regular/irregular noun).
    *   Simplest parser: a lexicon with all possible inflected words.

2.  **Morphotactics (Slide 89-90):**
    *   Rules governing the order of morphemes within a word (e.g., plural suffix follows noun stem).
    *   Often implemented using FSAs.
    (Image context slide 90: Lexicon examples and an FSA for nominal inflection showing `reg-noun`, `plural -s`, `irreg-pl-noun`, `irreg-sg-noun` transitions.)

3.  **Orthographic Rules (Spelling Rules - Slide 91):**
    *   Model spelling changes when morphemes combine.
    *   Example: `cook` + `ing` → `cooking` (concatenation).
    *   Example: `care` + `ing` → `caring` (e-deletion, not `careing`).
	![[Pasted image 20250519130832.png]]

## Finite State Transducers (FSTs)

While FSAs recognize languages, **FSTs map input strings to output strings**, making them suitable for morphological analysis (surface form → lexical form) and generation (lexical form → surface form).

*   FSTs operate on two (or more) tapes: an input tape and an output tape.
*   Transitions are labeled with an **input symbol : output symbol** pair.
*   An FST defines a **regular relation** between sets of strings.

![[Pasted image 20250519130406.png]]
## Multi-Level Tapes and Orthographic Rules with FSTs

Complex spelling changes can be handled by introducing intermediate levels between the lexical and surface tapes, with FSTs mapping between each level.

(Image context slide 101: Lexical `|d|o|g|+N|+PL|`, Intermediate `|d|o|g|^|s|#|`, Surface `|d|o|g|s|`. `^` = morpheme boundary, `#` = word end.)

(Image context slide 102-103: FSTs for "foxes" showing lexical, intermediate, and surface tapes. The intermediate tape helps manage morpheme boundaries (`^`) and spelling changes. For "foxes", `x + ^s#` (lexical/intermediate) becomes `xes` (surface) due to e-insertion.)

**Orthographic Rules as FSTs (Slide 104-105):**
Each spelling rule can be implemented as an FST.
(Image context slide 104: Table of spelling rules like consonant doubling, E-deletion, E-insertion e.g., `watch` + `s` -> `watches`.)

*   **Rule Formalism:** `a => b / c __ d` (rewrite 'a' as 'b' when between left context 'c' and right context 'd').
*   **E-insertion for FST:** `ε : e / {s,z,x,ch,sh} __ ^s#`
    *   Lexical `ε` (nothing) maps to surface `e` when the left context on the lexical/intermediate tape is one of {s,z,x,ch,sh} and the right context is a morpheme boundary `^` followed by a plural `s` and word end `#`.
    *   Example: `fox` (lexical) + `^s#` (plural morpheme on intermediate tape) → `foxes` (surface). The `ε:e` rule applies after `x` and before `^s`.