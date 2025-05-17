## 1. Introduction to Attention
- **Core Idea**: A mechanism that allows a neural network to selectively focus on the most relevant parts of an input while processing it, rather than treating all parts equally.
- **Inspiration**: Human visual attention – we don't process an entire scene with uniform detail; our eyes and brain focus on salient regions.
- **Benefits**:
	- Improves model performance by concentrating computational resources on important information.
	- Helps handle long sequences or large inputs by highlighting critical segments.
	- Can provide insights into model interpretability by showing where the model "looks."
- **Examples Illustrating Need for Attention**:
	- **Image Understanding**: Finding a specific person/object in a crowded photo (humans don't scan pixel-by-pixel).
	- **Machine Translation (e.g., Google Translate)**:
		- *Old RNNs*: Translated word-by-word, leading to grammar/meaning loss (e.g., "He went to the bank to withdraw money." -> literal translation might miss context of "bank").
		- *Attention-based*: Focuses on relevant phrases (e.g., "withdraw money" together), understands context ("bank" as financial institution), reorders words properly.
	- **Autocorrect**: Needs context beyond nearby words to correct "bark" to "park" in "I am going to the bark later."
	- **Recommendation Systems (Netflix, YouTube)**: Focuses on relevant parts of user history (e.g., "thriller-like" aspects) rather than treating all past interactions equally.

## 2. Self-Attention
- **Definition**: A specific type of attention mechanism where elements within a *single sequence* (or set of elements, like image patches) attend to each other to compute a representation of that sequence.
- **Mechanism**: Each element calculates "attention scores" with every other element in the input, determining how much focus to place on other elements when computing its own updated representation.
- **Key in Transformers**: The foundational component of Transformer architectures.

## 3. Attention Models in Computer Vision
- **Why Attention in Vision?**:
	- Allows models to focus on important regions or features in an image, ignoring irrelevant background or clutter.
	- Can capture long-range dependencies between distant parts of an image.
- **Types of Attention Mechanisms in Vision**:
	- **Spatial Attention**: Identifies *which regions* in an image are important. Generates a spatial attention map that highlights salient areas.
	- **Channel Attention**: Determines *which feature channels* (output by convolutional layers) are more relevant. Assigns different weights to different channels.
	- **Self-Attention (Transformer-based)**: Computes relationships between all pixels or image patches, allowing global context understanding.
- **Popular Architectures Incorporating Attention**:
	- **SE-Net (Squeeze-and-Excitation Networks)**: Focuses on Channel Attention.
	- **CBAM (Convolutional Block Attention Module)**: Combines Spatial and Channel Attention.
	- **Vision Transformers (ViTs)**: Primarily use Self-Attention, largely replacing traditional CNN convolutional layers.

## 4. SE-Net (Squeeze-and-Excitation Networks)
- **Type**: Channel Attention.
- **Goal**: To explicitly model interdependencies between channels of convolutional features, adaptively recalibrating channel-wise feature responses.
- **Mechanism**:
	1.  **Squeeze Operation**:
		- Takes a feature map (output of a convolutional block) with dimensions `H x W x C`.
		- Compresses each channel `C` into a single scalar descriptor using **Global Average Pooling (GAP)**. This results in a `1 x 1 x C` vector representing channel-wise statistics.
		- GAP: Shrinks each feature map channel to a single value by averaging all its pixel values.
	2.  **Excitation Operation**:
		- The `1 x 1 x C` descriptor from Squeeze is fed through a small neural network (typically two Fully Connected layers with a ReLU and a Sigmoid activation).
		- This network learns to output a set of channel-wise attention weights (scores between 0 and 1 for each channel), indicating the importance of each channel.
	3.  **Recalibration (Scaling) Operation**:
		- The original feature map channels are multiplied (scaled) by their corresponding learned attention weights from the Excitation step.
		- Important channels are enhanced (weights close to 1), while less important ones are suppressed (weights close to 0).
- **Example**: In an image of a "cat on grass," SE-Net might learn to increase the importance (weight) of channels that respond to "fur texture" features while reducing the importance of channels related to "background color."

## 5. CBAM (Convolutional Block Attention Module)
- **Type**: Combines Channel Attention and Spatial Attention.
- **Goal**: To improve feature representation by inferring attention maps along two separate dimensions (channel and spatial) and then multiplying these maps with the input feature map for adaptive feature refinement.
- **Mechanism (typically sequential: Channel then Spatial, or vice-versa)**:
	1.  **Channel Attention Module**:
		- Similar to SE-Net, it learns which channels are important.
		- Often uses both Global Average Pooling (GAP) and Global Max Pooling (GMP) on the input feature map to generate channel descriptors.
		- These descriptors are fed through a shared multi-layer perceptron (MLP) to produce channel attention weights.
	2.  **Spatial Attention Module**:
		- Learns which spatial regions of the image (or feature map) are important.
		- Often applies average pooling and max pooling across the *channels* of the feature map (output by the channel attention module) to get two 2D spatial descriptors.
		- These descriptors are concatenated and passed through a convolutional layer to generate a 2D spatial attention map.
	3.  **Multiplication (Applying Attention)**:
		- The input feature map is first multiplied by the channel attention weights.
		- The resulting feature map is then multiplied by the spatial attention map.
		- This enhances important features in relevant channels and spatial locations, while suppressing irrelevant ones.
- **Example**: For a cat in a crowded image, Channel Attention might prioritize "fur texture" channels, and Spatial Attention might highlight the region where the cat's body is located.

## 6. Vision Transformers (ViTs)
- **Core Idea**: Apply the Transformer architecture (originally successful in NLP) directly to image recognition tasks, largely replacing the convolutional layers of CNNs with **self-attention mechanisms**.
- **Working Principle**:
	1.  **Splitting Image into Patches**:
		- The input image (e.g., 224x224 pixels) is divided into a sequence of fixed-size, non-overlapping (or minimally overlapping) patches (e.g., 16x16 pixels each).
		- For a 224x224 image and 16x16 patches, this results in `(224/16) * (224/16) = 14 * 14 = 196` patches.
		- **Stride**: The distance the "patch window" moves. If stride = patch size, there's no overlap.
	2.  **Flattening Patches**: Each 2D patch (e.g., 16x16x3 for RGB) is flattened into a 1D vector (e.g., `16*16*3 = 768` elements). These are treated as "tokens," analogous to words in NLP.
	3.  **Linear Projection (Patch Embedding)**:
		- Each flattened patch vector is linearly projected into a fixed-dimensional embedding space (e.g., D=768 for ViT-Base). This is done using a learnable weight matrix `E`.
		- `Z_patch = Patch_vector * E`
	4.  **Adding Positional Embeddings**:
		- Since self-attention is permutation-invariant (doesn't inherently know the order/position of patches), learnable positional embeddings are added to the patch embeddings to incorporate spatial information.
	5.  **Prepending [CLS] Token (Optional but common for classification)**:
		- A special learnable embedding, the `[CLS]` (classification) token, is often prepended to the sequence of patch embeddings. The final representation of this token from the Transformer encoder is used for image classification.
	6.  **Transformer Encoder**:
		- The sequence of (patch embeddings + positional embeddings) is fed into a stack of Transformer encoder layers.
		- Each Transformer encoder layer typically consists of:
			- **Layer Normalization**.
			- **Multi-Head Self-Attention (MHSA)**: Allows each patch embedding to attend to all other patch embeddings in the sequence, capturing global relationships and context. It computes "Query," "Key," and "Value" vectors for each patch and calculates weighted sums of Values based on Query-Key similarities. "Multi-Head" means doing this in parallel with different learned projections.
			- **Residual Connection**.
			- **Layer Normalization**.
			- **MLP (Feed-Forward Network)**: Applied independently to each patch representation.
			- **Residual Connection**.
	7.  **Final Classification Head**:
		- The output representation corresponding to the `[CLS]` token (or an average of all patch outputs) from the final Transformer encoder layer is passed through an MLP (Multi-Layer Perceptron) head to produce the final class probabilities (e.g., using a softmax function).
- **Self-Attention Importance in ViT**:
	- **Global Context**: Captures relationships between distant parts of the image because every patch can attend to every other patch.
	- **Flexibility**: Can attend to any part of the image dynamically based on content.
	- **Scalability**: Transformers scale well with model size and data, often outperforming CNNs on very large datasets (though they may require more data to train effectively from scratch than CNNs).
- **Choosing Patch Size**:
	- **Smaller patch size**: More patches, higher computational cost, potentially better fine-grained feature extraction.
	- **Larger patch size**: Fewer patches, faster, might lose fine details. Typical: 16x16 or 32x32.
- **ViT Applications**: Image classification, object detection (e.g., DETR uses a Transformer encoder-decoder), segmentation (e.g., Segmenter, MaskFormer), image generation.
