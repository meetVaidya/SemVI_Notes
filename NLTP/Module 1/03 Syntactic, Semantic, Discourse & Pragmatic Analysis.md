These stages of NLP build upon morphological analysis to understand the structure and meaning of language at sentence and conversational levels.

## 1. Syntactic Analysis (Parsing)
*   **Level of Analysis:** Sentence-Level Analysis.
*   **Focus:** Analyzing the grammatical structure of a sentence to understand its meaning based on the arrangement of words. It checks if a sentence is grammatically correct according to the rules of a language.
*   **Key Tasks:**
    *   Identifying the subject, verb, object, phrases, and clauses.
    *   Creating a parse tree (or syntax tree) that represents the syntactic structure.
*   **Importance:** Word order and grammatical rules are crucial for meaning.
    *   **Example:**
        *   `John Ate the Apple` (Correct syntax, meaningful)
        *   `Ate the Apple John` (Incorrect syntax in English, harder to interpret directly)
        *(Image context: A checkmark next to "John Ate the Apple" and a cross mark next to "Ate the Apple John".)*

### Parse Tree
A parse tree is a hierarchical representation of the syntactic structure of a sentence according to a formal grammar.

*   **Example Sentence:** `John ate the apple.`
*   **Grammar Rules (Context-Free Grammar - CFG):**
    1.  `S -> NP VP` (Sentence consists of a Noun Phrase and a Verb Phrase)
    2.  `VP -> V NP` (Verb Phrase consists of a Verb and a Noun Phrase)
    3.  `NP -> NAME` (Noun Phrase can be a Name)
    4.  `NP -> ART N` (Noun Phrase can be an Article and a Noun)
    5.  `NAME -> John`
    6.  `V -> ate`
    7.  `ART -> the`
    8.  `N -> apple`
    *(Image context: A parse tree diagram for "John ate the apple."
    S branches to NP and VP.
    NP (left) branches to NAME, which is "John".
    VP branches to V ("ate") and NP (right).
    NP (right) branches to ART ("the") and N ("apple").)*

## 2. Semantic Analysis
*   **Level of Analysis:** Sentence-Level Analysis.
*   **Focus:** Determining the meaning of words, phrases, and sentences. It goes beyond grammatical structure to interpret the actual message.
*   **Definition:** Semantics refers to meaning.
*   **Process:** A computer understands the meaning of a text by analyzing the text as a whole and not just looking at individual words.
*   **Importance of Context:** The context in which a word is used is very important for determining its meaning.

*   **Examples:**
    *   **Example 1 (Lexical Semantics & Collocations):**
        *   `She drank Some Milk` (Semantically plausible)
        *   `She drank Some books` (Semantically implausible, "drink" usually doesn't apply to "books")
    *   **Example 2 (Sentence Meaning & Intent):**
        > “Does it all sound like a joke to you?”
        This sentence, while grammatically simple, carries a specific semantic load implying annoyance or disbelief, which goes beyond the literal meanings of the individual words.

## 3. Discourse Analysis
*   **Level of Analysis:** Sentence-Level Analysis (often extending to multiple sentences or paragraphs).
*   **Focus:** Understanding how the meaning of a sentence is influenced by preceding and following sentences. It deals with the linguistic context and the relationships between sentences in a larger text.
*   **Key Task:** Resolving references, especially anaphora (pronouns or other referring expressions referring back to previously mentioned entities).

*   **Example (Anaphora Resolution):**
    *   **Sentence 1:**
        > Monkeys Eat Banana, when **they** Wake up.
        *   Who is "they" here?
        *   **Answer:** Monkey (The pronoun "they" refers to "Monkeys")
    *   **Sentence 2:**
        > Monkeys eat Banana, when **they** are ripe.
        *   Who is "they" here?
        *   **Answer:** Banana (The pronoun "they" refers to "Banana")
    *   **Explanation:** The interpretation of "they" changes based on the context provided by the rest of the sentence.

## 4. Pragmatic Analysis
*   **Level of Analysis:** Sentence-Level Analysis (highly dependent on real-world context).
*   **Focus:** Understanding the intended meaning of a speaker or writer, which may differ from the literal meaning. It considers the context of the utterance, the speaker's intentions, and the relationship between speakers.
*   **Definition:** Knowledge of the relationship of meaning to the goals and intentions of the speaker.
*   **Key Aspects:** Speaker's intent, implicature, speech acts.

*   **Examples (Speech Acts):**
    *   **Utterance 1:**
        > Close the Door
        *   **Interpretation:** Order / Command
    *   **Utterance 2:**
        > Please Close the Door
        *   **Interpretation:** Request, affirmation (more polite)
    *   **Explanation:** Both sentences have similar semantic content (related to closing a door), but their pragmatic function (how they are intended to be used in communication) is different due to the presence of "Please" and social conventions.