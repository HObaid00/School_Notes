# Structure and Motion / Visual SLAM

**Structure and Motion** is the joint problem of estimating:

1. the **3D structure** of the scene, and
2. the **motion** of the camera.

The same idea is often called **visual SLAM**, which stands for:

$$\Large
\text{Simultaneous Localization and Mapping}
$$

In visual SLAM:

- **Localization** means estimating where the camera is.
- **Mapping** means estimating the 3D geometry of the environment.

For example, a robot moving through a room must estimate its own pose while also building a map of walls, objects, and landmarks. The camera images alone are not enough unless the algorithm uses geometric constraints between multiple views.

A basic relation is:

$$\Large
\text{camera motion} + \text{image correspondences}
\Rightarrow
\text{3D scene structure}
$$

Important historical results:

- Kruppa showed that two views of five points are sufficient to determine relative motion and point structure up to finitely many solutions.
- Longuet-Higgins proposed a linear method based on the epipolar constraint.
- Tomasi and Kanade developed factorization methods for multiple views under orthographic projection.

The key idea is that camera motion and scene structure are coupled: to know where points are in 3D, we need to know how the camera moved; to know how the camera moved, we use how points appear to move in the images.

---

## Links

[[3D Computer Vision]]

