# Nonlinear Classification with Basis Functions

Some datasets cannot be separated by a straight line.

---

# Example

Suppose one class forms a circle around another class.

No linear boundary can separate them.

---

# Key Idea

Transform the input into a new feature space:

$$\Large
\phi:\mathbb{R}^D \rightarrow \mathbb{R}^M
$$

Then perform linear classification in the transformed space.

---

# Example Transformation

Convert Cartesian coordinates into polar coordinates:

$$\Large
\phi(x)=(\theta,r) =
(\text{angle}(x), \|x\|_2 )
$$

where:

- $\theta$ = angle
- $r=\|x\|_2$

Transforms data to linearly separable space.

![[Pasted image 20260227224307.png]]


---

# Why This Helps

The transformed data may become linearly separable even if the original data is not.

---

# Important Insight

The classifier is linear in transformed features, even though the boundary is nonlinear in the original space.

---

# Limitations of Hard Decisions

- No uncertainty estimate  
- Poor handling of noise  
- Difficult optimization  
- Poor generalization  

![[Pasted image 20260227105923.png]]

---
# Links
[[Basis]]
[[Basis functions]]
[[Machine Learning]]