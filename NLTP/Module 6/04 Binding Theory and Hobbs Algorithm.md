## Binding Theory

Binding Theory provides syntactic rules for how pronouns can refer within a sentence, particularly distinguishing reflexives and non-reflexive pronominals.

*   **Principle A (Reflexives):** A reflexive pronoun (e.g., "himself," "herself") must find its antecedent (be "bound") within its local clause, typically as a co-argument (often the subject).
    *   Example: *John₁ bought **himself₁** a new car.* (himself = John)
*   **Principle B (Pronominals):** A non-reflexive pronoun (e.g., "him," "her") must be "free" in its local clause; its antecedent cannot be a co-argument in that same clause.
    *   Example: *John₁ bought **him₂** a new car.* (him ≠ John)
    *   Example: *John₁ thinks that Mary₂ likes **him₁**.* ("him" can be "John" as John is outside the local clause "Mary likes him").

**Application Example:**
*S1: Jack is an engineer. S2: Jill likes **him**.*
*   Binding Theory (Principle B): In S2, "him" cannot refer to "Jill" (subject of local clause).
*   Gender Agreement: "him" (masculine) ≠ "Jill" (feminine).
*   Therefore, search for antecedent in S1. "Jack" matches. "him" resolves to "Jack."

(Image context: PDF2 Slide 41-42 illustrates these principles with examples. PDF2 Slide 43 shows application to the "Jack and Jill" example.)

## Hobbs' Algorithm for Pronoun Resolution

Hobbs' Algorithm is a classic, syntax-based heuristic for pronominal anaphora resolution. It searches parse trees in a specific order.

**Intuition:**
1.  Start at the target pronoun.
2.  Climb the parse tree to its sentence root (S).
3.  At each NP or S node on this upward path, search its children (and descendants) to the *left* of this path (breadth-first, left-to-right).
4.  Propose valid NPs (matching gender/number, not ruled out by Binding Theory) as antecedents.
5.  If no antecedent in the current sentence, repeat on previous sentences (most recent first).
6.  The first suitable NP found is chosen.

(Image context: PDF2 Slide 33 shows "Jack fell down and broke **his** crown," with an arrow from "his" to "Jack." PDF2 Slide 34 outlines the algorithm's intuition.)

**Example: "S1: Jack is an engineer. S2: Jill likes him."**
(Image context: PDF2 Slides 39, 46-48 show parse trees and resolution.)
1.  Target: "him" in S2.
2.  Binding Theory/Gender: "him" ≠ "Jill".
3.  Move to S1: "Jack is an engineer."
4.  Traverse S1's parse tree (breadth-first, left-to-right).
5.  "Jack" is found and matches "him."
6.  Resolution: "him" = "Jack."
    *   **Hobbs Distance Property:** The search order (e.g., subject "Jack" before object "an engineer") is key.

**Detailed Steps (Simplified from PDF2 S50-51):**
1.  Start at NP dominating pronoun.
2.  Go up to first NP/S node (X) via path (p).
3.  Search branches below X, left of p (left-to-right, breadth-first). Propose valid NPs.
4.  If X is sentence root: Traverse previous sentences (recent first, left-to-right, breadth-first). Propose valid NPs. Stop at first match.
5.  If X is not sentence root: Go up to next NP/S. Repeat search left of new path, then right of new path (not going below NPs/Ss on right). Continue up if needed.

(Image context: PDF2 Slide 49 shows another example: "Lyn's mom is a gardener. Craige likes her." resolving "her" to "Lyn's mom" by searching S1 after S2.)

Hobbs' algorithm relies on syntactic structure, search order, recency, and subject prominence.