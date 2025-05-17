## 1. Zero-Shot Learning (ZSL)
  - **Definition**: Enables a system to recognize new faces (or classes) that it has **never seen during training**.
  - **How it Works**:
      - Relies on **attribute-based learning** or shared semantic embedding spaces.
      - The model learns a mapping from visual features to a set of high-level attributes (e.g., "round face," "wears glasses," "male," "long hair") or to a general semantic space (e.g., word embeddings of class names).
      - For an unseen class, its attributes/semantic description are provided, and the model tries to match the visual input to this description.
  - **Need for ZSL**:
      - Useful when there is absolutely **no labeled training data** for a new person/class.
      - Helps systems generalize beyond the set of explicitly known faces/classes.
      - Can recognize a new person based on a textual description or a set of defining characteristics.
  - **Example**:
      - Recognizing an "unseen celebrity" based on a textual description of their features.
      - An AI trained on common animals (cats, dogs, horses) identifying a "zebra" (never seen) by understanding it has "stripes" (a known attribute) and "resembles a horse" (a known class with shared attributes).
      - Airport security: Recognizing a new traveler based on a government-provided description ("tall male with glasses") without a prior photo.

## 2. One-Shot Learning (OSL)
- **Definition**: Enables a model to recognize a face (or class) after seeing **only one example image** during enrollment/training for that specific face/class.
- **How it Works**:
	- Typically uses deep learning models like **Siamese Networks** or models pre-trained for embedding generation (e.g., **FaceNet**).
	- The single example image is used to generate a reference embedding.
	- New input images are converted to embeddings and their distance to the reference embedding is computed to determine similarity.
- **Need for OSL**:
	- Practical in real-world applications where collecting multiple images per person is not feasible or convenient (e.g., initial setup for phone face unlock).
	- Essential for security applications like passport verification (comparing live face to single passport photo).
- **Example**:
	- Smartphone face unlock: Scans your face once during setup. Later, it recognizes you even with minor changes (hairstyle, glasses) by comparing the new face embedding to the single stored embedding.

## 3. Few-Shot Learning (FSL)
- **Definition**: Enables recognition using only a **few example images** (typically 2 to 10) per person/class for training/enrollment.
- **How it Works**:
	- Often applies **meta-learning ("learning to learn")** techniques. The model learns how to quickly adapt to new classes given limited data, by leveraging knowledge from other classes it was trained on with more data.
	- Can also involve fine-tuning pre-trained embedding models with the few available examples.
- **Need for FSL**:
	- Useful in scenarios where data collection is difficult or limited, but more than one example is available.
	- Examples: Medical imaging (few samples of rare diseases), new employee registrations for an attendance system.
	- Helps build adaptive security systems that require minimal training data per new user.
- **Example**:
	- A university attendance system needing only 3-5 images of each student to recognize them accurately across different conditions.

## 4. Comparison of ZSL, OSL, and FSL

| Learning Type | Training Data Needed (for the new class) | How It Works                                                                 | Example Use Case                                       |
|---------------|------------------------------------------|------------------------------------------------------------------------------|--------------------------------------------------------|
| **Zero-Shot** | No direct data for new classes           | Learns via attributes, semantic embeddings, or general knowledge transfer    | AI recognizing an unseen celebrity from description    |
| **One-Shot**  | One image per class                      | Embedding-based comparison (e.g., Siamese Networks, FaceNet)                 | Phone unlock after scanning face once                  |
| **Few-Shot**  | Two to ten images per class (typically)  | Meta-learning to generalize quickly; fine-tuning pre-trained embedding models | School attendance system with limited student photos |

## 5. Why Are These Methods Needed in Face Recognition?
- **Efficiency**: Reduces the need for extensive and often costly data collection for every individual.
- **Security**: Enables robust authentication even with minimal initial training data per user.
- **Scalability**: Allows recognition of new faces/individuals without the need to retrain the entire model from scratch each time a new person is added.
- **Robustness**: When combined with good embedding techniques, these methods can handle variations in lighting, aging, slight pose changes, and accessories.
