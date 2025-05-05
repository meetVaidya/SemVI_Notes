## Time-aware factor model
- Time-aware factor models in recommender systems acknowledge that user preferences and **item popularity evolve over time**, improving recommendations by incorporating **temporal data** and using techniques like **recency-based weighting** or **time-decayed factors**.

#### Time-Aware Factor Model Approaches:
- Recency-Based Models:
	- Window-Based
	- Decay-Based
- Time-Decay Factors
- Periodic Context-Based Models
- Explicit Time as an Independent Variable

## Echo Chambers
- An echo chambers occurs when users are **repeatedly recommended similar content based on their past preferences**, reinforcing their existing opinions and **limiting exposure to diverse options**.
- **Causes in CFRS**:
	- Over-reliance on past interaction: Recommendations are based on prior user behaviour, leading to a self-reinforcing feedback loop.
	- Popularity Bias: Frequently recommended items become even more popular, overshadowing diverse or niche content.
	- Lack of novelty: Users rarely get exposed to new or unexpected items outside their established interests.

## Data Drift
- Data drift occurs when the **statistical properties of user-item interactions change over time**, causing the model to generate sub-optimal recommendations.
- **Causes in CFRS**
	- User behaviour shifts: users' preferences change due to trends , external events or personal evaluation.
	- Item popularity fluctuations: A once-popular item may lose relevance over time.
	- Seasonal variations: Certain items may be popular only during specific times.

## Concept Drift
- Concept drift refers to **changes in the underlying relationships between users and items**, making previous patterns obsolete.
- **Causes in CFRS**:
	- Evolving user interests: Users may develop new preferences that were not evident in past interactions.
	- Emerging constant trends: New categories or genres of content may gain traction
	- Cultural and societal shifts: Broader social changes can influence user preferences.