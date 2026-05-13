# Linear Regression

Linear regression is one of the most fundamental machine learning algorithms.

Its goal is to predict a continuous value from input data.

Examples:

- house price prediction
- temperature forecasting
- sales estimation
- stock trend prediction

---

# Regression Problem

We are given:

$$\Large
D=\{(x_i,y_i)\}_{i=1}^{N}
$$

where:

- $x_i$ = input features
- $y_i$ = target value

The goal is to learn a function:

$$\Large
f(x)
$$

such that:

$$\Large
y_i \approx f(x_i)
$$

---

# Linear Model

The simplest model assumes a linear relationship:

$$\Large
f_w(x)
=
w_0+w_1x_1+w_2x_2+\dots+w_Dx_D
$$

or compactly:

$$\Large
f_w(x)=w^Tx
$$

where:

- $w$ = weight vector
- $w_0$ = bias term

---

# Interpretation of Weights

Each weight measures how strongly a feature influences the prediction.

Example:

$$
f(x)=2x+5
$$

means:

- increasing $x$ by 1 increases prediction by 2
- $5$ is the offset

---

# Main Idea

Linear regression tries to fit the "best line" through the data.

---
# Links
[[Machine Learning]]