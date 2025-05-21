## What is Q-Learning?

Q-learning is a prominent model-free, value-based, off-policy reinforcement learning algorithm.

*   **Goal**: It aims to find the best series of actions an agent can take based on its current state.
*   **"Q"**: The "Q" in Q-learning stands for **Quality**. The Q-value, denoted $Q(s, a)$, represents the quality (or expected future reward) of taking action $a$ in state $s$ and then following the optimal policy thereafter.
*   **Off-Policy Nature**: Q-learning learns the optimal Q-values (and thus, the optimal policy) independently of the policy being followed to explore the environment.
![[Pasted image 20250521133325.png]]
## Q-Learning as Off-Policy TD Control

*   **Off-Policy Learning Definition**: In off-policy learning, we evaluate or improve a **target policy (π)** while the agent is following a different **behavior policy (μ)** to generate experience.
    *   Example: A robot learning by watching a video (behavior policy from video, target policy is what the robot learns) or an agent learning from experience gained by another agent.
*   **Policies in Q-Learning**:
    *   **Target Policy (π)**: In Q-learning, the target policy is typically a **greedy policy** with respect to the current Q-value estimates. It aims to learn the optimal Q-values, $Q*(s, a)$.
    *   **Behavior Policy (μ)**: The behavior policy is often an **epsilon-greedy (ε-greedy) policy**. This policy mostly chooses actions greedily based on current Q-values but occasionally (with probability ε) chooses a random action. This ensures sufficient **exploration** of the state-action space.

## The Q-Table

*   **Purpose**: The agent uses a **Q-table** to store and update the Q-values for all state-action pairs. This table helps the agent decide the best possible action to take from any given state by looking up the action with the highest Q-value for that state.
*   **Structure**: A Q-table is essentially a data structure (often a matrix or a dictionary) where rows might represent states and columns represent actions, and each cell $(s, a)$ stores the $Q(s, a)$ value.
*   **Update Mechanism**: The Q-learning algorithm is used to iteratively update the values in the Q-table based on experience.
1.  Initialize Q-Table
2.  Loop (for multiple iterations until a good Q-Table is ready):
    a.  Choose an Action (typically using the behavior policy, e.g., ε-greedy on the current Q-table)
    b.  Perform Action
    c.  Measure Reward (and observe next state)
    d.  Update Q-Table (using the Q-learning update rule))

## Q-Table Update Rule

The core of Q-learning is its update rule for $Q(S_t, A_t)$:
$$
Q(S_t, A_t) \leftarrow Q(S_t, A_t) + \alpha \left[ R_{t+1} + \gamma \max_a Q(S_{t+1}, a) - Q(S_t, A_t) \right]
$$
Where:
*   $Q(S_t, A_t)$: The current Q-value of taking action $A_t$ in state $S_t$.
*   $α$: Learning rate.
*   $R_{t+1}$: Reward received after taking action $A_t$ and transitioning from $S_t$ to $S_{t+1}$.
*   $γ$: Discount factor.
*   $max_a Q(S_{t+1}, a)$: The maximum Q-value for the next state $S_{t+1}$ over all possible actions $a$ from $S_{t+1}$. This term represents the optimal future value achievable from $S_{t+1}$ according to the current Q-table. This is the key part that makes Q-learning off-policy, as it considers the best next action regardless of what action the behavior policy might actually choose.

**Breakdown of the Update Rule Components:**
*   **New Q-value estimation**: The left side of the arrow.
*   **Former Q-value estimation**: The first $Q(S_t, A_t)$ on the right.
*   **Learning Rate**: $α$.
*   **Immediate Reward**: $R_{t+1}$.
*   **Discounted Estimate of optimal Q-value of next state**: $γ max_a Q(S_{t+1}, a)$.
*   **TD Target**: $R_{t+1} + γ max_a Q(S_{t+1}, a)$. This is what $Q(S_t, A_t)$ is trying to move towards.
*   **TD Error**: $[R_{t+1} + γ max_a Q(S_{t+1}, a) - Q(S_t, A_t)]$.

(Image context: Three cartoon robot illustrations are shown below the formula and its breakdown.)

## Q-Learning Algorithm Steps (Conceptual)

1.  **Temporal Difference (TD) Error Calculation**:
    *   $TD Error = R_{t+1} + γ * max_a Q(S_{t+1}, a) - Q(S_t, A_t)$
    *   This represents the difference between the estimated future reward (TD Target) and the current Q-value estimate for $(S_t, A_t)$.

2.  **Iterative Q-Value Update**:
    *   The Q-learning update equation is applied repeatedly for each experienced transition $(S_t, A_t, R_{t+1}, S_{t+1})$. It uses the previous episode's (or step's) estimated Q-values, the learning rate, and the calculated TD error.

3.  **Q-Table Convergence**:
    *   The process of updating Q-values is repeated many times (across many episodes or steps).
    *   Eventually, the Q-table converges, meaning the Q-values no longer change significantly with additional updates. At this point, they approximate the optimal action-value function $Q*$.

4.  **Q-Value Maximization (Policy Extraction)**:
    *   The goal is to maximize the Q-value function by finding the optimal action-value estimates for each state-action pair.
    *   The final (converged) Q-table represents the learned optimal policy. The agent can select the action with the highest Q-value in each state to maximize the expected future reward.
    *   $Optimal Action in state s = argmax_a Q(s, a)$

This iterative process of updating Q-values using the TD error is the core of the Q-learning algorithm, allowing the agent to learn the optimal policy through trial-and-error interactions with the environment.

## Q-Learning Update Diagram