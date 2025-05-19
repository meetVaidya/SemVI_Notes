## Supervised Coreference Resolution

(Content from PDF2 Slides 52-55)

Modern coreference resolution often uses supervised machine learning, treating it as a classification task.

**Approaches:**
1.  **Rule-Based:** (e.g., Hobbs' Algorithm)
2.  **Supervised Algorithms:** Classify pairs of mentions as coreferent or not, or choose the best antecedent. Requires annotated training data.

**Features for Supervised Resolution Classifier:**
For a potential anaphor (mention `i`) and antecedent (mention `j`):
*   **Agreement Constraints (PNG):** Person, Number, Gender agreement.
    *   Example: *Jack gave Mary a gift. **She** was excited.* (She/Mary agree in gender).
*   **Recency:** Distance between mentions.
    *   Example: *John went to a movie. Jack went as well. **He** was not busy.* ("He" likely Jack).
*   **Grammatical Role:** Subject position entities are often preferred.
    *   Example: *John went to a movie with Jack. **He** was not busy.* ("He" likely John).
*   **Parallelism:** Structural similarity between clauses.
    *   Example: *John went with Jack for a movie. Joe went with **him** for the restaurant.* ("him" likely Jack).
*   **Verb Semantics / Thematic Roles:** Verb's influence on argument salience.
    *   Example: *John criticized Bill. **He** lost the laptop.*
*   **Selectional Restrictions:** Semantic fit.
    *   Example: *John parked his car in the garage after driving **it** for hours.* ("it" = car).
*   **Lexical Features:** Words, headwords, mention type.
*   **Syntactic Features:** Parse tree distance, c-command, binding constraints.

## Centering Theory

(Content from PDF1 Slides 22-35)

Centering Theory (Grosz, Joshi, Weinstein) models local discourse coherence based on attentional state and entity salience.

**Core Ideas:**
*   **Backward-looking Center (`Cb(Un)`):** The most salient entity in utterance `Un` also present in `Un-1`.
*   **Forward-looking Centers (`Cf(Un)`):** Ordered list of all entities in `Un` by salience (e.g., Subject > Object).
*   **Preferred Center (`Cp(Un)`):** Highest-ranked entity in `Cf(Un)`.
*   Coherence is higher if `Cb` is maintained or shifted smoothly.

**Intuition Example (Grosz et al., 1995):**
Text 1 (John as consistent subject) is more coherent than Text 2 (focus shifts between John and store).
(Image context: PDF1 Slide 23 shows these two texts.)

**Intersentential Transitions (between `Un` and `Un+1`):**

|                               | `Cb(Un+1) = Cb(Un)` OR `Cb(Un)` undef. | `Cb(Un+1) ≠ Cb(Un)` |
|-------------------------------|----------------------------------------|---------------------|
| **`Cb(Un+1) = Cp(Un+1)`**     | **CONTINUE**                           | **SMOOTH-SHIFT**    |
| **`Cb(Un+1) ≠ Cp(Un+1)`**     | **RETAIN**                             | **ROUGH-SHIFT**     |

*(Table based on PDF1 Slide 26. Descriptions: CONTINUE - Cb maintained & preferred; RETAIN - Cb maintained, not preferred; SMOOTH-SHIFT - Cb changes to preferred; ROUGH-SHIFT - Cb changes, not to preferred.)*

**Rules/Preferences:**
1.  **Pronoun Rule:** Use pronouns for continued `Cb`.
2.  **Transition Ordering (Coherence):** `CONTINUE > RETAIN > SMOOTH-SHIFT > ROUGH-SHIFT`.

**Example Analysis (Natalie Texts):**
(Image context: PDF1 Slides 31-35 analyze two texts about "Natalie.")
*   **Text 1 (More "CONTINUE" transitions):**
    *   U₁: Natalie was an assistant professor at UIC. (`Cp(U₁)`: Natalie)
    *   U₂: She taught a class... (`Cb(U₂)`: Natalie, `Cp(U₂)`: Natalie) -> **CONTINUE**
*   **Text 2 (More "RETAIN" or "SHIFT" transitions):**
    *   U₁: Natalie was an assistant professor at UIC. (`Cp(U₁)`: Natalie)
    *   U₂: UIC had a class that she taught... (`Cb(U₂)`: Natalie, `Cp(U₂)`: UIC) -> **RETAIN**

Centering Theory predicts Text 1 is more coherent.