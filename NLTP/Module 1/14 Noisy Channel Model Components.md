# 16 Noisy Channel Model: Components In-Depth and Example

This section details the estimation of the Language Model and Channel Model probabilities and walks through an example of applying the Noisy Channel Model for spelling correction.

*(Refers to content from PDF6, Slides 9-23, and practice problems on slides 34-48)*

## Non-word Spelling Error Example: "acress"
*(Refers to content from PDF6, Slide 9, 10)*

Let the misspelled (observed) word `x` be "acress".

**Candidate Generation (words within 1 Damerau-Levenshtein edit distance):**
*(Slide 10 shows a table of candidates, the correct letter, error letter, and type of edit)*
| Error  | Candidate Correction | Correct Letter(s) in Candidate | Error Letter(s) in "acress" | Type         | `x` (acress) | `w` (candidate) |
| :----- | :------------------- | :----------------------------- | :-------------------------- | :----------- | :----------- | :-------------- |
| acress | actress              | t                              | - (deletion from actress)   | deletion     | acres        | actress         |
| acress | cress                | - (insertion into cress)       | a                           | insertion    | acress       | cress           |
| acress | caress               | ca                             | ac                          | transposition| acress       | caress          |
| acress | access               | c                              | r                           | substitution | acress       | access          |
| acress | across               | o                              | e                           | substitution | acress       | across          |
| acress | acres                | - (insertion into acres)       | s (final s)                 | insertion    | acress       | acres           |
*(Note: The table on slide 10 is slightly ambiguous in its "Correct Letter" / "Error Letter" columns. The interpretation above tries to match the edit type. For `P(x|w)`, `x` is the observed error, `w` is the correct candidate.)*

*   **Observation:**
    *   80% of spelling errors are typically within edit distance 1.
    *   Almost all errors are within edit distance 2.
    *(Refers to content from PDF6, Slide 11)*
*   **Extended Edits:** Sometimes, insertion of space or hyphen is also allowed as an edit.
    *   `thisidea` -> `this idea`
    *   `inlaw` -> `in-law`

## Step 1: Language Model `P(w)` - Prior Probability
*(Refers to content from PDF6, Slide 12, 13)*

*   **Source:** Use any language modeling algorithm (Unigram, Bigram, Trigram).
    *   For web-scale spelling correction, simpler models like "Stupid Backoff" might be used for efficiency.
*   **Example: Unigram Prior Probability for candidates of "acress"**
    Counts from COCA (Corpus of Contemporary American English - 404,253,213 words):
    | Word    | Frequency | P(word) (Freq / Total Words) |
    | :------ | :-------- | :--------------------------- |
    | actress | 9,321     | .0000230573                  |
    | cress   | 220       | .0000005442                  |
    | caress  | 686       | .0000016969                  |
    | access  | 37,038    | .0000916207                  |
    | across  | 120,844   | .0002989314                  |
    | acres   | 12,874    | .0000318463                  |

## Step 2: Channel Model `P(x|w)` - Error/Edit Probability
*(Refers to content from PDF6, Slide 14, 15, 17)*

*   **Goal:** Calculate `P(x|w)` for all candidate words `w` (generated in the previous step, e.g., those within 1 or 2 edit distance from `x`).
*   `P(x|w)` = Probability of the specific edit that transforms `w` (correct word) into `x` (misspelled word).
    *   `x = x₁, x₂, x₃… xₘ` (misspelled word)
    *   `w = w₁, w₂, w₃… wₙ` (correct word candidate)
