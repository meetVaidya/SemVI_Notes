## Introduction to Finite Automata (FA / FSM)

*   A **Finite Automaton (FA)**, also known as a **Finite State Machine (FSM)**, is the simplest abstract machine used to recognize patterns.
*   It consists of a finite set of **states** and rules (transitions) for moving from one state to another based on **input symbols**.
*   FSAs model a computation process that can be in one of a finite number of states at any given time.
*   They either **accept** or **reject** an input string based on whether the processing ends in a designated final (accept) state.

(Image context slide 55: Diagram of an automaton with Input tape, Automata box (states q1-qn), Output tape, and labels for "States of Automata", "State relation", "Output relation".)

## Formal Definition of a Finite Automaton

A Finite Automaton is formally defined by a 5-tuple: (Q, Σ, δ, q₀, F)

*   **Q:** A finite set of **states**.
*   **Σ (Sigma):** A finite set of **input symbols** (the alphabet).
*   **δ (Delta):** The **transition function**. It dictates how the machine moves from one state to another.
*   **q₀ (or q):** The **initial state** (or start state), an element of Q.
*   **F:** A set of **final states** (or accept states), a subset of Q (F ⊆ Q).

## Deterministic Finite Automata (DFA)

A Deterministic Finite Automaton (DFA) is a specific type of FA where:

*   For each state and each input symbol, there is **exactly one** transition to a next state.
*   The transition function is defined as: **δ: Q × Σ → Q**.
*   No **null (ε) transitions** are allowed (i.e., the machine cannot change state without consuming an input symbol).
*   A transition function must be defined for **every state and every input symbol**.

(Image context slide 58: A DFA diagram for Σ = {0, 1} that accepts all strings ending with 0. State 0 is initial. State 1 is final. Transitions: 0 --1--> 0; 0 --0--> 1; 1 --0--> 1; 1 --1--> 0.)

## FSM Design Example: Decimal Number Divisible by 3

(Based on handwritten slides 59-64)

**Problem:** Design an FSM to check if a given decimal number is divisible by 3.

**Core Idea:** The states of the FSM will represent the remainder of the number processed so far when divided by 3.
*   States:
    *   `q_s` (or `q_initial`): Start state (before any digits, effective remainder 0).
    *   `q_0`: Remainder is 0 (Accept state).
    *   `q_1`: Remainder is 1.
    *   `q_2`: Remainder is 2.
*   Input Alphabet (Σ): Decimal digits {0, 1, ..., 9}. These can be grouped by their value modulo 3:
    *   `d mod 3 = 0`: {0, 3, 6, 9} (let's call this input class `R0`)
    *   `d mod 3 = 1`: {1, 4, 7} (input class `R1`)
    *   `d mod 3 = 2`: {2, 5, 8} (input class `R2`)
*   Transition Logic: If current remainder is `rem_curr` and new digit `d` is read, new remainder `rem_new = (rem_curr * 10 + d) mod 3 = (rem_curr * 1 + (d mod 3)) mod 3`.

**Transition Table:**

| Current State (rem_curr) | Input `d` (d mod 3 = 0) | Input `d` (d mod 3 = 1) | Input `d` (d mod 3 = 2) |
| :----------------------- | :---------------------- | :---------------------- | :---------------------- |
| `q_s` (initial, rem 0)   | `q_0`                   | `q_1`                   | `q_2`                   |
| `q_0` (rem 0) *Accept*   | `q_0`                   | `q_1`                   | `q_2`                   |
| `q_1` (rem 1)            | `q_1`                   | `q_2`                   | `q_0`                   |
| `q_2` (rem 2)            | `q_2`                   | `q_0`                   | `q_1`                   |

**Transition Diagram (Slide 64):**
(Image context: State diagram with `q_s` as initial, `q_0` as accept (double circle), and `q_1`, `q_2`. Arrows are labeled with input classes R0, R1, R2 corresponding to digits mod 3 = 0, 1, 2 respectively.)
*   From `q_s`: `q_s --R0--> q_0`, `q_s --R1--> q_1`, `q_s --R2--> q_2`.
*   From `q_0`: `q_0 --R0--> q_0`, `q_0 --R1--> q_1`, `q_0 --R2--> q_2`.
*   From `q_1`: `q_1 --R0--> q_1`, `q_1 --R1--> q_2`, `q_1 --R2--> q_0`.
*   From `q_2`: `q_2 --R0--> q_2`, `q_2 --R1--> q_0`, `q_2 --R2--> q_1`.

**Simulation Example (Slide 63):**
*   **Number 312:**
    1. `q_s` --3(R0)--> `q_0`
    2. `q_0` --1(R1)--> `q_1`
    3. `q_1` --2(R2)--> `q_0` (End in `q_0` - Accept)
*   **Number 7258:**
    1. `q_s` --7(R1)--> `q_1`
    2. `q_1` --2(R2)--> `q_0`
    3. `q_0` --5(R2)--> `q_2`
    4. `q_2` --8(R2)--> `q_1` (End in `q_1` - Reject)