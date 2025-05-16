## 1. Camera Parameters
- Values that define the geometric and optical characteristics of a camera.
- Crucial for tasks like 3D reconstruction, object tracking, AR.

### a. Intrinsic Parameters (Internal Properties)
- Define how the camera projects 3D world points onto the 2D image plane.
- **Represented by the Camera Matrix (K)**:  
  $$
  K = \begin{bmatrix}
  f_x & s & c_x \\
  0 & f_y & c_y \\
  0 & 0 & 1
  \end{bmatrix}
  $$
- **Components**:
  - **Focal Length $(f_x, f_y)$**:
    - Distance from the camera's optical center to the image plane, expressed in pixel units.
    - $f_x$ and $f_y$ can differ if pixels are not square.
    - Determines how strongly the lens converges/diverges light, affecting image scale.
  - **Principal Point $(c_x, c_y)$**:
    - Coordinates (in pixels) of the point where the optical axis intersects the image plane.
    - Ideally the center of the image, but often slightly offset.
  - **Skew Coefficient $(s)$**:
    - Accounts for non-perpendicularity (skew) between the x and y pixel axes.
    - Usually 0 for modern cameras (square pixels).
- **Distortion Coefficients**:
  - Account for imperfections in the lens that cause image distortions.
  - **Radial Distortion**: Lines appear curved.
    - *Barrel distortion*: Lines curve outwards (common in wide-angle lenses).
    - *Pincushion distortion*: Lines curve inwards (common in telephoto lenses).
    - Modeled by coefficients $k_1, k_2, k_3, \ldots$
  - **Tangential Distortion**: Occurs if lens and image plane are not parallel.
    - Modeled by coefficients $p_1, p_2$.

### b. Extrinsic Parameters (External Properties)
- Define the camera's position and orientation in the 3D world coordinate system.
- Describe the transformation from world coordinates to camera coordinates.
- **Components**:
  - **Rotation Matrix (R)**: A $3 \times 3$ matrix describing the camera's orientation (rotation) relative to the world.
  - **Translation Vector (t)**: A $3 \times 1$ vector describing the camera's position (translation) relative to the world origin.
- Together, $[R \mid t]$ form a $3 \times 4$ matrix that transforms 3D world points to 3D camera coordinates.

## 2. Camera Calibration
- **Definition**: The process of estimating the intrinsic and extrinsic parameters of a camera.
- **Why Calibrate?**:
  - To correct for lens distortion (undistort images).
  - To obtain accurate 3D measurements from 2D images.
  - Essential for 3D reconstruction, stereo vision, Structure from Motion (SfM).
- **General Steps (e.g., using a chessboard pattern)**:
  1. **Capture Images**: Take multiple images of a known calibration pattern (e.g., chessboard, ChArUco board) from different viewpoints and orientations.
  2. **Detect Pattern Corners**: For each image, accurately find the 2D pixel coordinates of known 3D points on the pattern (e.g., chessboard corners).
  3. **Estimate Parameters**:
     - Use the 2D-3D correspondences to solve for the camera matrix ($K$), distortion coefficients, and the extrinsic parameters ($R, t$) for each view.
     - Algorithms like Zhang's method are commonly used.
     - OpenCV: `cv2.calibrateCamera()`
  4. **Optimize/Refine**: Often involves non-linear optimization to minimize reprojection error (the distance between detected 2D points and projected 3D points).
  5. **Use Calibration Data**:
     - **Undistort Images**: `cv2.undistort()`
     - For 3D reconstruction, metric measurements.