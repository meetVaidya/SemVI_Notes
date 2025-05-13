### Macroaveraging

**Definition**:
- Macroaveraging computes the performance metrics (precision, recall, and F-measure) for each class independently and then takes the average of these metrics across all classes.

**Formulas**:
$$
\text{Macro Precision} = \frac{\sum_{i=1}^{n} \text{Precision}_i}{n}
$$
$$
\text{Macro Recall} = \frac{\sum_{i=1}^{n} \text{Recall}_i}{n}
$$
$$
\text{Macro F1} = \frac{\sum_{i=1}^{n} F1_i}{n}
$$

**Use Case**:
- Useful when you want to treat all classes equally, regardless of their size.

### Microaveraging

**Definition**:
- Microaveraging aggregates the contributions of all classes to compute the overall precision, recall, and F-measure. It sums up all the true positives, false positives, and false negatives across all classes and then computes the metrics.

**Formulas**:
$$
\text{Micro Precision} = \frac{\sum_{i=1}^{n} TP_i}{\sum_{i=1}^{n} (TP_i + FP_i)}
$$
$$
\text{Micro Recall} = \frac{\sum_{i=1}^{n} TP_i}{\sum_{i=1}^{n} (TP_i + FN_i)}
$$
$$
\text{Micro F1} = 2 \times \frac{\text{Micro Precision} \times \text{Micro Recall}}{\text{Micro Precision} + \text{Micro Recall}}
$$

**Use Case**:
- Useful when you want to give more weight to larger classes, as it considers the overall performance across all classes.

### Summary

- **Macroaveraging**: Treats all classes equally, useful for balanced datasets or when each class is of equal importance.
- **Microaveraging**: Considers the overall performance, useful for imbalanced datasets or when larger classes are more important.

### Multi-class Confusion Matrix (3-class)
![[Pasted image 20250513221312.png]]