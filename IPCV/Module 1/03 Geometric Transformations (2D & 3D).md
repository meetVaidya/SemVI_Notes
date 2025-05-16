## 1. Definition
- Operations that alter the geometry (position, orientation, size, shape) of objects.
- Typically represented by matrices.
- In 2D, points $(x,y)$ are transformed. In 3D, points $(x,y,z)$ are transformed.
- **Homogeneous Coordinates** are often used to represent all transformations (including translation) as matrix multiplications. (See [[06 Coordinate Systems]])

## 2. Common Types of Transformations

### a. Translation
- **Definition**: Moves an object from one location to another without changing its shape or orientation.
- **Parameters**: $(t_x, t_y)$ in 2D; $(t_x, t_y, t_z)$ in 3D.
- **Equations (Non-homogeneous)**:
  - $x' = x + t_x$
  - $y' = y + t_y$
  - $z' = z + t_z$ (for 3D)

### b. Scaling
- **Definition**: Changes the size of an object.
- **Parameters**: $(S_x, S_y)$ in 2D; $(S_x, S_y, S_z)$ in 3D.
  - $S > 1$: Enlargement
  - $0 < S < 1$: Reduction
  - $S < 0$: Reflection + Scaling
- **Equations (Non-homogeneous, about origin)**:
  - $x' = x \times S_x$
  - $y' = y \times S_y$
  - $z' = z \times S_z$ (for 3D)

### c. Rotation
- **Definition**: Rotates an object around a fixed point (2D) or axis (3D).
- **Parameters**: Angle $\theta$. In 3D, also the axis of rotation (X, Y, or Z).
- **2D Rotation (about origin)**:
  - $x' = x \cos \theta - y \sin \theta$
  - $y' = x \sin \theta + y \cos \theta$
- **3D Rotation**: Matrices differ based on the axis (X, Y, Z). Positive rotation often follows the right-hand rule.
  - **X-axis rotation**:  
    $$y' = y \cos \theta - z \sin \theta$  
    $$$$z' = y \sin \theta + z \cos \theta$$
    $$x' = x$$
  - **Y-axis rotation**:  
    $$z' = z \cos \theta - x \sin \theta$$  
    $$x' = z \sin \theta + x \cos \theta$$  
    $$y' = y$$
  - **Z-axis rotation**:  
    $$x' = x \cos \theta - y \sin \theta$$
    $$y' = x \sin \theta + y \cos \theta$$
    $$z' = z$$

### d. Shearing
- **Definition**: Distorts the shape of an object by slanting it. Parallel lines remain parallel, but angles change.
- **Example**: Skewing a rectangle into a parallelogram.
- **Parameters**: Shear factors (e.g., $SH_x$ relative to y-axis, $SH_y$ relative to x-axis).

### e. Reflection
- **Definition**: Flips an object over an axis (2D) or a plane (3D), creating a mirror image.
- **3D Reflection**: Reflection about an axis is equivalent to a 180° rotation around that axis.

## 3. 3D Transformation Matrices (Homogeneous Coordinates - 4x4)
- **Translation Matrix**: Identity matrix with $t_x, t_y, t_z$ in the last column.
- **Scaling Matrix**: Diagonal matrix with $S_x, S_y, S_z, 1$.
- **Rotation Matrices**: More complex, involving $\sin \theta$ and $\cos \theta$ terms depending on the axis.

## 4. Applications
- Computer Graphics: Modeling, animation, rendering.
- Robotics: Robot arm movement, navigation.
- AR/VR: Placing virtual objects, tracking.
- Image Processing: Image registration, rectification.