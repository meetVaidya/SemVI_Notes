## 1. Basic Definitions (from a classification context)
- **True Positive (TP)**: Model correctly predicts the presence and class of an object, and the bounding box sufficiently overlaps with the ground truth (IoU > threshold).
- **False Positive (FP)**:
    - Model predicts an object where there is none (background).
    - Model predicts an object of the correct class, but the bounding box has poor overlap with ground truth (IoU < threshold).
    - Model predicts an object of the wrong class.
- **False Negative (FN)**: Model fails to detect an object that is present in the ground truth.
- **True Negative (TN)**: Model correctly identifies a region as background. *Note: TN is generally not directly used in standard object detection mAP calculation but is conceptually important for understanding.*

## 2. Precision
- **Formula**:  
    $$\text{Precision} = \frac{TP}{TP + FP}$$
- **Interpretation**: Of all the objects the model *detected* for a class, what fraction was actually correct?  
  High precision means the model makes few false positive detections.

## 3. Recall (Sensitivity)
- **Formula**:  
    $$\text{Recall} = \frac{TP}{TP + FN}$$
- **Interpretation**: Of all the *actual objects* of a class present in the ground truth, what fraction did the model correctly detect?  
  High recall means the model finds most of the relevant objects.

## 4. Precision-Recall Curve
- **Concept**: Object detection models typically output a confidence score for each detection. By varying the confidence threshold, we get different sets of TPs and FPs, leading to different precision and recall values.
- **Plot**: Recall is plotted on the x-axis, and Precision on the y-axis.
- **Shape**: Ideally, the curve stays high in the top-right corner (high precision and high recall).

## 5. Average Precision (AP)
- **Definition**: A single number summarizing the Precision-Recall curve for a *specific object class* and a *specific IoU threshold*. It is the area under the (interpolated) Precision-Recall curve.
- **Calculation Steps**:
    1. **Sort Detections**: For a given class, sort all predicted bounding boxes by their confidence scores in descending order.
    2. **Assign TP/FP**: Iterate through the sorted detections. For each detection:
        - Compare it with ground truth boxes of the same class that haven't been matched yet.
        - If IoU with a ground truth box >= IoU threshold (e.g., 0.5), it's a TP (and that ground truth box is marked as detected).
        - Otherwise, it's an FP.
    3. **Calculate Precision and Recall**: At each detection, calculate cumulative TP, FP, and then current precision and recall.
    4. **Interpolate Precision**: To create a monotonically decreasing PR curve, for each recall value $$r$$, the interpolated precision $$P_{\text{interp}}(r)$$ is the highest precision found for any recall value $$r' \geq r$$.
    5. **Compute Area**: AP is the area under this interpolated PR curve. Common methods:
        - **11-Point Interpolation (PASCAL VOC pre-2010)**: Average precision at 11 equally spaced recall levels (0, 0.1, ..., 1.0).
        - **All-Point Interpolation (PASCAL VOC post-2010, COCO)**: Calculate area by summing $$ (\text{Recall}_i - \text{Recall}_{i-1}) \times \text{Precision}_i $$ over all unique recall points where precision changes.
- **Significance**: Provides a balanced measure of a model's performance for a single class.

## 6. Mean Average Precision (mAP)
- **Definition**: The primary metric for evaluating object detection models across multiple object classes and/or multiple IoU thresholds.
- **Calculation**:
    - **Standard mAP (e.g., PASCAL VOC style)**: Calculate AP for each object class (at a fixed IoU threshold, typically 0.5). Then, mAP is the mean of these APs.  
      $$\text{mAP@0.5}$$ or $$\text{mAP50}$$.
    - **COCO mAP**: Calculate AP for each class at 10 different IoU thresholds (from 0.5 to 0.95 with a step of 0.05). Average these APs across all classes and all 10 IoU thresholds. This is a more stringent metric.  
      Also reported: $$\text{mAP@0.75}$$ (mAP at IoU=0.75), $$\text{mAP}_{\text{small}}$$, $$\text{mAP}_{\text{medium}}$$, $$\text{mAP}_{\text{large}}$$.
- **Significance**: Provides a single, comprehensive score for overall model performance.

## 7. Computational Efficiency
- **Inference Time**: How long the model takes to detect objects in a single image (Frames Per Second - FPS). Critical for real-time applications.
- **Memory Usage**: Amount of RAM/VRAM required by the model, important for deployment on resource-constrained devices.

## 8. Qualitative Analysis
- **Visualization of Bounding Boxes**: Visually inspect if predicted boxes align well with ground truth.
- **Failure Cases Analysis**: Identify types of errors:
    - False Positives (detecting non-objects or wrong class).
    - False Negatives (missing objects).
    - Localization errors (correct class but poor bounding box).
    - Confusion between similar classes.
