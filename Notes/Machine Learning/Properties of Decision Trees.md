Advantages:

- Easy to interpret  
- Handle categorical and numerical data  
- No feature scaling required  
- Nonlinear decision boundaries  

Disadvantages:

- High variance  
- Prone to overfitting  
- Unstable (small data changes → different tree)  

---

# Axis-Aligned Splits

Standard trees create splits of form:

$$\Large
x_j \le t
$$

This creates axis-aligned partitions.

*(Copy figure showing rectangular regions on slide.)*

---

# Limitations

- Cannot easily model oblique boundaries  
- Greedy training may not find optimal tree  
- Performance often worse than ensemble methods  

---

# Computational Complexity

Training:

- For each node: evaluate many candidate splits  
- Roughly $\Large O(N D \log N)$ for balanced trees  

Prediction:

- $\Large O(\text{depth})$

---
# Links
[[Machine Learning]]
