## 1. One-to-One

*   **Description:** A single input produces a single output.
*   **Structure:** This is the standard architecture for traditional feedforward neural networks, not typically considered an RNN in its recurrent sense unless the single input/output is part of a temporal process handled by a simple RNN cell with no unrolling.
*   **Example:** Image classification (single image input -> single class label output), simple character-level prediction if only one character is considered.
*   **Note:** The diagram labels this "typical neural network."

## 2. One-to-Many

*   **Description:** A single input produces a sequence of outputs.
*   **Structure:** The RNN takes a single fixed-size input (e.g., an image vector or a context vector) and generates a sequence of outputs over several time steps. The initial hidden state might be conditioned on the single input.
*   **Examples:**
    *   **Image Captioning:** Input is an image; output is a sequence of words describing the image.
    *   **Music Generation:** Input might be a genre or a starting note; output is a sequence of musical notes.

## 3. Many-to-One

*   **Description:** A sequence of inputs produces a single output.
*   **Structure:** The RNN processes a sequence of inputs, and the final output is generated only after the entire sequence has been processed. The final hidden state often summarizes the entire sequence.
*   **Examples:**
    *   **Sentiment Classification:** Input is a sequence of words (a sentence or review); output is a single sentiment label (positive/negative).
    *   **Text Categorization:** Input is a document (sequence of words); output is a single category.

## 4. Many-to-Many (Synchronized/Matching Lengths)

*   **Description:** A sequence of inputs produces a sequence of outputs, where there is a one-to-one correspondence between each input and output at each time step, and the input and output sequences have the same length.
*   **Structure:** The RNN processes an input at each time step and generates an output for that specific time step.
*   **Examples:**
    *   **Part-of-Speech (POS) Tagging:** Input is a sequence of words; output is a sequence of POS tags, one for each word.
    *   **Named Entity Recognition (NER):** Input is a sequence of words; output is a sequence of entity labels for each word.
    *   **Video Classification (frame-by-frame):** Input is a sequence of video frames; output is a classification label for each frame.

## 5. Many-to-Many (Unsynchronized/Non-Matching Lengths)

*   **Description:** A sequence of inputs produces a sequence of outputs, but the input and output sequences can have different lengths, and there isn't necessarily a direct step-by-step alignment.
*   **Structure:** This architecture often employs an **Encoder-Decoder** framework.
    *   **Encoder:** An RNN processes the entire input sequence and compresses it into a fixed-size context vector (often the final hidden state of the encoder).
    *   **Decoder:** Another RNN takes the context vector from the encoder as its initial state and generates the output sequence one element at a time.
*   **Examples:**
    *   **Machine Translation:** Input is a sentence in one language (sequence of words); output is a sentence in another language (sequence of words), and lengths can differ.
    *   **Text Summarization:** Input is a long document; output is a shorter summary.
    *   **Question Answering:** Input is a question (sequence); output is an answer (sequence).