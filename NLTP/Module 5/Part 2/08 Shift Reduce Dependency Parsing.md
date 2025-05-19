Shift-Reduce parsing is a common algorithm for dependency parsing. The "Arc Standard" system is one popular variant. It builds the parse tree by making a sequence of decisions (shift or reduce).

## Algorithm Setup

We need the following components:
1.  **A Stack**: Initially contains a dummy `[Root]` symbol. Words are pushed onto the stack.
2.  **A Buffer**: Contains the input words of the sentence to be parsed.
3.  **An Oracle (or Parser/Classifier)**: A function (often a trained machine learning model) that decides the next action to take based on the current configuration of the stack and buffer.
4.  **Set of Dependency Relations**: Tags like `obj`, `nsubj`, `iobj`, etc., that are used to label the arcs created.

(Image context: A diagram showing the components: "Stack" (s1, s2, ..., sn), "Input buffer" (w1, w2, ..., wn). An arrow from input buffer to "Parser" and an arrow from stack to "Parser". The "Parser" contains an "Oracle". An arrow from "Parser" outputs "Dependency Relations".)

## Algorithm Steps and Transitions

1.  **Initialization**:
    *   The Stack has `[Root]`.
    *   All words of the sentence are in the Buffer.

2.  **Processing Loop**:
    *   Repeatedly, a word can be popped from the buffer and pushed onto the Stack (this is part of a SHIFT action).
    *   The Oracle/parser looks at the top elements of the stack (typically the top two, `s1` and `s2`, where `s1` is on top) and predicts one of three possible transitions (actions), potentially with a relationship type:

    *   **LEFTARC (relation_type)**:
        *   Asserts a head-dependent relation `s2 -> s1` (s2 is head, s1 is dependent) with the given `relation_type`.
        *   Pops `s1` (the dependent) from the stack.
        *   `s2` remains on the stack.

    *   **RIGHTARC (relation_type)**:
        *   Asserts a head-dependent relation `s1 -> s2` (s1 is head, s2 is dependent) with the given `relation_type`.
        *   Pops `s2` (the dependent) from the stack.
        *   `s1` remains on the stack.

    *   **SHIFT**:
        *   Removes the first word from the buffer and pushes it onto the stack.

3.  **Prediction by Oracle**:
    *   The actual prediction by the Oracle has two parts:
        1.  Determining Head & Dependent using LEFTARC/RIGHTARC (or deciding to SHIFT).
        2.  Determining their relation type (e.g., `conj`, `iobj`).
    *   So, actual predictions might be `LEFTARC_IOBJ`, `RIGHTARC_CONJ`, etc. (For simplicity, examples often just use `LEFTARC` or `RIGHTARC`).

4.  **Termination**:
    *   The algorithm stops when the **buffer is empty** and the **stack has only `[Root]` left**.

## Restrictions and Considerations

*   **No LEFTARC if `s2` is `[Root]` and buffer is non-empty**: `[Root]` cannot be a dependent if there are still words to process.
*   **At least 2 elements on Stack for LEFTARC/RIGHTARC**: These operations require two items on the stack to form a relation.
*   **`[Root]` cannot be a dependent**: `[Root]` is a dummy variable and always the ultimate head.
*   The Oracle is typically a classifier trained on features from the stack, buffer, and partially built dependency tree.

## Dependency Treebank

*   A **Dependency Treebank** is a text corpus in which each sentence has a corresponding dependency tree.
*   These trees are usually either:
    *   Extracted/converted from Syntactic Treebanks (like PennTreebank, which is primarily constituency-based).
    *   Manually marked by humans.
*   Treebanks are crucial for training and evaluating dependency parsers.

## Example of Shift-Reduce Parsing

Consider the statement: **‘book me the morning flight’**.

(Image context: A table showing the steps of the Shift-Reduce parsing algorithm for the sentence "book me the morning flight". Columns: Step, Stack, Word List (Buffer), Action, Relation Added.)

| Step | Stack                             | Word List (Buffer)            | Action    | Relation Added      |
|------|-----------------------------------|-------------------------------|-----------|---------------------|
| 0    | `[root]`                          | `[book, me, the, morning, flight]` | SHIFT     |                     |
| 1    | `[root, book]`                    | `[me, the, morning, flight]`  | SHIFT     |                     |
| 2    | `[root, book, me]`                | `[the, morning, flight]`      | RIGHTARC  | (book → me)         |
| 3    | `[root, book]`                    | `[the, morning, flight]`      | SHIFT     |                     |
| 4    | `[root, book, the]`               | `[morning, flight]`           | SHIFT     |                     |
| 5    | `[root, book, the, morning]`      | `[flight]`                    | SHIFT     |                     |
| 6    | `[root, book, the, morning, flight]`| `[]`                          | LEFTARC   | (morning ← flight)  |
| 7    | `[root, book, the, flight]`       | `[]`                          | LEFTARC   | (the ← flight)      |
| 8    | `[root, book, flight]`            | `[]`                          | RIGHTARC  | (book → flight)     |
| 9    | `[root, book]`                    | `[]`                          | RIGHTARC  | (root → book)       |
| 10   | `[root]`                          | `[]`                          | Done      |                     |

**Explanation of selected steps:**

*   **Step-0**: Stack has only `[root]`. Oracle predicts SHIFT (as per restrictions, cannot do ARC operations yet). ‘book’ is pushed.
    *   Stack: `[root, book]`
    *   Buffer: `[me, the, morning, flight]`

*   **Step-1**: Top of stack: `book`, `root`. Oracle predicts SHIFT. ‘me’ is pushed.
    *   Stack: `[root, book, me]`
    *   Buffer: `[the, morning, flight]`

*   **Step-2**: Top two elements of stack: `book` (s2), `me` (s1). Oracle predicts RIGHTARC.
    *   This means `book` is Head, `me` is Dependent. Relation: `book → me`.
    *   `me` is popped. `book` remains.
    *   Stack: `[root, book]`
    *   Buffer: `[the, morning, flight]`

*   **Step-6**: Stack: `[root, book, the, morning, flight]`. Top two: `morning` (s2), `flight` (s1). Oracle predicts LEFTARC.
    *   This means `flight` is Head, `morning` is Dependent. Relation: `morning ← flight` (or `flight → morning`).
    *   `morning` is popped. `flight` remains.
    *   Stack: `[root, book, the, flight]`

*   **At last (Step-9)**: Buffer is empty. Stack: `[root, book]`. Oracle predicts RIGHTARC.
    *   Relation: `root → book`. `book` is popped (conceptually, as it becomes dependent of root, but root is special).
    *   Stack: `[root]`
    *   The parse tree is obtained from the accumulated relations, with ‘book’ as the root node of the actual sentence.