# Perceptron

The perceptron is one of the earliest binary classification algorithms.

It predicts classes using a hard threshold.

---

# Decision Rule

The perceptron predicts:

$$\Large
\hat{y}=f(w^Tx+w_0)
$$

where:

$$\Large
f(t)=
\begin{cases}
1 & t>0\\
0 & \text{otherwise}
\end{cases}
$$

---

# Intuition

The classifier computes a score:

$$\Large
w^Tx+w_0
$$

and assigns:

- class 1 if positive
- class 0 otherwise

---

# Perceptron Learning Rule

Initialize:

$$\Large
w=0
$$

For every misclassified sample:

$$\Large
w \leftarrow
\begin{cases}
w+x_i & y_i=1\\
w-x_i & y_i=0
\end{cases}
$$

Converges in finite steps if linearly separable.
![[Pasted image 20260227110151.png|629]]


---

# Why This Works

The update shifts the decision boundary toward correctly classifying the sample.

---

# Important Property

If the data is linearly separable, the perceptron converges in a finite number of steps.

---
# Links
[[Machine Learning]]