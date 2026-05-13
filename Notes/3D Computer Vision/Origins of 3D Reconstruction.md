# The Origins of 3D Reconstruction

3D reconstruction is the problem of recovering the three-dimensional structure of the world from one or more two-dimensional images.

The central difficulty is that a 2D image loses depth information. A single image point can correspond to infinitely many possible 3D points along a ray going out from the camera. Because of this, 3D reconstruction is an **ill-posed problem**: the observations alone usually do not determine a unique 3D solution.

To make reconstruction possible, computer vision uses additional assumptions, such as:

- the scene is rigid,
- the camera motion is smooth,
- corresponding image points are known,
- multiple images are available,
- camera calibration is known or estimated.

Mathematically, 3D reconstruction is based on two important transformations:

1. **Rigid-body motion**, which describes how the camera moves from one frame to another.
2. **Perspective projection**, which describes how 3D points are mapped onto a 2D image plane.

A 3D point $X$ in the world is transformed by the camera motion and then projected into the image. In simplified form:

$$\Large
\text{3D world point} \rightarrow \text{camera coordinates} \rightarrow \text{2D image point}
$$

Historically, the study of perspective projection goes back to ancient Greek geometry and Renaissance art. It later became part of **projective geometry**, which studies properties preserved under projection.

In modern computer vision, reconstructing both the camera motion and the 3D scene is called **Structure and Motion** or **visual SLAM**.

---

## Links

[[3D Computer Vision]]