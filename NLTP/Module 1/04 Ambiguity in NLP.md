Ambiguity is a fundamental characteristic of natural language, where a word, phrase, or sentence can have multiple possible interpretations. Resolving ambiguity is a major challenge in NLP.
*   **Definition of Ambiguous Input:** An input is ambiguous if there are multiple alternative linguistic structures that can be built for it.
*   **General Definition:** A situation where a word or a sentence may have more than one meaning.

## Types of Ambiguities

There are different types of ambiguities that NLP systems must handle:

1.  **Lexical Ambiguity**
2.  **Syntactical (or Structural) Ambiguity**
3.  **Semantic Ambiguity**
4.  **Discourse Ambiguity (often Anaphoric Ambiguity)**
5.  **Pragmatic Ambiguity**

### 1. Lexical Ambiguity
This occurs when a single word form has multiple meanings (i.e., it can be a homonym or polyseme).

*   **Definition:** The ambiguity of a single word.
*   **Resolution:** Can often be resolved by Part-of-Speech (POS) tagging and considering the surrounding context.
*   **Cause:** A word has more than one meaning or belongs to more than one lexical category.

*   **Examples:**
    *   **Book:**
        *   `Book` (Noun) - Textbook/Novel
        *   `Book` (Verb) - Book ticket/seat
    *   **Bank:**
        *   `Bank` (Noun) - Financial institute
        *   `Bank` (Noun) - River Bank
        *   `Bank` (Verb) - Banking Transaction (e.g., "to bank a check")
### 2. Syntactical (or Structural) Ambiguity
This arises when a sentence can be parsed in more than one way, leading to different grammatical structures and thus different meanings.

*   **Definition:** Syntactic Ambiguity exists in the presence of two or more possible meanings within the sentence due to its structure.
*   **Cause:** The grammar or rules allow for multiple valid parse trees for the same sequence of words.
*   **Focus:** Specifies the possible arrangements of words in a sentence.

*   **Example:**
    > I saw the girl with the binocular.
    *   **Interpretation 1:** I (saw the girl) [who was holding a binocular]. (The binocular belongs to the girl)
    *   **Interpretation 2:** I (saw the girl) [using a binocular]. (I used the binocular to see the girl)
    *   **Question:** Did I have the binoculars? Or did the girl have the binoculars?
    *(Image context: Two different parse tree structures are shown for a sentence like "list all flights on Tuesday".
    Tree 1: (VP (V list) (NP (DET all) (N flights) (PP (P on) (NP Tuesday)))) - "list (all flights that are on Tuesday)"
    Tree 2: (VP (V list) (NP (DET all) (N flights)) (PP (P on) (NP Tuesday))) - This seems to be a repetition or slight variation. The key is that "on Tuesday" can modify "flights" or the verb "list".)*
    *The slide's parse trees are for "list all flights on Tuesday", illustrating how "on Tuesday" can attach differently.*

### 3. Semantic Ambiguity
This occurs when a sentence has a well-defined syntactic structure but can still be interpreted in multiple ways due to the meanings of the words or their relationships.

*   **Definition:** When a sentence has more than one meaning, it is called semantic ambiguity.
*   **Example:**
    > Rahul loves his cat and Dipesh does too.
    *   **Interpretation 1:** Dipesh loves Rahul's cat.
    *   **Interpretation 2:** Dipesh loves his own cat.
    *   **Question:** Whether Dipesh loves his cat or Rahul's cat.

### 4. Anaphoric Ambiguity (A type of Discourse Ambiguity)
This type of ambiguity occurs due to the use of anaphoric entities (like pronouns) in discourse, where the referent of the pronoun is unclear.

*   **Definition:** This kind of ambiguity occurs in the sentence due to the use of Anaphoric entities in discourse.
*   **Anaphora:** When the same beginning of a sentence is repeated in the sentence several times, we often use a pronoun instead of a noun. (More generally, anaphora is when a word or phrase refers to an earlier word or phrase).
*   **Example (from discourse analysis):**
    *   > My mother liked the house very much, but **she** couldn't purchase **it**.
        ("she" refers to "My mother", "it" refers to "the house")
    *   **Ambiguous Anaphora Example:**
        *   Monkeys Eat Banana, when **they** Wake up.
            *   Who is "they" here? **Monkey**
        *   Monkeys eat Banana, when **they** are ripe.
            *   Who is "they" here? **Banana**
*   **Resolution:** Identify When, Where, by whom an occurrence was said or to whom/what a pronoun refers, based on context.

### 5. Pragmatic Ambiguity
This arises when the intended meaning of an utterance cannot be determined from the literal meaning alone and depends on the context, speaker's intent, and shared knowledge.

*   **Focus:** Understanding the speaker's intention.
*   **Example:**
    > You are Late
    *   **Possible Interpretations:**
        *   **Informative:** Simply stating a fact.
        *   **Criticizing:** Expressing disapproval or annoyance.
    *   The actual meaning depends on tone, situation, and relationship between speakers.