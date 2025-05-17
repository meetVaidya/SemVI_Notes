## Computational Linguistics
Computational Linguistics is an interdisciplinary field concerned with the statistical or rule-based modeling of natural language from a computational perspective, as well as the study of appropriate computational approaches to linguistic questions.

## Natural Language

*   **Definition:** Languages that are spoken naturally by human beings.
    *   These are languages that have evolved naturally in humans through use and repetition without conscious planning or premeditation.

## Languages

*   **Human to Human:** Communication between people using natural language.
    *(Image context: Icon showing two human figures with arrows indicating communication flow between them.)*
*   **Machine to machine:** Communication protocols and data exchange formats used by computer systems.
    *(Image context: Icon showing two computer monitors with arrows indicating communication flow between them.)*

## Perspective on NLP: Areas of AI and their Interdependencies

NLP is a core component of Artificial Intelligence (AI) and has strong interdependencies with other AI areas.

*   **NLP (Natural Language Processing):** Concerned with computers being able to process, understand, and generate human language (e.g., Hindi, Marathi, Gujarati, French, English).
*   **Machine Learning (ML):** Provides algorithms that allow computers to learn from data. NLP heavily relies on ML for tasks like classification, clustering, and prediction.
    *   Statistical techniques used in NLP are often ML techniques.
*   **Knowledge Representation (KR):** Deals with how to represent knowledge in a way that computers can use it. NLP can be fed by KR to understand context and meaning.
*   **Search:** NLP techniques improve search engine understanding of queries and documents. Search can provide data for NLP models.
*   **Logic:** Provides formal methods for reasoning, which can be applied to language understanding.
*   **Planning:** Involves creating a sequence of actions to achieve a goal. NLP can be used to understand instructions or generate plans in natural language.
*   **Computer Vision:**
    *   NLP can be followed by Computer Vision where machines process and understand visual information to operate in a scene.
    *   Vision can provide context for language (e.g., describing an image).
*   **Robotics:**
    *   Involves embedded software in robots that perform actions like navigation. NLP allows robots to understand commands or interact using language.
*   **Expert Systems:**
    *   Concerned with emulating expert-level performance on specific tasks (e.g., medical diagnosis).
    *   These systems often operate based on a large number of rules, similar to how a doctor might use years of education and practice. NLP can be used for interacting with expert systems or extracting knowledge from texts to build them.

### Feeding Layers
*   Machine Learning and Planning feed into several layers in the outermost category.
*   Natural Language Processing is fed by Machine Learning.
*   Natural Language Processing is also fed by Knowledge Representation.
*   Modern NLP uses many Statistical Techniques, which are often Machine Learning techniques that utilize knowledge content in data.

## Introduction to Natural Language Processing (NLP)

*   **Definition 1:** NLP is a branch of artificial intelligence that helps computers understand, interpret, and manipulate human language.
*   **Definition 2:** NLP (Natural Language Processing) is a branch of artificial intelligence that deals with the interaction between computers and humans using natural language.
*   **Definition 3 (Computer Science perspective):** It refers to the branch of computer science—and more specifically, the branch of artificial intelligence or AI—concerned with giving computers the ability to understand text and spoken words in much the same way human beings can.
*   **Definition 4 (Interdisciplinary):** NLP is an interdisciplinary subfield of linguistics, computer science, and artificial intelligence concerned with the interactions between computers and human language.
*   **Ultimate Objective:** The ultimate objective of NLP is to read, decipher, understand, and make sense of human languages in a manner that is valuable.

## NLP System Overview

An NLP system typically processes input language data and produces a structured output.

*   **Basic Text Input:**
    *   Input: Text (Document / Paragraph / Sentence / Word)
    *   Process: NLP System
    *   Output: Text / Rating / Graph / Audio
    *(Image context: A block diagram showing "INPUT Text" feeding into an "NLP System" (represented by a computer monitor) which then produces "OUTPUT (Text/Rating/Graph/Audio)".)*

*   **Audio Input:**
    *   Input: Audio
    *   Process 1: Speech Processing (converts Audio to Text)
    *   Process 2: NLP System (processes Text)
    *   Output: Text / Rating / Graph
    *(Image context: A block diagram showing "Audio" -> "Speech Processing" -> "Text" -> "NLP System" -> "OUTPUT (Text/Rating/Graph)".)*

*   **Audio/Image Input:**
    *   Input: Audio OR Image
    *   Process 1 (Audio): Speech Processing (converts Audio to Text)
    *   Process 1 (Image): OCR Processing (converts Image to Text)
    *   Process 2: NLP System (processes Text from either source)
    *   Output: Text / Rating / Graph
    *(Image context: A block diagram showing two input paths: "Audio" -> "Speech Processing" -> "Text" AND "Image" -> "OCR Processing" -> "Text". The "Text" then feeds into the "NLP System" which produces "OUTPUT (Text/Rating/Graph)".)*