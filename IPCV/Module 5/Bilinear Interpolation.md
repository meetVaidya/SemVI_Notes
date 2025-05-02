#### Definition
- Bilinear Interpolation is a method to compute an unknown value at a point within a gird by interpolation the values of the four nearest corner points of a rectangular grid.
- It ensures smoother transitions compared to nearest-neighbour interpolation by averaging the contributions of neighbouring pixels, thus preserving finer details in resized or transformed images.

#### Applications in Image Processing
- **Image Resizing**: As highlighted in the document, Bilinear Interpolation is used to estimate pixel values when scaling images to different resolutions, ensuring smoother results compared to simpler methods.
- **Object Segmentation**: In deep learning architectures for segmentation (e.g., U-Net, PSPNet), Bilinear Interpolation is often employed during upsampling to restore feature maps to the original image size while retaining spatial details.

#### Advantages and Limitations

- **Advantages**:
    
    - Produces smoother transitions between pixel values compared to nearest-neighbor interpolation.
        
    - Computationally efficient for small grids or localized estimations.
        
- **Limitations**:
    
    - May not preserve sharp edges or high-frequency details as effectively as more advanced methods (e.g., Bicubic Interpolation).
        
    - Assumes linear variation between points, which may not always reflect real image characteristics.