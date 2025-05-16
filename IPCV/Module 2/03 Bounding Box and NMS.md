# Bounding Box Refinement and Non-Maximum Suppression (NMS)

## 1. Bounding Box Regression (General Concept in R-CNN family)
- **Purpose**: Initial region proposals (e.g., from Selective Search or RPN anchors) are often not perfectly aligned with the actual object. Bounding box regression refines these proposals to better fit the ground truth object.
- **How it works**:
  - Learns a transformation (offsets for center $x, y$ and scaling factors for $width, height$) to map a proposed box $P$ to a target ground truth box $G$.
  - **R-CNN Parameterization**:
    $$
    t_x = \frac{G_x - P_x}{P_w}
    $$
    $$
    t_y = \frac{G_y - P_y}{P_h}
    $$
    $$
    t_w = \log\left(\frac{G_w}{P_w}\right)
    $$
    $$
    t_h = \log\left(\frac{G_h}{P_h}\right)
    $$
  - The model predicts these $t_x, t_y, t_w, t_h$ values.
  - **Applying the transformation**:
    $$
    \hat{G}_x = P_w \cdot t_x + P_x
    $$
    $$
    \hat{G}_y = P_h \cdot t_y + P_y
    $$
    $$
    \hat{G}_w = P_w \cdot e^{t_w}
    $$
    $$
    \hat{G}_h = P_h \cdot e^{t_h}
    $$
- **Why Log-Space for Scale**: Ensures predicted width/height are positive and handles large scale variations more stably.
- **Stability**: Predicting offsets relative to an anchor/proposal is often more stable than predicting absolute coordinates directly.

## 2. Non-Maximum Suppression (NMS)
- **Problem**: Object detection models often predict multiple, overlapping bounding boxes for the same object, with varying confidence scores.
- **Purpose**: To filter out redundant bounding boxes and keep only the most accurate one for each detected object instance.
- **Algorithm**:
  1. Start with all predicted bounding boxes for a particular class, along with their confidence scores.
  2. Select the box with the **highest confidence score**. This is considered a true detection.
  3. Calculate the **Intersection over Union (IoU)** of this highest-confidence box with all other remaining boxes.
  4. Remove (suppress) any boxes that have an IoU with the selected box greater than a predefined **IoU threshold** (e.g., 0.5). These are considered duplicates of the same object.
  5. Repeat steps 2-4 with the remaining boxes until no boxes are left.
- **When NOT to Apply NMS (or use variants like Soft-NMS)**:
  - If highly overlapping boxes are known to represent *different distinct objects* (e.g., a stack of books where each book is detected). Standard NMS might incorrectly remove valid detections.
  - **Rule of Thumb**: Apply NMS if boxes refer to the *same object instance*. Don't apply (or use Soft-NMS) if they refer to *different objects*, even if overlapping.

## 3. Intersection over Union (IoU)
- **Definition**: A metric used to measure the extent of overlap between two bounding boxes (typically a predicted box and a ground truth box, or two predicted boxes in NMS).
- **Formula**:
  $$
  IoU = \frac{\text{Area of Intersection}}{\text{Area of Union}}
  $$
- **Range**: 0 (no overlap) to 1 (perfect overlap).
- **Calculation Steps**:
  1. **Define Boxes**: Each box defined by $(x_{min}, y_{min}, x_{max}, y_{max})$.
  2. **Compute Intersection Box Coordinates**:
     $$
     x_{\text{intersect\_min}} = \max(x_{min}^A, x_{min}^B)
     $$
     $$
     y_{\text{intersect\_min}} = \max(y_{min}^A, y_{min}^B)
     $$
     $$
     x_{\text{intersect\_max}} = \min(x_{max}^A, x_{max}^B)
     $$
     $$
     y_{\text{intersect\_max}} = \min(y_{max}^A, y_{max}^B)
     $$
  3. **Compute