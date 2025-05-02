## Kinematic Models
#### Definition
- Kinematic models are mathematical representations used in motion analysis to describe how objects or systems move over time, focusing solely on their position, velocity, and orientation without considering the forces or torques causing the motion.
- kinematic models are categorized into three main types depending on the complexity of the object and motion being analyzed: **Point Mass Model**, **Rigid Body Model**, and **Articulated Body Model**.

##### 1. Point Mass Model
- This is the simplest kinematic model, where an object is treated as a single point with all its mass concentrated at that point. The size, shape and rotational aspects of the object are ignored.
- **Key Characteristics**:
    - Focuses only on the movement of the object's center point.
    - Rotational effects are not considered since the object is reduced to a dimensionless point.
    - Useful for scenarios where the object's dimensions are negligible compared to the distance it travels.
- **Example from Document**: Imagine an ant moving on the ground. You don't consider its legs or antennas; you just track its body as a single point moving around.
- **Applications**: Simplifying calculations for large or complex objects where only position and linear motion matter, such as tracking a car's center of mass over a long distance in traffic analysis.
- **Limitations**: Cannot account for rotational motion or detailed shape dynamics, making it unsuitable for complex systems.

##### 2. Rigid Body Model
- This model assumes that the object is a solid entity whose shape and size do not change during motion. Every point in the object maintains a fixed distance from every other point.
- **Key Characteristics**:
    - Accounts for both translational motion (movement in a straight line) and rotational motion (spinning around an axis).
    - Considers the object's shape, size, and orientation, unlike the point mass model.
- **Example from Document**: Think of a toy car. No matter how you push or pull it, the car doesn't bend or stretch; it moves as one solid piece.
- **Applications**: Used in scenarios where rotation and orientation are important, such as analyzing the motion of a satellite in space or a gymnast performing a flip.
- **Advantages over Point Mass**: Captures more realistic motion by including rotation, making it suitable for objects with significant shape and orientation changes during movement.
- **Limitations**: Fails to represent objects that deform or have independently moving parts.

##### 3. Articulated Body Model
- This model represents complex objects as a collection of rigid bodies connected by joints, allowing relative motion between the parts. It is ideal for systems with multiple interconnected components.
- **Key Characteristics**:
    - Each segment (or part) is treated as a rigid body, but joints introduce flexibility for independent movement.
    - Models constraints at joints, enabling realistic simulation of bending or articulation.
- **Example from Document**: Consider a robot with arms and legs that can move independently. Each limb is a separate rigid body connected by joints, mimicking human or robotic motion.
- **Applications**: Widely used for modeling the human body in sports science, rehabilitation, or animation (e.g., tracking joint movements during a dance), and for robotic arms in industrial automation.
- **Advantages over Rigid Body**: Captures the complexity of systems with multiple moving parts, providing a more accurate representation of natural or mechanical motion.
- **Limitations**: Computationally intensive due to the need to track multiple segments and joint constraints, especially in real-time applications.
---
## Dynamic Model
#### Definition
- In **dynamics**, focus on analyzing **how forces affect motion**.
- Dynamic models focus on the **relationship between forces, mass and acceleration**.
- This involves the application of Newton's second law of motion (Force = Mass x Acceleration) and Euler's rotation equations to describe how forces and torques result in translation and rotational motion, respectively.