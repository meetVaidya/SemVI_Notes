## 1. Definition
- A framework used to define the position of points or objects in space using numbers (coordinates).
- Consists of reference axes and a method to describe a point's position relative to these axes.

## 2. Types of Coordinate Systems

### a. Cartesian Coordinate System
- **2D**: $(x, y)$ - Two perpendicular axes.
- **3D**: $(x, y, z)$ - Three mutually perpendicular axes.
- **Origin**: $(0,0)$ or $(0,0,0)$.
- **Quadrants/Octants**: Regions defined by the axes.

### b. Polar Coordinate System (2D)
- **Definition**: Describes a point by its radial distance $(r)$ from the origin and an angle $(\theta)$ relative to a reference direction (usually the positive x-axis).
- **Representation**: $(r, \theta)$.
- *Example*: $(r=5, \theta=45^\circ)$ means 5 units away at a 45° angle.

### c. Spherical Coordinate System (3D)
- **Definition**: Describes a point in 3D space by:
  - **Radius $(r)$**: Distance from the origin.
  - **Polar Angle $(\theta)$ or Zenith Angle**: Angle from the positive z-axis.
  - **Azimuthal Angle $(\phi)$**: Angle from the positive x-axis in the xy-plane.
- **Representation**: $(r, \theta, \phi)$.

### d. Homogeneous Coordinate System
- **Purpose**: To represent geometric transformations (especially translation) as matrix multiplications, and to handle points at infinity (useful in projective geometry).
- **Representation**:
  - A 2D point $(x, y)$ becomes $(x', y', w) = (w x, w y, w)$. Typically $w=1$, so $(x, y, 1)$.
  - A 3D point $(x, y, z)$ becomes $(x', y', z', w) = (w x, w y, w z, w)$. Typically $w=1$, so $(x, y, z, 1)$.
- **Conversion back to Cartesian**: Divide by $w$:  
  $$\left(\frac{x'}{w}, \frac{y'}{w}\right) \quad \text{or} \quad \left(\frac{x'}{w}, \frac{y'}{w}, \frac{z'}{w}\right)$$
- **Advantages**:
  - **Unified Transformations**: All affine (linear + translation) and projective transformations can be represented by a single matrix multiplication.
    - In 2D, transformations use $3 \times 3$ matrices.
    - In 3D, transformations use $4 \times 4$ matrices.
  - **Points at Infinity**: When $w=0$, represents a point at infinity (direction).
- **Structure of 4x4 Transformation Matrix (3D Homogeneous)**:  
  $$
  \begin{bmatrix}
  R & \mathbf{T} \\
  \mathbf{P} & S
  \end{bmatrix}
  =
  \begin{bmatrix}
  R_{3\times3} & \begin{matrix} T_x \\ T_y \\ T_z \end{matrix} \\
  \begin{matrix} P_x & P_y & P_z \end{matrix} & S
  \end{bmatrix}
  $$
  - **Upper-left $3 \times 3$ (R)**: Rotation and Scaling components.
  - **Last column, top 3 $(T_x, T_y, T_z)$**: Translation components.
  - **Bottom row, first 3 $(P_x, P_y, P_z)$**: Perspective projection components.
  - **Bottom-right $(S)$**: Overall scaling factor (usually 1). For affine, bottom row is $[0 \quad 0 \quad 0 \quad 1]$.