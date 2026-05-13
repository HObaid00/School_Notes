# Multiclass Classification

Real-world problems often involve more than two classes.

Example:

- handwritten digits
- object recognition
- language classification

---

# One-vs-Rest

Train one classifier per class:

$$
\Large
\text{class } c \quad \text{vs all others}
$$

Prediction:

- choose classifier with strongest response

![[Pasted image 20260227105657.png]] 

---

# One-vs-One

Train classifiers for every pair of classes.

For $C$ classes:

$$
\Large
\frac{C(C-1)}{2}
$$

binary classifiers are needed.

Prediction uses majority voting.

![[Pasted image 20260227105719.png]]

---

# Multiclass Discriminant

Define one linear function per class:

$$\Large
f_c(x)=w_c^Tx+w_{0c}
$$

Predict:

$$\Large
\hat{y}
=
\arg\max_{c} f_c(x)
$$

![[Pasted image 20260227105746.png]]


---

# Geometric Interpretation

Each class owns a region in feature space.

Decision boundaries form intersections of hyperplanes.

---
# Links
[[Machine Learning]]