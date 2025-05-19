Resolving coreferences, especially for pronouns, involves applying constraints to filter impossible antecedents and preferences to choose among likely ones.

## Reference Resolution Tasks

1.  **Coreference Resolution:** Finding all expressions referring to the same entity.
    *   **Constraint ('it'):** 'It' that doesn't refer to a specific entity (e.g., "It's raining") must be handled.
2.  **Pronominal Anaphora Resolution:** Finding the antecedent for a single pronoun.
    *   Example: For "his," find "Ram" if Ram is the antecedent.

## Syntactic and Semantic Constraints

These are relatively hard rules:

1.  **Number Agreement:** Singular/plural agreement.
    *   Singular: she, her, he, him, his, it
    *   Plural: we, us, they, them
    *   Unspecified: you
2.  **Person Agreement:** First/second/third person agreement.
    *   Example: "I" (1st) vs. "he" (3rd).
3.  **Gender Agreement:** Masculine/feminine/nonpersonal agreement.
    *   Example: "She" for "Zuha" (feminine); "It" for "printer" (nonpersonal).
4.  **Case Agreement (Pronoun Form):** Pronoun form depends on its syntactic role (subject vs. object).
    *   Example: "he" (subject) vs. "him" (object).
5.  **Syntactic Constraints (Binding Theory):** Governs local coreference for reflexives and pronominals (detailed separately).
    *   Reflexive: *John bought **himself** a car.* (himself=John)
    *   Pronominal: *John bought **him** a car.* (him≠John)
6.  **Selectional Restrictions:** Verb's semantic requirements for its arguments.
    *   Example: *John parked his Acura in the garage. He had driven **it**.* ("it" = Acura, because a garage can't be driven).
    *   Example: *Zuha put an apple on the table. Suha is eating **it**.* ("it" = apple, because a table isn't typically eaten).

## Preferences in Pronoun Interpretation

These are tendencies or heuristics:

1.  **Recency (Recently Introduced References):** More recent entities are more salient.
    *   Example: *John has an Integra. Bill has a Legend. Mary likes to drive **it**.* ("it" likely Legend).
2.  **Grammatical Role (Subject Preference):** Subjects are often more salient.
    *   Example: *John went to the dealership with Bill. **He** bought an Integra.* ("He" likely John).
3.  **Repeated Mention (Focus):** Entities repeatedly focused on remain salient.
    *   Example: *John needed a car... He decided... Bill went with him. **He** bought an Integra.* ("He" likely John, the sustained focus).
4.  **Parallelism:** Parallel grammatical structures influence pronoun interpretation.
    *   Example: *Mary went with Sue. Sally went with **her**.* ("her" likely Sue).
5.  **Verb Semantics (Implicit Causality):** Some verbs emphasize certain argument roles, biasing pronoun reference.
    *   Example: *John **telephoned** Bill. **He**...* (He=John). *John **criticized** Bill. **He**...* (He might be Bill, depending on verb bias).