## Graphical Representation of RST Relations

*   RST relations are often shown as tree structures.
*   Asymmetric Nucleus-Satellite relations: Arrow from satellite to nucleus, labeled with relation type.

(Image context: PDF1 Slide 6 shows "Kevin must be here." (NUC) and "His car is parked outside" (SAT) linked by an "evidence" relation, arrow from SAT to NUC.)

## Elementary Discourse Units (EDUs)

*   Leaves of an RST tree are **Elementary Discourse Units (EDUs)** or **discourse segments**.
*   Basic, non-overlapping text spans (often clauses/phrases).
*   Determining EDU boundaries (segmentation) is a crucial first step.
*   Analogous to constituents in sentence syntax.

## Hierarchical Structure and Complete Discourse Example

RST represents the coherence of larger texts through a hierarchical structure of relations between EDUs.
(Image context: PDF1 Slide 8 shows a complex RST tree for a paragraph about Mars (text on Slide 7), with relations like evidence, background, elaboration, list, contrast, purpose, connecting 9 EDUs.)

**Example Paragraph (Mars):**
> With its distant orbit-50 percent farther from the sun than Earth-and slim atmospheric blanket, Mars experiences frigid weather conditions. Surface temperatures typically average about -60 degrees Celsius (-76 degrees Fahrenheit) at the equator and can dip to -123 degrees C near the poles. Only the midday sun at tropical latitudes is warm enough to thaw ice on occasion, but any liquid water formed in this way would evaporate almost instantly because of the low atmospheric pressure.

## RST Discourse TreeBank

*   The **RST Discourse TreeBank (RST-DT)** (Carlson et al., 2001) is a major corpus for RST.
*   Contains 385 English Wall Street Journal articles with full RST parses.
*   Uses 78 distinct relations (grouped into 16 classes).
*   RST treebanks exist for other languages (Spanish, German, etc.).

## RST Parsing Process

1.  **EDU Segmentation:** Extract start/end of each EDU.
    *   Example: `[Mr. Rambo says]e1 [that a 3.2-acre property]e2 ...`
2.  **RST Tree Building:**
    *   Often uses shift-reduce parsing, similar to syntactic parsing.
    *   Modern parsers use neural approaches and representation learning.

**Parser State and Actions (Shift-Reduce):**
*   Uses a **stack** and a **queue** (of EDUs).
*   **`shift`**: Moves EDU from queue to stack.
*   **`reduce(l, d)`**: Merges top two stack subtrees with relation `l` and nuclearity `d` (NN, NS, SN).
*   **`pop root`**: Finalizes tree.

**Example RST Discourse Tree and Parser Actions:**
(Image context: PDF1 Slide 20 shows an RST tree for 4 EDUs:
e1: American Telephone & Telegraph Co. said it
e2: will lay off 75 to 85 technicians here, effective Nov. 1.
e3: The workers install, maintain and repair its private branch exchanges,
e4: which are large intracompany telephone networks.
Structure: e1(S)-attr-e2(N); e4(S)-elab-e3(N); then (e3,e4)(S)-elab-(e1,e2)(N).
This means (e1,e2) is the main nucleus, elaborated by (e3,e4).)

(Image context: PDF1 Slide 21 shows a table of parser actions to build this tree.
Key steps:
1. SH e1, SH e2, RD(attr, SN) -> e1:2 (e1 is SAT, e2 is NUC)
2. SH e3, SH e4, RD(elab, NS) -> e3:4 (e3 is NUC, e4 is SAT)
3. RD(elab, SN) on e1:2 and e3:4 -> e1:4 (e3:4 is SAT, e1:2 is NUC)
Final tree e1:4 is popped.)