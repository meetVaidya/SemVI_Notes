### 1. User Preference

*   A user study can be conducted to select the best algorithm by allowing participants to choose their preferred system. This makes decision-making straightforward through majority votes.
*   **Important Note:** Not all users should have equal influence in decision-making.
    *   **Example:** Frequent buyers' opinions might be more valuable than those of occasional buyers.  This allows for weighting user feedback based on their engagement level.

### 2. Prediction Accuracy

This section focuses on evaluating how well the recommender system predicts user behaviour.

1.  **Measuring Ratings Prediction Accuracy**

    *   **Goal:** To predict the rating a user would give to an item.  The accuracy of the system's predicted rating is then measured.
    *   **Metrics:**
        *   **Root Mean Square Error (RMSE):**  Measures the average magnitude of the error between predicted and actual ratings.
            $$\text{RMSE} = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2}$$

            Where:
            *   `n` is the number of ratings.
            *   `yᵢ` is the actual rating.
            *   `ŷᵢ` is the predicted rating.

        *   **Mean Absolute Error (MAE):** Measures the average absolute difference between predicted and actual ratings.
            $$\text{MAE} = \frac{1}{n} \sum_{i=1}^{n} |y_i - \hat{y}_i|$$
            Where:
            *   `n` is the number of ratings.
            *   `yᵢ` is the actual rating.
            *   `ŷᵢ` is the predicted rating.

2.  **Measuring Usage Prediction**

    *   **Goal:** The recommender system (RS) does not predict users' preferences (e.g., movie ratings) but instead recommends items that users may *use* (e.g., watch, purchase).
    *   **Offline Evaluation Assumption:** Data is typically collected *without* the recommender system under evaluation. It is assumed that unused items would not have been used even if they had been recommended.
    *   **Example:** If a movie was not watched by the user, it is assumed that the user would not have watched it regardless of whether it was recommended or not.  This is a crucial, and potentially limiting, assumption in offline evaluation.

### 3. Ranking Measures

This section focuses on evaluating the quality of the ranked list of recommendations.

*   Recommender systems typically present recommendations as a vertical or horizontal list, ordering items according to predicted user preferences.
*   **Approaches to Measure Ranking Accuracy:**

    1.  **Using a Reference Ranking:**
        *   Requires explicit user ratings of items.
        *   Rated items are ranked in decreasing order of rating to create a "ground truth" ranking.
    2.  **Utility-Based Ranking:**
        *   Assumes the utility of a list of recommendations is additive, given by the sum of the utility of each item in the list.
        *   The utility of an item reflects its value or relevance to the user.
    3.  **Online Evaluation of Ranking:**
        *   Analyzes the interactions of users with the *live* recommender system.
        *   Examples of interactions include: click-through rates (CTR), conversion rates, time spent viewing recommendations, and purchase rates.  This provides real-world feedback on the effectiveness of the ranking.
### 4. Coverage
- Provide recommendations with high quality but only for a small portion of the items where they have huge amounts of data.
	1. **Item Space Coverage** : The proportion of items that the RS can recommend.
	2. **User Space Coverage** : Proportion of users or user interaction for which the system can recommend items.

### 5. Confidence
- Defined as the systems trust in its recommendations or prediction

### 6. Trust
- Refers to the user's trust in the recommendation provided by the system.

### 7. Novelty
-  Recommendation of item that user did not know about.

### 8. Serendipity
- Surprises users with unexpected but delightful recommendations, enhancing their experience.