*   **Estimating `P(x|w)` using Confusion Matrices:**
    We build confusion matrices from error data to count how often specific types of errors occur.
    Let `char₁char₂` be two adjacent characters, `#` be a word boundary.
    *   `del[char₁, char₂]`: count of `char₁char₂` typed as `char₁` (i.e., `char₂` deleted after `char₁`).
        `P(typed=char₁ | correct=char₁char₂) = del[char₁, char₂] / count(char₁char₂)`
    *   `ins[char₁, char₂]`: count of `char₁` typed as `char₁char₂` (i.e., `char₂` inserted after `char₁`).
        `P(typed=char₁char₂ | correct=char₁) = ins[char₁, char₂] / count(char₁)`
    *   `sub[char₁, char₂]`: count of `char₁` typed as `char₂` (i.e., `char₁` substituted by `char₂`).
        `P(typed=char₂ | correct=char₁) = sub[char₁, char₂] / count(char₁)`
    *   `trans[char₁, char₂]`: count of `char₁char₂` typed as `char₂char₁` (transposition).
        `P(typed=char₂char₁ | correct=char₁char₂) = trans[char₁, char₂] / count(char₁char₂)`

    *(Image context: PDF6, Slide 16 shows a large confusion matrix for substitutions. Example: "Actually the letter 'a' was mistakenly typed 'e' 388 times". This means `sub[a,e]` (correct='a', typed='e') has a count of 388. The P(x|w) calculation on slide 17 normalizes these counts.)*

    **Slide 17: Normalizing Confusion Counts for `P(x|w)`**
    *   For deletion of `wᵢ` from `w = ...wᵢ₋₁wᵢ...` to get `x = ...wᵢ₋₁...`:
        `P(x|w) = count(wᵢ₋₁wᵢ typed as wᵢ₋₁) / count(wᵢ₋₁wᵢ)`
    *   For insertion of `xⱼ` into `w = ...wᵢ...` to get `x = ...wᵢxⱼ...` (between `wᵢ` and `wᵢ₊₁`, or `xⱼ` inserted after `wᵢ` if `wᵢ` is `xᵢ`):
        `P(x|w) = count(wᵢ typed as wᵢxⱼ) / count(wᵢ)`
    *   For substitution of `wᵢ` by `xᵢ`:
        `P(x|w) = count(wᵢ typed as xᵢ) / count(wᵢ)`
    *   For transposition of `wᵢwᵢ₊₁` to `xᵢxᵢ₊₁` (where `xᵢ=wᵢ₊₁`, `xᵢ₊₁=wᵢ`):
        `P(x|w) = count(wᵢwᵢ₊₁ typed as wᵢ₊₁wᵢ) / count(wᵢwᵢ₊₁)`

## Step 3: Calculation for `ŵ` (Most Probable Word)
*(Refers to content from PDF6, Slide 18)*

Now, combine `P(w)` and `P(x|w)` for each candidate:
`ŵ = argmax_{w ∈ Candidates} P(x|w) * P(w)`

**Example: Channel Model `P(x|w)` for "acress" (`x`) and its candidates (`w`)**
*(Refers to content from PDF6, Slide 19. `x|w` column describes the edit from `w` to `x`)*
| Candidate `w` | Edit `w` -> `x`="acress" | `x|w` notation (from slide) | `P(x|w)` (Hypothetical) |
| :------------ | :----------------------- | :-------------------------- | :---------------------- |
| actress       | del 't' from actress     | `c|ct` (acress from actress)  | .000117                 |
| cress         | ins 'a' into cress       | `a|#` (acress from cress)     | .00000144               |
| caress        | trans 'ca'->'ac' in caress| `ac|ca` (acress from caress) | .00000164               |
| access        | sub 'c'->'r' in access    | `r|c` (acress from access)  | .000000209              |
| across        | sub 'o'->'e' in across    | `e|o` (acress from across)  | .0000093                |
| acres         | ins 's' into acres       | `es|e` (acress from acres)   | .0000321                |
| acres         | ins 's' into acres       | `ss|s` (acress from acres)   | .0000342                |
*(Note: The `x|w` notation on the slide is a bit condensed. For `actress` -> `acress`, the edit is deleting 't' from `ct` in `actress`. For `cress` -> `acress`, it's inserting 'a' before `cress` (denoted `a|#`). For `access` -> `acress`, it's `r` in `acress` being a typo for `c` in `access`.)*

**Noisy Channel Probability for "acress" (`x`)**
*(Refers to content from PDF6, Slide 20, 21)*
| Candidate `w` | `P(x|w)`    | `P(w)`      | `P(x|w)P(w) * 10⁹` |
| :------------ | :---------- | :---------- | :----------------- |
| actress       | .000117     | .0000231    | 2.7                |
| cress         | .00000144   | .000000544  | .00078             |
| caress        | .00000164   | .00000170   | .0028              |
| access        | .000000209  | .0000916    | .019               |
| **across**    | **.0000093**| **.000299** | **2.8**            |
| acres         | .0000321    | .0000318    | 1.0                |
| acres         | .0000342    | .0000318    | 1.0                |

**Result:** "across" has the highest `P(x|w)P(w)` product (2.8 * 10⁻⁹), so it is chosen as the best correction for "acress" using a unigram language model.

