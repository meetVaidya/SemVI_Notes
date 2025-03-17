Great! Now, let's move on to the next topic:

---

# **User-Based Rating Prediction**

## **What is User-Based Collaborative Filtering (UBCF)?**

User-Based Collaborative Filtering (UBCF) is a method for predicting how much a user will like an item based on ratings given by other users with **similar preferences**.

- The main assumption:
    - Users who **rated items similarly in the past** will likely have **similar tastes** in the future.
- This method finds a group of **similar users** (neighbors) and predicts the missing ratings using their ratings.

## **Steps in User-Based Rating Prediction**

### **Step 1: Finding Similarity Between Users**

To make predictions, we first compute how similar other users are to the target user. The similarity between two users aa and bb can be calculated using **different similarity measures**:

#### **1. Pearson Correlation Coefficient (PCC)**

- Measures the **linear relationship** between two users’ ratings.
- Adjusts for users who rate items on different scales.
- Formula:

sim(a,b)=∑(ra,i−rˉa)(rb,i−rˉb)∑(ra,i−rˉa)2∑(rb,i−rˉb)2\text{sim}(a, b) = \frac{\sum (r_{a,i} - \bar{r}_a)(r_{b,i} - \bar{r}_b)}{\sqrt{\sum (r_{a,i} - \bar{r}_a)^2} \sqrt{\sum (r_{b,i} - \bar{r}_b)^2}}

where:

- ra,ir_{a,i} and rb,ir_{b,i} are ratings given by users aa and bb to item ii.
- rˉa\bar{r}_a and rˉb\bar{r}_b are the average ratings of users aa and bb.

#### **2. Cosine Similarity**

- Treats user rating vectors as points in multi-dimensional space and computes the cosine of the angle between them.
- Formula:

sim(a,b)=∑ra,i⋅rb,i∑ra,i2⋅∑rb,i2\text{sim}(a, b) = \frac{\sum r_{a,i} \cdot r_{b,i}}{\sqrt{\sum r_{a,i}^2} \cdot \sqrt{\sum r_{b,i}^2}}

- **Limitation**: Does not account for differences in user rating scales.

---

### **Step 2: Predicting the Missing Rating**

Once we have identified similar users, we estimate the missing rating using a **weighted average approach**, giving more importance to similar users.

#### **Basic Weighted Average Formula**

r^u,i=rˉu+∑sim(u,v)(rv,i−rˉv)∑∣sim(u,v)∣\hat{r}_{u,i} = \bar{r}_u + \frac{\sum \text{sim}(u, v) (r_{v,i} - \bar{r}_v)}{\sum |\text{sim}(u, v)|}

where:

- r^u,i\hat{r}_{u,i} is the predicted rating for user uu on item ii.
- rˉu\bar{r}_u is the average rating of user uu.
- rv,ir_{v,i} is the rating of a similar user vv for item ii.
- sim(u,v)\text{sim}(u, v) is the similarity between user uu and user vv.

#### **Example Calculation**

Consider the following rating matrix for a **news app recommendation system**:

|User|App1|App2|App3|App4|App5|
|---|---|---|---|---|---|
|Alice|5|3|?|2|1|
|U1|4|3|4|1|2|
|U2|5|2|3|2|1|
|U3|3|4|5|1|?|

- **Objective**: Predict Alice's rating for App3 (?).
- **Steps**:
    1. Compute similarity between Alice and each other user (U1, U2, U3).
    2. Use the weighted average formula to estimate the missing rating.

---

### **Challenges in User-Based Prediction**

1. **Cold-Start Problem**:
    
    - New users have no prior ratings, making it difficult to find similar users.
    - Solution: Hybrid methods (combine user-based and content-based filtering).
2. **Data Sparsity**:
    
    - Many users may not have rated the same items.
    - Solution: Use **item-based** filtering or **dimensionality reduction**.
3. **Scalability Issues**:
    
    - Finding similar users becomes computationally expensive with large datasets.
    - Solution: Use **pre-filtering** techniques to store only top neighbors.

---

### **Summary Table**

|**Step**|**Description**|
|---|---|
|**1. Find Similarity**|Compute similarity scores between users (e.g., Pearson, Cosine)|
|**2. Predict Missing Rating**|Use weighted average of neighbors’ ratings|
|**3. Handle Challenges**|Address cold-start, sparsity, and scalability issues|

---

This concludes **User-Based Rating Prediction**. Let me know when you're ready for the next topic, **Item-Based Recommendation**!