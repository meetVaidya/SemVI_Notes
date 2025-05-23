#### Definition
- FPN is a neural network framework that builds a pyramid of features maps at different scales from a single input image, enabling the detection of objects across a wide range of sizes. It is commonly integrated into models like [[06 Faster rCNN|Faster R-CNN]], Mask R-CNN and RetinaNet.
- The primary goal of FPN is to improve detection of objects at multiple scales by combining high-resolution, low-level features (detailed spatial information) with low-resolution, high-level features (semantic information) within an unified pyramid structure.
- FPN is essential for tasks such as object detection and instance segmentation, where objects in an image can appear at drastically different sizes due to perspective or distance from the camera.

#### Architecture and Workflow of FPN
1. **Step 1: Input Image:**
2. **Step 2: Feature Maps Extraction:**
	- As the image propagates through the CNN, multiple feature maps are generated at different layers, each representing the image at varying resolutions.
	- Early layers produce high-resolution feature maps with detailed spatial information (e.g., edges, textures).
	- Deeper layers produce low-resolution feature maps with high-level semantic information (e.g., object categories, contexts).
3. **Step 3: FPN Pyramid Construction:**
	- FPN creates a feature pyramid by merging these multi-scale feature maps.
	- It uses a top-down pathway and lateral connections to combine low-resolution, semantically rich features from deeper layers with high-resolution, spatially accurate features from shallower layers.
	- **Top-Down Pathway**: Upsamples the coarser, deeper feature maps to higher resolutions.
	- **Lateral Connections**: Fuse detailed spatial information from corresponding shallower layers into the upsampled maps, ensuring both context and detail are preserved.
4. **Step 4: Prediction:**
	- The resulting multi-scale feature maps in the pyramid are used for downstream tasks such as object detection or segmentation.
	- Each level of the pyramid is responsible for detecting objects at a specific scale range, ensuring comprehensive coverage from small to large objects.
#### Key Features of FPN
- **Multi-Scale Feature Representation**: FPN creates a pyramid of features that combine spatial detail (from early layers) and semantic understanding (from later layers), making it adept at detecting objects of varying sizes.
- **Lateral Connections**: These connections ensure that high-resolution details are not lost during the upsampling of low-resolution feature maps, improving accuracy in localization tasks.
- **Efficiency**: FPN is computationally efficient as it builds the pyramid using existing CNN feature maps rather than reprocessing the raw image at multiple scales.
#### Applications of FPN
- **Object Detection**:
    - Integrated into frameworks like Faster R-CNN and RetinaNet, FPN enhances the ability to detect objects of different sizes in images, such as in video surveillance or automated inspection systems.
- **Semantic Segmentation**:
    - FPN supports semantic segmentation by providing multi-scale feature maps that aid in pixel-wise labelling, capturing both local details and global context.
- **Instance Segmentation**:
    - Used in models like Mask R-CNN, FPN facilitates instance segmentation by detecting individual object instances and generating precise masks, essential for tasks like autonomous driving (e.g., distinguishing between adjacent cars).
#### Advantages of FPN
- **Scale Invariance**: By addressing objects at multiple scales, FPN ensures robust performance in scenarios where object sizes vary significantly.
- **Improved Accuracy**: The fusion of low-level and high-level features enhances both localization (spatial precision) and classification (semantic understanding), leading to higher detection accuracy.
- **Versatility**: FPN can be integrated into various deep learning architectures (e.g., Faster R-CNN, Mask R-CNN, RetinaNet), making it a flexible component for multiple vision tasks.