## Using a Bigram Language Model
*(Refers to content from PDF6, Slides 22, 23)*
If we use a bigram language model, the context matters.
Consider the phrase: "a stellar and versatile **acress** whose combination of sass and glamour..."

*   We need `P(candidate | versatile)` and `P(whose | candidate)`.
*   Example (with add-1 smoothing, hypothetical values):
    *   `P(actress|versatile) = .000021`
    *   `P(whose|actress) = .0010`
    *   `P(across|versatile) = .000021`
    *   `P(whose|across) = .000006`

*   Score for "versatile **actress** whose":
    `P(actress|versatile) * P(whose|actress) * P(x="acress"|w="actress")`
    `= .000021 * .0010 * .000117` (channel model prob for actress)
    `≈ 2.457 * 10⁻¹²`
    *(Slide 23 calculates `P("versatile actress whose")` using only LM bigram probabilities: `.000021 * .0010 = 210 * 10⁻¹⁰`. This is just the LM part. To combine with channel model, we multiply by `P(x|w)`.)*

*   Score for "versatile **across** whose":
    `P(across|versatile) * P(whose|across) * P(x="acress"|w="across")`
    `= .000021 * .000006 * .0000093` (channel model prob for across)
    `≈ 1.17 * 10⁻¹⁵`

In this contextual case, "actress" would likely be preferred over "across" because the language model `P(whose|actress)` is much higher than `P(whose|across)`, outweighing the slightly better unigram `P(x|w)P(w)` for "across".

## Real-Word Spelling Correction
*(Refers to content from PDF6, Slides 24-33)*
This is for when the typed word `x` is a valid dictionary word, but incorrect in context (e.g., "their" vs "there").

*   **Challenge:** 25-40% of spelling errors are real words.
*   **Process:**
    1.  For each word `wᵢ` in the input sentence `W = w₁, w₂, ..., wₙ`.
    2.  Generate a candidate set for `wᵢ`:
        *   The word `wᵢ` itself.
        *   All single-letter edits of `wᵢ` that are valid English words.
        *   Homophones of `wᵢ`.
    3.  Choose the best sequence of candidates `W'` that maximizes `P(W')` using the noisy channel framework.
        `W' = argmax P(X|W')P(W')` where `X` is the observed sentence.
        *(Image context: PDF6, Slide 28, 29 show a trellis/lattice diagram for choosing the best sequence of words like "two of thew" -> "to/tao/too/two" "of/off/on" "threw/thaw/the".)*
*   **Simplification:** Often assume only one error per sentence. Iterate through each word, generate candidates for that word, and re-score the whole sentence.
*   **Channel Model `P(x|w)` for Real-Word Errors:**
    *   If `x` is a candidate correction for `w` (original word in sentence), `P(x|w)` is the probability of the edit.
    *   Crucially, we also need `P(w|w)`: the probability of **no error** (i.e., the word was typed correctly). This is usually a high value (e.g., 0.90 to 0.995) depending on assumed error rates.
    *(Refers to content from PDF6, Slide 32)*

**Peter Norvig's "thew" Example (Real-Word Error Context):**
*(Refers to content from PDF6, Slide 33)*
Observed word `x` = "thew" (which is a real, albeit rare, word).
| Candidate `w` | Edit `w` -> `x` | `x|w` notation | `P(x|w)` (Channel) | `P(w)` (Language Model) | `10⁹ * P(x|w)P(w)` |
| :------------ | :-------------- | :------------- | :----------------- | :-------------------- | :------------------ |
| the           | e -> ew         | `ew|e`          | 0.000007           | 0.02                  | 144                 |
| **thew**      | **no error**    |                | **0.95** (assumed) | 0.00000009            | **90**              |
| thaw          | a -> e          | `e|a`          | 0.001              | 0.0000007             | 0.7                 |
| threw          | r -> -          | `h|hr` (del r) | 0.000008           | 0.000004              | 0.03                |
| thwe          | - -> e          | `ew|we` (trans)| 0.000003           | 0.00000004            | 0.0001              |

Here, "the" is chosen as the correction for "thew" because `P("thew"|"the") * P("the")` is highest. The high prior `P("the")` and a reasonable channel probability for the specific error `e`->`ew` make it win over `P("thew"|"thew") * P("thew")` where `P("thew")` is very low.

---
*(Practice problems from PDF6, Slides 35-48 are specific calculation exercises based on these principles, often providing the necessary counts or probabilities directly.)*