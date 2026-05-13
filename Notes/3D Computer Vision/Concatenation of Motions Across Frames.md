# Concatenation of Motions Across Frames

Suppose we have two time frames $t_1$ and $t_2$. The transformation from frame $t_1$ to frame $t_2$ is denoted:

$$\Large
g(t_2,t_1)
$$

It maps coordinates from frame $t_1$ into frame $t_2$:

$$\Large
X(t_2) = g(t_2,t_1)X(t_1)
$$

If we move from frame $t_1$ to $t_2$, and then from $t_2$ to $t_3$, the total transformation is:

$$\Large
X(t_3)
=
g(t_3,t_2)g(t_2,t_1)X(t_1)
$$

Therefore:

$$\Large
g(t_3,t_1)
=
g(t_3,t_2)g(t_2,t_1)
$$

This is called **composition** or **concatenation** of transformations.

The inverse transformation maps back:

$$\Large
g^{-1}(t_2,t_1) = g(t_1,t_2)
$$

because going from $t_1$ to $t_2$ and then back to $t_1$ should give the identity transformation:

$$\Large
g(t_1,t_2)g(t_2,t_1)=I
$$

Intuition:

Rigid-body transformations behave like coordinate-change operations. To combine multiple coordinate changes, multiply their matrices in the correct order.

---

## Links

[[3D Computer Vision]]