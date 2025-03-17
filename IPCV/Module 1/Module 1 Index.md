- **Introduction & Overview**
    
    - Image Processing and Computer Vision – II module
    - Focus on Camera Geometry Model
- **Camera Fundamentals**
    
    - **Real Aperture Camera Basics**
        - Definition and role of the aperture
        - Relationship between aperture size, f-stop, and light intake
        - Impact on brightness, depth of field, and bokeh effect
    - **Focal Length**
        - Definition of focal length
        - Effects of shorter vs. longer focal lengths on the field of view
        - Calculation of aperture diameter using focal length and f-stop
- **Interaction of Light in Photography**
    
    - How light from the source interacts with the subject and camera sensor
    - Effects of light angle and intensity on image exposure and quality
- **Lens as a Linear Shift-Invariant (LSI) System**
    
    - **Linearity Properties**
        - Superposition: Combining light outputs from multiple sources
        - Scaling: Proportional response to changes in input brightness or object size
    - **Shift Invariance**
        - Consistent behavior regardless of object position
- **Geometric and Projective Transformations**
    
    - **Projective Geometry**
        - Mapping from 3D to 2D via projection
        - Invariant properties under projection (e.g., parallelism in 3D vs. convergence in 2D)
    - **2D Transformations**
        - Translation, scaling, rotation, shearing, and reflection
    - **3D Transformations**
        - Translation, scaling, rotation (about x-, y-, and z-axes), shearing, and reflection
- **Perspective Projection**
    
    - **Full Perspective Projection**
        - Uses actual depth information (z-coordinate) for realistic scaling
    - **Weak Perspective Projection**
        - Simplified approach assuming average depth for all points
    - **Perspective Types**
        - One-point, two-point, and three-point perspective projections
- **Homography**
    
    - **Concept and Definition**
        - Mapping points between two planes using a 3×3 transformation matrix
    - **Applications**
        - Correcting perspective distortion in document scanning and image stitching
    - **Planar Homography**
        - Specific to flat surfaces and transforming images to a top-down view
- **Pinhole Camera Model**
    
    - Explanation of the pinhole camera
    - How image inversion occurs due to straight-line propagation of light
- **Camera Parameters and Calibration**
    
    - **Intrinsic Parameters**
        - Focal length, principal point, skew coefficient, and distortion coefficients
    - **Extrinsic Parameters**
        - Camera’s rotation matrix and translation vector (position and orientation)
    - **Camera Calibration Process**
        - Capturing images, detecting corners, estimating parameters, and undistorting images
- **Coordinate Systems**
    
    - Cartesian coordinates
    - Spherical coordinates
    - Homogeneous coordinate system for representing projective transformations
- **Detailed 3D Transformations & Operations**
    
    - **Rotation**
        - Rotations about the x-, y-, and z-axes (with the right-hand rule)
    - **Translation & Scaling**
        - Applying transformations to 3D points and objects
    - **Reflection and Shear Transformations**
        - Reflecting points about axes and applying shear in the x-y plane
- **Perspective Distortion and Projections**
    
    - **Types of Perspective Distortion**
        - Wide-Angle (Barrel) Distortion and Telephoto (Compression) Distortion
    - **Orthographic Projection**
        - Parallel projection without perspective distortion, used in technical drawing and 2D game design
- **Practical Applications and Exercises**
    
    - Real-time video stitching techniques
    - Face detection and recognition: differences between detection and identification
    - Sample exercises involving transformation questions on specific 3D points and objects

This detailed bullet list encapsulates the key topics and concepts discussed in the PDF.