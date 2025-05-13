### Example Scenario

Imagine you have a dataset of 1 million tweets, and you want to classify them into two categories:
- **Positive class**: Tweets about Delicious Pie Co.
- **Negative class**: All other tweets.

Out of these 1 million tweets:
- 100 tweets are about Delicious Pie Co. (Positive class).
- 999,900 tweets are about something else (Negative class).

### Accuracy

**Definition**: Accuracy is the proportion of correct predictions (both true positives and true negatives) among the total number of cases examined.

**Example**:
- If you build a "dumb" classifier that labels every tweet as "not about pie," it will correctly identify 999,900 tweets as not about pie (True Negatives) and incorrectly label 100 tweets as not about pie (False Negatives).

**Calculation**:
$$
\text{Accuracy} = \frac{\text{Number of correct predictions}}{\text{Total number of predictions}} = \frac{TP + TN}{TP + TN + FP + FN}
$$
$$
\text{Accuracy} = \frac{0 + 999,900}{0 + 999,900 + 0 + 100} = \frac{999,900}{1,000,000} = 0.9999 \text{ or } 99.99\%
$$

**Issue with Accuracy**:
- While the accuracy is very high (99.99%), this classifier is useless because it doesn't identify any of the tweets about Delicious Pie Co. This is why accuracy alone can be misleading, especially in imbalanced datasets.

### Precision

**Definition**: Precision is the proportion of positive identifications (predicted as positive) that were actually correct.

**Example**:
- Suppose your classifier predicts 150 tweets as about Delicious Pie Co. (Positive class), out of which 90 are actually about Delicious Pie Co. (True Positives) and 60 are not (False Positives).

**Calculation**:
$$
\text{Precision} = \frac{TP}{TP + FP}
$$
$$
\text{Precision} = \frac{90}{90 + 60} = \frac{90}{150} = 0.6 \text{ or } 60\%
$$

**Interpretation**:
- A precision of 60% means that 60% of the tweets predicted as about Delicious Pie Co. are actually about Delicious Pie Co.

### Recall

**Definition**: Recall is the proportion of actual positives that were identified correctly.

**Example**:
- Out of the 100 actual tweets about Delicious Pie Co., your classifier correctly identifies 90 (True Positives) and misses 10 (False Negatives).

**Calculation**:
$$
\text{Recall} = \frac{TP}{TP + FN}
$$
$$
\text{Recall} = \frac{90}{90 + 10} = \frac{90}{100} = 0.9 \text{ or } 90\%
$$

**Interpretation**:
- A recall of 90% means that 90% of the actual tweets about Delicious Pie Co. were correctly identified by the classifier.

### Summary

- **Accuracy**: Measures overall correctness but can be misleading in imbalanced datasets.
- **Precision**: Focuses on the accuracy of positive predictions.
- **Recall**: Focuses on the ability to find all positive cases.