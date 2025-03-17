There are **two main types** of neighborhood-based collaborative filtering:

1. **User-Based Collaborative Filtering (UBCF)**
    
    - Identifies users with similar interests.
    - Recommends items based on what these similar users have liked.
    - Example: _Booking.com suggests destinations by analyzing travel history of similar users._
2. **Item-Based Collaborative Filtering (IBCF)**
    
    - Finds relationships between items based on user interactions.
    - Example: _Netflix’s "Because you watched..." feature recommends movies based on viewing history._

### **Strengths of Neighborhood-Based Methods**

- **Simple & Intuitive:** Easy to understand and implement.
- **Explainability:** Recommendations can be justified based on user similarity.
- **Scalability:** No need for extensive training like deep learning models.
- **Serendipity:** Can introduce novel items that users might not have considered.

### **Limitations**

- Struggles with **cold-start problems** (new users or new items with no prior data).
- **Scalability issues** in very large datasets.
- **Data sparsity** can lead to poor recommendations if there aren’t enough overlapping ratings.