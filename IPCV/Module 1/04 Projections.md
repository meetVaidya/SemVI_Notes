## 1. Geometric Projective (Projective Geometry)
- **Definition**: A branch of geometry dealing with properties that are invariant under projective transformations. It's how 3D objects are mapped to a 2D plane (the image).
- **Key Concept**: Focuses on properties that remain unchanged even when objects are projected or transformed.
- **Vanishing Point**: In perspective projection, parallel lines in 3D space appear to converge at a vanishing point on the 2D image plane.  
  - *Example*: Railway tracks appearing to meet at the horizon. The *fact* they are parallel in 3D is an invariant property.

## 2. Types of Projections

### a. Parallel Projection
- **Definition**: Projectors (lines from object vertices to projection plane) are parallel to each other.
- **Characteristics**:
  - Preserves relative proportions of objects.
  - Does not provide a realistic sense of depth (objects don't get smaller with distance).
- **Orthographic Projection (Sub-type)**:
  - Projectors are perpendicular to the projection plane.
  - Used for engineering drawings, architectural plans, some 2D games.
  - Shows true size and shape of faces parallel to the projection plane.
  - No perspective distortion; objects appear same size regardless of distance.

### b. Perspective Projection
- **Definition**: Projectors converge at a single point called the Center of Projection (COP) or viewpoint (like the camera lens or eye).
- **Characteristics**:
  - Produces realistic views, objects farther away appear smaller.
  - Lines not parallel to the projection plane converge to vanishing points.
- **Types based on number of principal axes intersected by projection plane / number of vanishing points**:
  - **1-Point Perspective**: One principal axis intersects projection plane (e.g., looking down a straight road). One vanishing point.
  - **2-Point Perspective**: Two principal axes intersect (e.g., looking at the corner of a building). Two vanishing points.
  - **3-Point Perspective**: Three principal axes intersect (e.g., looking up at a tall building or down from above). Three vanishing points.

## 3. Full Perspective Projection vs. Weak Perspective Projection

### Full Perspective Projection
- **Also known as**: True Perspective Projection.
- **Accuracy**: Accurately models how objects appear to the human eye/camera.
- **Depth Handling**: Uses the actual depth ($Z$) of each point to determine its projected size.
  - $x_{proj} = f \times \frac{X_{world}}{Z_{world}}$
  - $y_{proj} = f \times \frac{Y_{world}}{Z_{world}}$
  - (where $f$ is focal length, $(X,Y,Z)_{world}$ are 3D world coordinates)
- **Scaling**: Changes for each point based on its $Z$ depth.
- **Realism**: More realistic.

### Weak Perspective Projection
- **Nature**: A simplified approximation of full perspective projection.
- **Assumption**: Assumes all objects (or points on an object) are at a similar, average depth ($Z_{avg}$) from the camera.
- **Depth Handling**: Uses an average depth to calculate a single scaling factor $s = \frac{f}{Z_{avg}}$.
  - $x_{proj} = s \times X_{world}$
  - $y_{proj} = s \times Y_{world}$
- **Scaling**: Constant for all points (objects scale uniformly). $Z$-depth of individual points is ignored for scaling.
- **Realism**: Less accurate but computationally simpler/faster. Good approximation when object depth is small compared to its distance from the camera.

## 4. Perspective Distortion
- **Definition**: The visual effect where objects appear to change in size and shape based on their distance from the camera and the lens's focal length.
- **Types**:
  - **Wide-Angle (Barrel) Distortion**: Objects closer to the camera appear disproportionately larger. Straight lines near the edges of the frame may appear curved outwards. (Common in selfies with wide-angle front cameras).
  - **Telephoto (Compression) Distortion**: Distant objects appear closer together and "flatter," reducing the perceived depth between them. (e.g., cyclists in a race appearing tightly packed).