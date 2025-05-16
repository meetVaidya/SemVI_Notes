## 1. Definition
- A transformation that maps points from one plane to another in a perspective view.
- It's a 2D projective transformation.
- Represented by a **3x3 matrix (H)**.
- If $p = [x, y, 1]^T$ are homogeneous coordinates of a point on the first plane, and $p' = [x', y', w']^T$ are coordinates on the second plane, then  
  $$p' = H \times p$$  
  The actual 2D coordinates are  
  $$\left(\frac{x'}{w'}, \frac{y'}{w'}\right)$$
- Preserves straight lines (collinearity).

## 2. Planar Homography
- Specifically refers to the homography between two planes.
- Arises in scenarios like:
  - Viewing a planar surface (e.g., a floor, a wall, a piece of paper) from two different camera viewpoints.
  - Viewing a planar surface from one viewpoint, and then transforming it to a "rectified" view (e.g., top-down).

## 3. Homography Matrix (H)
- A 3x3 matrix with 8 degrees of freedom (DoF). (The 9th element is a scale factor, so $h_{33}$ is often set to 1).  
  $$H = \begin{bmatrix}
  h_{11} & h_{12} & h_{13} \\
  h_{21} & h_{22} & h_{23} \\
  h_{31} & h_{32} & h_{33}
  \end{bmatrix}$$
- Can represent various transformations including rotation, translation, scaling, shearing, and perspective warping.

## 4. Computation
- Requires at least **4 corresponding point pairs** between the two planes (no three of which are collinear).
- **Steps**:
  1. **Identify Correspondences**: Find at least 4 pairs of points $(x_i, y_i)$ in the source image and $(x'_i, y'_i)$ in the destination image/plane.
     - *Manual Selection*: User clicks on points.
     - *Automatic Detection*: Using feature detectors (SIFT, SURF, ORB) and matchers.
  2. **Set up Equations**: Each correspondence provides two linear equations involving the elements of $H$.
  3. **Solve for $H$**: Solve the system of linear equations (e.g., using Direct Linear Transform - DLT, or optimization methods like RANSAC to handle outliers).
     - OpenCV: `cv2.findHomography()`
     - Scikit-image: `transform.estimate_transform('projective', src, dst)`

## 5. Applications
- **Image Stitching**: Aligning multiple images to create a panorama. Homography maps overlapping regions.
- **Perspective Correction / Rectification**:
  - Document scanning (e.g., CamScanner): Transforming a skewed image of a document into a flat, top-down view.
  - Removing perspective distortion from images of planar surfaces.
- **Augmented Reality (AR)**: Overlaying virtual objects onto planar surfaces in the real world.
- **Camera Pose Estimation (relative to a plane)**: If the geometry of a planar object is known.
- **Visual Odometry/SLAM**: For planar scenes.
- **Art Digitization**: Rectifying photos of paintings/murals taken from different angles.

## 6. Warping
- The process of applying the homography transformation to an image, changing its appearance to align with a new viewpoint or to correct distortion.
- OpenCV: `cv2.warpPerspective()`