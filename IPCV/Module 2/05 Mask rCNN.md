# Mask R-CNN and RoIAlign

## 1. Mask R-CNN: Overview
- **Purpose**: Extends Faster R-CNN to perform **instance segmentation**.
- **Instance Segmentation**: Not only detects and classifies individual objects (like object detection) but also generates a pixel-wise segmentation mask for *each distinct instance* of an object.
    - *Contrast with Semantic Segmentation*: Semantic segmentation assigns a class label to every pixel but doesn't distinguish between instances of the same class.
- **Architecture**: Builds upon Faster R-CNN.
    - **Backbone Network**: Extracts features (e.g., ResNet, FPN).
    - **Region Proposal Network (RPN)**: Generates candidate object bounding boxes (RoIs).
    - **Key Addition**: A third parallel branch (the "mask head") in addition to the classification and bounding box regression heads.
        - **Classification Head**: Predicts object class.
        - **Bounding Box Regression Head**: Refines bounding box coordinates.
        - **Mask Prediction Head**: For each RoI, outputs a binary mask (pixel-wise) indicating which pixels within the RoI belong to the object. This is typically a small FCN (Fully Convolutional Network) applied per RoI.

## 2. Problem with RoI Pooling for Masks
- **RoI Pooling (used in Fast/Faster R-CNN)**:
    - Involves quantizing RoI coordinates to align with the discrete grid of the feature map.
    - Then, divides the RoI into a fixed number of spatial bins and performs max pooling within each bin.
- **Misalignment Issue**: The quantization (rounding) steps lead to misalignment between the RoI and the extracted features.
- **Impact**: While this misalignment might be tolerable for coarse tasks like classification and bounding box regression, it significantly degrades the quality of pixel-accurate segmentation masks. Spatial information is lost.

## 3. RoIAlign: Solution for Accurate Mask Prediction
- **Purpose**: To address the misalignment caused by RoI Pooling and extract features more precisely for instance segmentation.
- **How it Works**:
    1. **No Quantization**: RoI boundaries (which can be floating-point values) are not rounded. The feature map is treated as a continuous signal.
    2. **Sampling Grid**: For each RoI, a grid of $k \times k$ bins is defined (e.g., 7x7 or 14x14 for masks). Within each bin, a fixed number of sampling points are chosen (e.g., 4 points).
    3. **Bilinear Interpolation**: The feature values at these exact floating-point sampling point locations are computed using bilinear interpolation from the four nearest grid points on the feature map.
        - **Bilinear Interpolation Steps (for a point $(x,y)$ with fractional coordinates)**:
            - Identify the four nearest integer grid points: $V_{00}, V_{10}, V_{01}, V_{11}$.
            - Compute horizontal offsets $dx$ and vertical offsets $dy$ from the top-left grid point.
            - Interpolate:  
              $$ V(x,y) = (1 - dx)(1 - dy)V_{00} + dx(1 - dy)V_{10} + (1 - dx)dyV_{01} + dx \cdot dy \cdot V_{11} $$
    4. **Aggregation**: The interpolated values from the sampling points within each bin are aggregated (e.g., by max pooling or average pooling) to produce a single value for that bin.
- **Result**: Produces a fixed-size feature map for each RoI with much better spatial alignment, leading to significantly improved mask quality.
- **Differentiability**: The entire RoIAlign process, including bilinear interpolation, is differentiable, allowing end-to-end training.

## 4. Mask R-CNN Workflow Summary
1. **Feature Extraction**: Input image -> Backbone CNN (e.g., ResNet-FPN) -> Feature maps.
2. **Region Proposal**: Feature maps -> RPN -> Candidate RoIs.
3. **Feature Pooling**: RoIs + Feature maps -> **RoIAlign** -> Fixed-size feature vectors for each RoI.
4. **Parallel Heads**: Each RoI's feature vector is fed into:
    - Classifier (object category).
    - Bounding box regressor (refined box coordinates).
    - Mask predictor (FCN generating a binary mask for the object instance).
- **Loss Function**: Combined loss from classification, bounding box regression, and mask prediction (typically binary cross-entropy for masks).
