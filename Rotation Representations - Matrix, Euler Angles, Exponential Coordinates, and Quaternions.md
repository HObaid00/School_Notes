# Rotation Representations: Matrix, Euler Angles, Exponential Coordinates, and Quaternions

There are several common ways to represent 3D rotations.

## Rotation Matrix

A rotation matrix $R \in SO(3)$ satisfies:

$$\Large
R^\top R=I,
\qquad
\det(R)=1
$$

Advantages:

- directly transforms vectors,
- easy to compose by multiplication.

Disadvantages:

- uses 9 numbers for only 3 degrees of freedom,
- must satisfy orthogonality constraints.

## Euler Angles

Euler angles use three sequential rotations around coordinate axes.

Example:

$$\Large
R = R_z(\psi)R_y(\theta)R_x(\phi)
$$

Advantages:

- intuitive,
- only 3 parameters.

Disadvantages:

- convention-dependent,
- has singularities such as gimbal lock.

## Exponential Coordinates

Exponential coordinates use the Lie algebra $\mathfrak{so}(3)$:

$$\Large
R = \exp(\hat{w})
$$

Advantages:

- directly connected to angular velocity,
- useful for optimization and differential geometry.

Disadvantages:

- not globally unique,
- logarithm can be numerically delicate near special cases.

## Unit Quaternions

A unit quaternion satisfies:

$$\Large
|q|=1
$$

Advantages:

- no gimbal lock,
- efficient composition,
- good interpolation behavior.

Disadvantages:

- uses 4 numbers for 3 degrees of freedom,
- $q$ and $-q$ represent the same rotation.

Summary:

| Representation | Parameters | Main Advantage | Main Problem |
|---|---:|---|---|
| Rotation matrix | 9 | Direct transformation | Constraints |
| Euler angles | 3 | Intuitive | Gimbal lock |
| Exponential coordinates | 3 | Lie theory / optimization | Non-unique |
| Unit quaternion | 4 | Smooth, no gimbal lock | Unit constraint |

---

## Links

[[3D Computer Vision]]