## 1. Case Study 1: AI Camera Traps for Wildlife
- **Scenario**: Detect tigers, elephants, leopards in forests. Accuracy is key, real-time processing not necessary.
- **Analysis**:
    - Need high accuracy for identification and localization.
    - Speed is secondary.
    - Instance segmentation (Mask R-CNN) might be overkill if only bounding boxes are needed.
- **Suggested Model**: Faster R-CNN.
    - **Reasoning**: Offers high accuracy. RPN makes it faster than R-CNN/Fast R-CNN. Suitable for offline analysis.

## 2. Case Study 2: Automated Defect Detection in Car Parts
- **Scenario**: Detect scratches, dents, missing components. Identify and classify defects.
- **Key Requirements**:
    - High accuracy (even minor defects).
    - Moderate processing speed (real-time helpful but not mandatory).
    - Precise localization of defect regions.
    - **Segmentation needed** to measure defect size and shape for severity assessment.
- **Suggested Model**: Mask R-CNN.
    - **Reasoning**: Provides both detection and instance segmentation, allowing for accurate localization and measurement of defect characteristics. Balances speed and precision adequately for quality control. Faster R-CNN would detect but not segment.

## 3. Case Study 3: Retail Theft Detection
- **Scenario**: AI surveillance for shoplifting. Detect suspicious behavior (hiding items), real-time alerts, recognize individual objects and people separately.
- **Key Requirements**:
    - Real-time performance.
    - Distinguish between people and objects they might be interacting with/hiding.
    - Instance-level understanding.
- **Suggested Model**: Mask R-CNN (if real-time constraints can be met by optimized versions or hardware) or a very fast instance segmentation model. If strictly bounding boxes and speed are paramount, a highly optimized Faster R-CNN or even a very accurate YOLO variant with good small object detection might be considered, but Mask R-CNN provides better scene understanding for "hiding items."
    - **Justification for Mask R-CNN**: Instance segmentation helps distinguish between a customer and an item they might be hiding. More detailed than just bounding boxes for analyzing actions.
    - **Caveat**: Real-time performance of Mask R-CNN can be a challenge; YOLOv8-seg or similar might be more practical for pure speed with segmentation.