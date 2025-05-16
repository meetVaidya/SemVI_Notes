## 1. Introduction
    - **Etymology**: "Siamese" refers to Siamese twins, who are physically connected. A Siamese Network consists of two (or more) **identical subnetworks** that are "connected" by **sharing the same weights and parameters**.
    - **Purpose**: Primarily used for **similarity comparison** between two inputs, rather than direct classification of a single input.
    - **Core Idea**: Learns a feature representation (embedding) such that similar inputs are mapped to nearby points in the embedding space, and dissimilar inputs are mapped to distant points.
    - **Output**: Typically a distance or similarity score between the two inputs.

## 2. How Siamese Networks Work
    1.  **Input**: Takes two inputs simultaneously (e.g., two images, Image A and Image B).
    2.  **Identical Subnetworks**: Both inputs are processed independently by two identical neural network branches (often CNNs). These branches share the exact same architecture and weights.
        - Each subnetwork transforms its input image into a high-dimensional **feature embedding (vector)**.
    3.  **Distance/Similarity Calculation**: The two output embeddings are then compared using a distance metric (e.g., Euclidean distance, Cosine distance) or a similarity function.
        - `Distance(Embedding_A, Embedding_B)`
    4.  **Decision Layer (Optional but common for verification)**:
        - The calculated distance is often compared against a learned or predefined threshold.
        - If `distance < threshold`, the inputs are classified as "similar" or "same class."
        - If `distance >= threshold`, the inputs are classified as "dissimilar" or "different class."
        - Alternatively, the distance can be fed into further layers (e.g., dense layers + sigmoid) to output a similarity probability (0 to 1).

## 3. Architecture Details (Typical for Image Comparison)
    - **Input Images**: Two images are fed into the network.
    - **Shared CNN Backbone (Subnetworks)**:
        - Each branch is a CNN (e.g., AlexNet-like, VGG-like, ResNet-like).
        - **Convolutional Layers**: Extract hierarchical features. Filter sizes (e.g., 11x11, 5x5, 3x3) capture global and local patterns.
        - **Pooling Layers (e.g., 2x2 Max Pooling)**: Reduce spatial dimensions, retain important features, provide some translation invariance.
        - **Dropout Layers**: Help prevent overfitting during training.
        - **Fully Connected (FC) Layers**: At the end of each CNN branch, FC layers often produce the final fixed-dimensional embedding vector (e.g., 128-D or 512-D).
    - **Embedding Layer**: The output of each CNN branch is the feature embedding for its respective input image.
    - **Comparison Module**:
        - Calculates the distance (e.g., Euclidean: `sqrt(Σ(a_i - b_i)^2)`) or similarity between the two embeddings.
        - This distance is then used by a loss function during training.

## 4. Training Siamese Networks
    - **Paired Data**: Requires training data in the form of pairs:
        - **Positive Pairs**: Two images belonging to the *same* class/identity (e.g., two different photos of the same person). Target label: Similar (e.g., 1 or 0 depending on loss).
        - **Negative Pairs**: Two images belonging to *different* classes/identities (e.g., photos of two different people). Target label: Dissimilar (e.g., 0 or 1).
    - **Loss Functions**:
        - **Contrastive Loss**: Aims to pull embeddings of positive pairs closer and push embeddings of negative pairs apart by at least a margin.
        - **Triplet Loss**: Uses triplets (Anchor, Positive, Negative) to ensure the anchor is closer to the positive than to the negative by a margin. (Triplet Networks are a variation of Siamese architecture).
        - **Binary Cross-Entropy**: If the network outputs a similarity score (e.g., via a sigmoid after distance calculation), BCE can be used with target labels (1 for similar, 0 for dissimilar).
    - **Weight Sharing**: Crucially, the weights of the two subnetworks are shared and updated together during training. This ensures that both inputs are processed and mapped to the embedding space in exactly the same way.

## 5. Why Use Siamese Networks?
    - **Effective with Small Data (per class)**: Learns a *similarity function* rather than trying to learn distinct class boundaries for many classes. This makes it suitable for scenarios with few examples per class (e.g., One-Shot Learning).
    - **Good for Verification Tasks**: Ideal for determining if two items are the same (e.g., face verification, signature matching, fingerprint matching).
    - **Generalizes to New, Unseen Classes without Retraining**: Once trained to understand "similarity," it can compare instances of classes it wasn't explicitly trained on, as long as the feature extractor is general enough.
        - *Example*: A Siamese network trained on animal image pairs can compare two new, unseen animal species for similarity without needing retraining on those specific species.
    - **Efficient (Inference & Storage)**:
        - For verification, only one reference embedding per class needs to be stored.
        - Comparison of embeddings is computationally fast.
    - **Robust to Variations**: Can learn to be robust to changes in lighting, pose, and appearance if trained with appropriate data augmentation and diverse pairs.

## 6. Siamese Networks vs. Traditional Classifiers

| Feature          | Traditional CNN Classifier                     | Siamese Network (with CNNs)                      |
|------------------|------------------------------------------------|---------------------------------------------------|
| **Goal**         | Learns to classify input into fixed categories | Learns to compare inputs and determine similarity |
| **Training Data**| Requires many labeled images per class         | Trained on *pairs* of images (similar/different)  |
| **Output**       | Probability distribution over known classes    | A similarity score or distance between embeddings |
| **Inference (New Class)** | Needs retraining to recognize a new class    | Can compare unseen classes without retraining     |

## 7. Use Cases
    - **Face Verification**: Smartphone unlock, access control.
    - **Signature Verification**: Detecting forged signatures.
    - **Handwriting Recognition/Verification**.
    - **Object Tracking**: Comparing an object patch in consecutive frames.
    - **Image Retrieval**: Finding similar images in a database.
    - **Plagiarism Detection**: Comparing text document embeddings.
    - **Anomaly Detection**: Identifying if a new sample is significantly different from known samples.

## 8. Key Points Summary
    - **Identical Networks with Shared Weights**.
    - **Feature Extraction** into embeddings.
    - **Embedding Comparison** (e.g., Euclidean distance).
    - **Similarity Measure**: Small distance = similar, large distance = different.
    - **Decision Making** based on a threshold.
    - Learns a **similarity function**, not individual classes.