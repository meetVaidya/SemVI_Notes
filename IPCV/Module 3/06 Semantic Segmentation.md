## 1. Definition
    - **Goal**: To assign a class label to **every pixel** in an image.
    - **Output**: A segmentation map where each pixel is colored based on the object class it belongs to.
    - **Distinction from other tasks**:
        - **Image Classification**: Assigns a single label to the entire image (e.g., "cat").
        - **Object Detection**: Locates objects with bounding boxes and classifies them (e.g., a box around a "cat").
        - **Instance Segmentation**: Detects, classifies, *and* provides a pixel-wise mask for *each distinct instance* of an object (e.g., differentiates between cat1, cat2).
        - **Semantic Segmentation**: Classifies each pixel (e.g., all cat pixels are labeled "cat," all grass pixels "grass," but doesn't distinguish between two different cats).

## 2. Key Characteristics
    - **Pixel-level Understanding**: Provides a dense, detailed understanding of the image content.
    - **No Instance Differentiation**: All objects of the same class share the same label/color in the output map.

## 3. Common Architectures
    - **Fully Convolutional Networks (FCNs)**:
        - Replace fully connected layers in classification CNNs with convolutional layers to maintain spatial information and output a heatmap.
        - Use upsampling layers (e.g., transposed convolutions or "deconvolutions") to restore the feature map to the original image resolution for pixel-wise classification.
    - **Encoder-Decoder Architectures**:
        - **Encoder**: A typical CNN (e.g., VGG, ResNet) that downsamples the input, extracting hierarchical features (capturing semantic information).
        - **Decoder**: Upsamples the low-resolution feature maps from the encoder back to the original image resolution, progressively refining spatial details.
        - **Skip Connections**: Often used to connect encoder features to corresponding decoder layers (e.g., U-Net architecture). This helps the decoder recover fine-grained spatial information lost during downsampling.
    - **U-Net**: A popular encoder-decoder architecture, especially in medical imaging, characterized by its U-shape and extensive use of skip connections.
    - **DeepLab Family**: Uses Atrous (dilated) convolutions to increase the receptive field without losing resolution, and Conditional Random Fields (CRFs) for refining segmentation boundaries.

## 4. Applications
    - **Autonomous Driving**: Understanding road scenes (identifying road, lanes, pedestrians, vehicles, sidewalks).
    - **Medical Image Analysis**: Segmenting organs, tumors, lesions in CT scans, MRIs, X-rays.
    - **Satellite Imagery Analysis**: Land cover classification, urban planning.
    - **Robotics**: Scene understanding for navigation and interaction.
    - **Augmented Reality**: Separating foreground from background for realistic object insertion.