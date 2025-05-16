## 1. Face Detection vs. Face Recognition

### Face Detection
- **Primary Objective**: To locate and delineate human faces within an image or video.
- **Output**: Bounding boxes or markers indicating the location and size of detected faces.
- **Algorithms**: Viola-Jones (Haar cascades), HOG + SVM, Deep Learning models (e.g., MTCNN, SSD, YOLO).
- **Question it answers**: "Are there any faces in this image, and where are they?"

### Face Recognition
- **Primary Objective**: To identify or verify an individual based on their facial features.
- **Input**: A detected face.
- **Output**: The identity (name) of the person, or a confirmation if it matches a known identity, along with a confidence score.
- **Process**:
  1. Face Detection.
  2. Facial Feature Extraction / Embedding (e.g., using Eigenfaces, Fisherfaces, Deep Learning models like FaceNet, ArcFace to create a compact vector representation).
  3. Matching/Classification against a database of known faces.
- **Question it answers**: "Whose face is this?"

## 2. Real-time Performance of Instagram Filters

- **Challenge**: Applying complex visual effects (filters) smoothly in real-time on diverse mobile devices with varying lighting conditions.
- **Key Techniques**:
  - **Lightweight Deep Learning Models**: For real-time face tracking and facial feature (landmark) detection (e.g., MediaPipe Face Mesh). These models are optimized for speed and efficiency.
  - **Mobile-Optimized Frameworks**: TensorFlow Lite, Core ML, allow efficient execution of ML models on lower-end devices.
  - **Efficient Segmentation**: Algorithms (e.g., U-Net variants) to accurately segment parts of the face or scene for applying effects precisely (e.g., lipstick, hair color).
  - **Depth Sensing (if available)**: Some phones have depth sensors (e.g., LiDAR, ToF) that provide depth information for more realistic filter placement and occlusion.
  - **Graphics APIs**:
    - **Metal (iOS), Vulkan (Android)**: Low-level graphics APIs providing high-performance access to the GPU for rendering complex effects.
    - Device-specific optimizations.
  - **Optimized Rendering Engines**: Instagram's AR engine (Meta Spark AR) is designed for real-time rendering of AR effects.
  - **Pre-computation and Look-Up Tables (LUTs)**: For color transformations and some effects to speed up processing.
  - **Adaptive Algorithms**: Adjusting filter complexity or quality based on device capabilities or processing load.