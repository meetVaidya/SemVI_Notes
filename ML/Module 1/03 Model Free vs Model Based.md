### Model-Based RL:
- **Learns a model** of the environment: predicts **next state** and **reward** given a state and action.
- Uses the model for **planning** (e.g., **value iteration**, **Monte Carlo Tree Search**).
- Pros: **Sample efficient**, good for **simulated planning**.
- Cons: Model can be **inaccurate**, leading to poor decisions.

> Think of it like learning to drive by **simulating traffic scenarios** in your head before trying them.

### Model-Free RL:

- **Directly learns the policy** or **value function** from interaction.
- Doesn’t learn or use a model of the environment.
- Example algorithms:
    - **Policy-based**: **REINFORCE**, **PPO**
    - **Value-based**: **Q-learning**, **DQN**
- Pros: Simpler, less prone to **model errors**.
- Cons: Needs **more data**, can be **sample inefficient**.

> Think of it like learning to drive by **trial and error** on the road.

### Summary:

| Feature           | Model-Based RL          | Model-Free RL |
| ----------------- | ----------------------- | ------------- |
| Learns model?     | ✅ (transition + reward) | ❌             |
| Planning          | ✅                       | ❌             |
| Sample Efficiency | High                    | Low           |