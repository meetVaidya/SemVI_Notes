## FSA as Language Recognizer
*   **Recognition:** The process of determining if an input string is accepted by the FSA (i.e., if it belongs to the language defined by the FSA or matches its corresponding regular expression).
*   **Process (Slide 74):**
    1.  Start in the start state.
    2.  For each input symbol:
        *   Consult the transition table/diagram.
        *   Move to the new state.
        *   Advance input pointer.
    3.  If, after all input is consumed, the FSA is in an accept state, the string is accepted; otherwise, rejected.

**Example: FSA for "sheeptalk" `/^baa+!$/` (Slides 75-77)**
(Image context: Sheep saying "baa!", regex `/^baa+!$/`, and FSA diagram: `q0 --b--> q1 --a--> q2 --a--> q3 --a(loop)--> q3 --!--> q4(Accept)`.)
*   Input `aba!b`: REJECTED (does not start with 'b').
*   Input `baaa!`: ACCEPTED (ends in `q4`).
![[Pasted image 20250519123936.png]]