
## Confusion Matrix

|               | Predicted 1 | Predicted 0 |
|---------------|------------|------------|
| True 1        | TP         | FN         |
| True 0        | FP         | TN         |

- TP = true positive  
- TN = true negative  
- FP = false positive  
- FN = false negative  

![[Pasted image 20260226172059.png]]

---

## Metrics

Accuracy:

$$\Large
\text{acc} = \frac{TP + TN}{TP + TN + FP + FN}
$$

Precision:

$$\Large
\text{prec} = \frac{TP}{TP + FP}
$$

Recall (Sensitivity):

$$\Large
\text{rec} = \frac{TP}{TP + FN}
$$

Specificity:

$$\Large
\text{tnr} = \frac{TN}{FP + TN}
$$

False Negative Rate:

$$\Large
\text{fnr} = \frac{FN}{TP + FN}
$$

False Positive Rate:

$$\Large
\text{fpr} = \frac{FP}{FP + TN}
$$

F1 Score:

$$\Large
\text{f1} =
\frac{2 \cdot \text{prec} \cdot \text{rec}}
{\text{prec} + \text{rec}}
$$

Note:

- Trade-off between precision and recall  
- Be careful with imbalanced classes  

---

# Links
[[Machine Learning]]
