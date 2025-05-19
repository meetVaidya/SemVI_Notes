## Syntax Analysis in NLP

Syntax analysis is a crucial step in Natural Language Processing (NLP) that deals with the grammatical structure of sentences. It determines if a sentence is grammatically correct.

## Tagging

*   **Definition**: Tagging is a classification process that automatically assigns descriptions (tags) to tokens (words).
*   **Tag**: The descriptor is called a tag. It can represent part-of-speech, semantic information, etc.
*   Parts of speech are defined based on their grammatical relationship with neighboring words or their morphological properties (affixes).

## Part-of-Speech (PoS) Tagging

*   **Definition**: The process of assigning one of the parts of speech to a given word.
*   **Task**: Labeling each word in a sentence with its appropriate part of speech.
*   **Examples of Parts Of Speech**: Nouns, verbs, adverbs, adjectives, pronouns, conjunctions, and their sub-categories.

### POS Tagging Example

*   Annotate each word in a sentence with a part-of-speech.
*   A POS tagger considers surrounding words while assigning a tag.

Example: "I like to read books"
`[(“I”, “Pronoun”), (“like”, “Verb”), (“to”, “To”), (“read”, “Verb”), (“books”, “Noun”)]`
(Image context: A visual representation of "I like to read books" with tags PRP, VBP, TO, VB, NNS above each word respectively.)

## Categories of Parts of Speech

1.  **Open Class (Mostly Content Words)**
    *   New words are frequently added to this class (e.g., google, skype, photoshop).
    *   Includes: Nouns, Verbs, Adjectives, Adverbs.
    *   Mostly content-bearing: they refer to objects, actions, and features in the world.

2.  **Closed Class (Function Words)**
    *   Consists of a limited, fixed number of words.
    *   Includes: Pronouns, determiners, prepositions, connectives.
    *   Used to tie the concepts of the sentences together.

## POS Tags: Level of Details

The level of detail in POS tags depends on the application's needs.
(Image context: A diagram showing "Level of details of POS Tag" branching into "Coarse grained" and "Fine grained".)

*   **Coarse Grained (Small Tag Set)**:
    *   Provides less detailed POS tags (fewer grammatical details).
    *   Example: Can identify a word as NOUN but not whether it's Singular or Plural.

*   **Fine Grained (Large Tag Set)**:
    *   Provides detailed grammatical information.
    *   Example: If a word is a Verb, it can specify if it's past tense, future tense, or present tense.
    *   **Note**: May lead to confusion due to too many POS tags.

## POS TAG / Word Classes

There are traditionally 9 word classes (parts of speech):
*   Noun, verb, adjective, preposition, adverb, article, pronoun, conjunction, interjection.

Common tags and examples:
*   **N** (noun): chair, bandwidth, pacing
*   **V** (verb): study, debate, munch
*   **ADJ** (adjective): purple, tall, ridiculous
*   **ADV** (adverb): unfortunately, slowly
*   **P** (preposition): of, by, to
*   **PRO** (pronoun): I, me, mine
*   **DET** (determiner): the, a, that, those

## Part-of-speech Tagging Process

*   **Input**: A sequence x1, x2,..., xn of (tokenized) words and a tagset.
*   **Output**: A sequence y1, y2,..., yn of tags, where each output yi corresponds exactly to one input xi.
(Image context: A diagram of a "Part of Speech Tagger" taking input words (Janet, will, back, the, bill) and outputting corresponding tags (NOUN, AUX, VERB, DET, NOUN).)

## POS Tagging as a Disambiguation Task

*   Words can be ambiguous (have more than one possible part-of-speech).
*   The goal of POS tagging is to find the correct tag for the given context.
*   **Example**:
    *   "book" can be a **verb** (e.g., "book that flight").
    *   "book" can be a **noun** (e.g., "hand me that book").
*   The goal of POS-tagging is to resolve these ambiguities by choosing the proper tag for the context.

## Part-of-Speech Tag Sets

The choice of tag set depends on the application.
*   **Small tag set**: More general tags.
*   **Large tag set**: Finer, more detailed tags.

Widely used part-of-speech tag sets:
*   **Penn Treebank**: 45 tags
*   **Brown Corpus**: 87 tags
*   **C7 tag set**: 146 tags
*   In a tagged corpus, each word is associated with a tag from the used tag set.

## POS Tagging Approaches Overview

*   **Rule-based tagging** (e.g., EnCG ENGTWOL tagger)
*   **Stochastic, or, Probabilistic tagging** (e.g., HMM - Hidden Markov Model tagging)
*   **Transformation-based tagging** (Learned rules - statistic and linguistic; e.g., Brill tagger)
