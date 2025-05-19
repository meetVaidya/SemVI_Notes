## Coherence Relations

Coherence relations describe the functional or logical connections between different spans of text (e.g., sentences, clauses), helping readers understand how parts of a text fit together.

**Example of Coherence:**
1.  *Jane took a train from Paris to Istanbul. She likes spinach.* (Less coherent)
2.  *Jane took a train from Paris to Istanbul. She had to attend a conference.* (More coherent, second sentence provides a REASON)

These connections can be specified as a set of coherence relations.

**Models and Corpora for Coherence Relations:**
*   **Rhetorical Structure Theory (RST)**
*   **The Penn Discourse TreeBank (PDTB)**

## Rhetorical Structure Theory (RST) Overview

*   RST (Mann and Thompson, 1987) is a widely used model for discourse organization.
*   It analyzes text based on relations between text spans.

## Nucleus and Satellite in RST

*   Relations are typically defined between two spans: a **nucleus (NUC)** and a **satellite (SAT)**.
    *   **Nucleus:** More central to the writer's purpose, interpretable independently.
    *   **Satellite:** Less central, provides supporting information, interpretable with respect to the nucleus.
*   Some relations are **symmetric**, holding between two nuclei (e.g., LIST).

## Examples of RST Coherence Relations

(Definitions adapted from RST Treebank Manual)

*   **Reason:**
    *   NUC: Action by animate agent.
    *   SAT: Reason for the action.
    *   Example: `[NUC Jane took a train...] [SAT She had to attend a conference.]`
*   **Elaboration:**
    *   SAT: Gives additional information/detail about the NUC.
    *   Example: `[NUC Dorothy was from Kansas.] [SAT She lived in the midst of the great Kansas prairies.]`
*   **Evidence:**
    *   SAT: Provides information to convince the reader of the NUC.
    *   Example: `[NUC Kevin must be here.] [SAT His car is parked outside.]`
*   **Attribution:**
    *   SAT: Gives the source of reported speech/thought in the NUC.
    *   Example: `[SAT Analysts estimated] [NUC that sales...declined...]`
*   **List:**
    *   Multinuclear: A series of nuclei without contrast or explicit comparison.
    *   Example: `[NUC Billy Bones was the mate;] [NUC Long John, he was quartermaster]`