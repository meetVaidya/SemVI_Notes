Minimum Edit Distance is a measure of similarity between two strings, calculated as the minimum number of single-character edits (insertions, deletions, or substitutions) required to change one string into the other.
## How Similar Are Two Strings?
Many NLP tasks are concerned with measuring how similar two strings are.

*   **Spell Correction:**
    *   User typed: "graffe"
    *   Which is closest? `graf`, `graft`, `grail`, `giraffe`
    *   Intuitively, "giraffe" (differs by one letter) seems more similar than "grail" or "graf". Minimum edit distance quantifies this.
*   **Other Applications:** Machine Translation, Information Extraction, Speech Recognition.
## Edit Distance
*   **Definition:** Edit distance gives us a way to quantify intuitions about string similarity.
*   **Minimum Edit Distance:** The minimum number of editing operations needed to transform one string into the other.
*   **Basic Editing Operations:**
    *   **Insertion:** Adding a character.
    *   **Deletion:** Removing a character.
    *   **Substitution:** Replacing one character with another.

## Minimum Edit Distance Example: Alignment
Consider transforming the string "INTENTION" to "EXECUTION".

*   **Alignment:**
    ```
    I N T E N * T I O N
    | | | | | | | | | |
    * E X E C U T I O N
    d s s   i s
    ```
    (Where `*` indicates an insertion or deletion, `d`=deletion, `s`=substitution, `i`=insertion. The alignment shows 'I' deleted, 'N' to 'E' sub, 'T' to 'X' sub, 'E' same, 'N' to 'C' sub, 'T' inserted as 'U', 'T' same, 'I' same, 'O' same, 'N' same.
    A better alignment might be:
    ```
    I N T E N T I O N
    * E X E C U T I O N
    d s s s s i
    ```
    Or, as shown on PDF3, Slide 4:
    ```
      I N T E N * T I O N
      | | | | | | | | | |
    * E X E C U T I O N
    ```
    Operations (from PDF3, Slide 5, based on the above alignment):
    `d` (delete I)
    `s` (substitute N with E)
    `s` (substitute T with X)
    ` ` (E matches E - no cost if substitution cost depends on match)
    `s` (substitute N with C)
    `i` (insert U)
    `s` (substitute T with T - no cost if match)
    ` ` (I matches I)
    ` ` (O matches O)
    ` ` (N matches N)

    A clearer alignment from PDF5, Slide 3:
    ```
    I N T E * N T I O N
    | | | | | | | | | |
    * E X E C U T I O N
    d s s   i s
    ```
    This implies:
    1. Delete 'I' from source
    2. Substitute 'N' with 'E'
    3. Substitute 'T' with 'X'
    4. 'E' matches 'E' (no operation or cost 0 substitution)
    5. Insert 'C' into source (or delete from target if thinking target to source) - slide implies 'E' to 'C' substitution.
       Let's use the standard interpretation:
       String 1: I N T E N T I O N
       String 2: E X E C U T I O N

       Align:
       I N T E N - T I O N
       - E X E C U T I O N
       d s s s s i (delete I, sub N->E, T->X, E->E, N->C, insert U, T->T, I->I, O->O, N->N)
       This is one possible alignment.

       The alignment from PDF3, Slide 4:
       `I N T E N * T I O N`
       `* E X E C U T I O N`
       This implies:
       1. Delete I
       2. N -> E (sub)
       3. T -> X (sub)
       4. E -> E (match/sub)
       5. N -> C (sub)
       6. Insert U
       7. T -> T (match/sub)
       8. I -> I (match/sub)
       9. O -> O (match/sub)
       10. N -> N (match/sub)

*   **Cost Calculation:**
    *   **If each operation (insertion, deletion, substitution) has a cost of 1:**
        The distance is the number of operations. For the alignment:
        `I N T E N - T I O N`
        `- E X E C U T I O N`
        Operations: del(I), sub(N,E), sub(T,X), sub(E,E), sub(N,C), ins(U), sub(T,T), sub(I,I), sub(O,O), sub(N,N)
        If substitution of identical chars costs 0, and others cost 1:
        del(I) = 1
        sub(N,E) = 1
        sub(T,X) = 1
        sub(E,E) = 0
        sub(N,C) = 1
        ins(U) = 1
        sub(T,T) = 0
        sub(I,I) = 0
        sub(O,O) = 0
        sub(N,N) = 0
        Total = 5.
        *(PDF3, Slide 5: "Distance between these is 5" if each operation has cost 1. This implies 5 distinct edit operations like del, sub, ins, ignoring matches as operations.)*
    *   **If substitutions cost 2 (Levenshtein distance variant where sub=2, ins=1, del=1):**
        Using the same 5 operations:
        1 del (cost 1) + 3 subs (cost 2 each) + 1 ins (cost 1) = 1 + 6 + 1 = 8.
        *(PDF3, Slide 5: "Distance between them is 8" if substitutions cost 2.)*

## Other Uses of Edit Distance in NLP
*   **Evaluating Machine Translation and Speech Recognition:**
    *   Word Error Rate (WER) and similar metrics use edit distance to compare system output with a reference translation/transcription.
    *   Example:
        ```
        R (Reference): Spokesman confirms senior government adviser was appointed
        H (Hypothesis): Spokesman said    the senior              adviser was appointed
                          S (Sub)   I (Ins)     D (Del)                      I (Ins)
        ```
*   **Named Entity Extraction and Entity Coreference:**
    *   To identify and link mentions of the same entity that might have slight variations.
    *   Examples:
        *   `IBM Inc.` announced today
        *   `IBM` profits
        *   `Stanford Professor Jennifer Eberhardt` announced yesterday
        *   for `Professor Eberhardt`…
        (Edit distance can help recognize these as referring to the same entities despite variations.)

## Defining Minimum Edit Distance Formally
*   **For two strings:**
    *   `X` of length `n` (source string)
    *   `Y` of length `m` (target string)
*   **We define `D(i,j)`:**
    *   The edit distance between the first `i` characters of `X` (i.e., `X[1..i]`) and the first `j` characters of `Y` (i.e., `Y[1..j]`).
*   **Goal:** The edit distance between the full strings `X` and `Y` is thus `D(n,m)`.