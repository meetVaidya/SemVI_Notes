## Overview of PDTB

*   The Penn Discourse TreeBank (PDTB) is another major dataset and model for coherence relations.
*   It focuses on annotating discourse relations, often signaled by explicit **discourse connectives**, but also implicit ones.
*   PDTB labeling is **lexically grounded**.

## Annotation Process

1.  **Explicit Connectives:**
    *   Identify connective (e.g., "because," "as a result") and its two arguments (Arg1, Arg2).
    *   Example: *Jewelry displays...fake. **As a result**, marketers...lost space.*
        *   Connective: "As a result"
        *   Arg1: "Jewelry displays...fake."
        *   Arg2: "marketers...lost space."

2.  **Implicit Connectives:**
    *   For relations between adjacent sentences without explicit signals.
    *   Annotators choose a plausible implicit connective and label its sense.
    *   Example: *EPA imposed a ban on asbestos. **(implicit=as a result)** By 1997, uses...will be outlawed.*
        *   Arg1: "EPA imposed a ban..."
        *   Arg2: "By 1997, uses..."

3.  **Sense Disambiguation:**
    *   For ambiguous connectives (e.g., "since"), the specific sense (CAUSAL vs. TEMPORAL) is marked.

## PDTB Sense Hierarchy

PDTB uses a hierarchical system for relation senses. Four high-level classes:

1.  **TEMPORAL:** Temporal relationship.
    *   Type Example: `SYNCHRONOUS`
    *   Example: *Parishioners chat. (Implicit while) In the tower, five men...pull ropes.*
2.  **CONTINGENCY:** Causal, conditional, purposeful.
    *   Type Example: `REASON`
    *   Example: *Mr. Breeden...position to get somewhere. (implicit=because) As a former White House aide...he is savvy.*
3.  **COMPARISON:** Similarity or difference.
    *   Type Example: `CONTRAST`
    *   Example: *The U.S. wants removal of barriers; Japan denies there are real barriers.*
4.  **EXPANSION:** Elaboration, restatement, specification.
    *   Type Example: `CONJUNCTION`
    *   Example: *Not only do actors stand outside characters...but they often literally stand on their heads.*

**(Image context: PDF1 Slide 15 provides a detailed breakdown of the PDTB sense hierarchy.)**
*   **Temporal:** Asynchronous, Synchronous.
*   **Contingency:** Cause (Reason, Result), Pragmatic Cause, Condition, Pragmatic Condition.
*   **Comparison:** Contrast, Pragmatic Contrast, Concession, Pragmatic Concession.
*   **Expansion:** Exception, Instantiation, Restatement, Alternative, List.

## Discourse Parsing with PDTB

(Content from PDF1 Slide 16)
*   Discourse parsing for PDTB often focuses on assigning labels (connective, Arg1, Arg2, sense) to leaf spans rather than building a full RST-style tree, though hierarchical structures can be built on top.