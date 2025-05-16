## 1. LSI System Definition
- A system that possesses two key properties: Linearity and Shift-Invariance.
- **Why a lens is considered an LSI system (idealized)**: It (ideally) behaves consistently regardless of where an object is placed or how much light is used (within limits).

## 2. Linearity Properties
- **a. Superposition**:
  - **Principle**: The response to a sum of inputs is the sum of the responses to each input individually.
  - **Lens Context**: If multiple light sources illuminate a scene, the image formed is the sum of the images that would be formed by each light source independently.  
    - *Example*: Red light source forms a red image component, blue light source forms a blue image component. Both on → image is sum of red and blue components.
- **b. Scaling (Homogeneity)**:
  - **Principle**: If the input is scaled by a factor, the output is scaled by the same factor.
  - **Lens Context**:
    - Double the brightness of an object (light source) → image brightness doubles.
    - Double the size of an object (if lens magnifies linearly) → image size doubles.

## 3. Shift Invariance
- **Principle**: Shifting the input in space (or time) results in an identical shift in the output.
- **Lens Context**: If an object is moved (shifted) in front of the lens, the image formed on the sensor shifts by a corresponding amount without changing its form (ideally).  
  - *Example*: Move a ball and a car together to the left; the entire image shifts to the left.

## 4. Importance
- Simplifies the analysis of optical systems.
- Allows the use of powerful mathematical tools like convolution (the output of an LSI system is the convolution of the input with the system's impulse response/Point Spread Function).