## Binary Text Classification Example

Let's consider a "Delicious Pie Company" that wants to build a tweet detector to find tweets about their pies.
*   **Positive Class:** Tweets about Delicious Pie Co.
*   **Negative Class:** All other tweets.

## The 2-by-2 Confusion Matrix

A confusion matrix is a table that summarizes the performance of a classification model. For a binary classification task, it looks like this:

|                       | **Predicted: Positive** | **Predicted: Negative** |
| :-------------------- | :---------------------- | :---------------------- |
| **Actual: Positive**  | True Positive (TP)      | False Negative (FN)     |
| **Actual: Negative**  | False Positive (FP)     | True Negative (TN)      |

*   **True Positives (TP):** Items correctly classified as positive.
*   **True Negatives (TN):** Items correctly classified as negative.
*   **False Positives (FP):** Items incorrectly classified as positive (Type I error).
*   **False Negatives (FN):** Items incorrectly classified as negative (Type II error).

## Evaluation: Accuracy

**Accuracy** is the proportion of correct predictions among the total number of cases evaluated.

`Accuracy = (Number of correct predictions) / (Total number of predictions)`
`Accuracy = (TP + TN) / (TP + TN + FP + FN)`

### Why Accuracy Can Be Misleading

Consider a scenario with 1 million tweets:
*   100 tweets are about Delicious Pie Co. (Positive)
*   999,900 tweets are about something else (Negative)

If we build a "dumb" classifier that labels *every* tweet as "not about pie" (Negative):
*   TP = 0
*   FN = 100
*   FP = 0
*   TN = 999,900
*   Accuracy = (0 + 999,900) / (0 + 100 + 0 + 999,900) = 999,900 / 1,000,000 = 99.99%

This classifier has 99.99% accuracy but is useless because it doesn't find any of the positive instances we are looking for. This is common in **imbalanced datasets** where one class is much more frequent than the other.

That's why we often use **Precision** and **Recall** instead, especially when the positive class is rare or more important.

## Evaluation: Precision

**Precision** measures the proportion of items the system detected as positive that are *in fact* positive. It answers: "Of all items the classifier labeled as positive, how many were actually positive?"

`Precision (P) = TP / (TP + FP)`

*   High precision means that when the classifier predicts positive, it is very likely correct.
*   It focuses on the "purity" of the positive predictions.

## Evaluation: Recall (Sensitivity)

**Recall** (also known as sensitivity or true positive rate) measures the proportion of items *actually present* in the input that were correctly identified by the system. It answers: "Of all the actual positive items, how many did the classifier correctly identify?"

`Recall (R) = TP / (TP + FN)`

*   High recall means that the classifier finds most of the actual positive items.
*   It focuses on the "completeness" of the positive predictions.

### Why Precision and Recall?

Revisiting the "dumb pie-classifier" that labels nothing as "about pie":
*   TP = 0, FP = 0, FN = 100
*   Precision = 0 / (0 + 0) = Undefined (or 0 if FP=0 implies no positive predictions)
*   Recall = 0 / (0 + 100) = 0

Precision and Recall, unlike accuracy in imbalanced scenarios, emphasize **true positives**: finding the things we are supposed to be looking for.

## A Combined Measure: F-measure

F-measure (or F-score) is a single number that combines Precision (P) and Recall (R). It is the harmonic mean of precision and recall.

The general formula for F-measure is:
`F_β = (1 + β²) * (P * R) / (β² * P + R)`

We almost always use the **balanced F1-score** (where β = 1), which gives equal weight to precision and recall:
`F1 = 2 * (P * R) / (P + R)`

*   F1-score is high if both precision and recall are high.
*   It's a good single metric if you want a balance between P and R.

## Development Test Sets ("Devsets") and Cross-Validation

To develop and evaluate machine learning models robustly:

*   **Data Splitting:**
    *   **Training Set:** Used to train the model (learn parameters).
    *   **Development Test Set (Devset) / Validation Set:** Used to tune hyperparameters and make model choices.
    *   **Test Set (Held-out Set):** Used for final evaluation of the model's performance. Reported results should be on this set.

*   **Process:** Train on the training set, tune on the devset, report final performance on the test set.
    *   This avoids **overfitting** to the test set (i.e., ‘tuning to the test set’).
    *   Provides a more conservative and realistic estimate of performance on unseen data.
*   **Paradox:** We want as much data as possible for training and also enough for a reliable devset. How to split? Common splits are 60/20/20 or 80/10/10 (Train/Dev/Test).

### Cross-Validation

When data is limited, cross-validation provides a more robust estimate of model performance, especially for the devset.
*   **k-Fold Cross-Validation:**
    1.  Split the training data into `k` equal (or nearly equal) folds.
    2.  For each fold `i` from 1 to `k`:
        *   Train the model on `k-1` folds (all folds except fold `i`).
        *   Evaluate the model on fold `i` (which acts as a temporary devset).
    3.  Pool the results (e.g., average the performance metrics) over all `k` folds to get a pooled dev performance.
*   This gives a better estimate of how the model will perform on unseen data.

## Evaluation with More Than Two Classes

When dealing with multi-class classification (more than two classes), precision, recall, and F1-score can be calculated in a few ways.
![[Pasted image 20250518123705.png]]
### How to Combine P/R from Multiple Classes to Get One Metric

1.  **Macro-averaging:**
    *   Compute the performance metric (e.g., Precision, Recall, F1) for each class independently (treating each class as a one-vs-rest binary problem).
    *   Then, average these per-class metrics over all classes.
    *   Gives equal weight to each class, regardless of its size.

2.  **Micro-averaging:**
    *   Collect decisions (TP, FP, TN, FN) for all classes into one global confusion matrix (or sum up the individual TP, FP, FN counts from each class's one-vs-rest perspective).
    *   Compute precision, recall, and F1 from these aggregated counts.
    *   Gives equal weight to each instance/decision, thus favoring larger classes. In multi-class settings where each instance belongs to exactly one class, micro-averaged precision, recall, and F1-score are all equal to accuracy.

#### Solving the above example given in the image

| Class            | TP  | FP  | FN  | Precision              | Recall               |
| ---------------- | --- | --- | --- | ---------------------- | -------------------- |
| **No‑ball**      | 8   | 25  | 7   | 8 / (8+25) ≈ 0.242     | 8 / (8+7) ≈ 0.533    |
| **Wide‑ball**    | 10  | 12  | 10  | 10 / (10+12) ≈ 0.455   | 10 / (10+10) = 0.5   |
| **Regular ball** | 270 | 10  | 30  | 270 / (270+10) ≈ 0.964 | 270 / (270+30) = 0.9 |

- **Micro‑averaging** pools all decisions: $$\text{micro‑precision} = \frac{\sum_i \text{TP}_i}{\sum_i (\text{TP}_i + \text{FP}_i)} \;=\; \frac{8+10+270}{335} \approx0.860$$    
    and because total positives = total actual,  
    $$\text{micro‑recall}=\text{micro‑precision}\approx0.860$$
- **Macro‑averaging** just averages the per‑class scores:
    $$\text{macro‑precision} = \frac{0.242 + 0.455 + 0.964}{3} \approx0.554$$
    $$\text{macro‑recall} = \frac{0.533 + 0.5 + 0.9 }{3} \approx0.644$$

**Summary**
- Micro‑precision = Micro‑recall ≈ 0.860
- Macro‑precision ≈ 0.554
- Macro‑recall ≈ 0.644