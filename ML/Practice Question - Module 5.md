### What does the SARSA algorithm update rule look like? How is it different from Q-learning?
The **SARSA** algorithm update rule is as follows:

##### SARSA Update Rule

$$
Q(s, a) \leftarrow Q(s, a) + \alpha \left[r + \gamma Q(s', a') - Q(s, a)\right]
$$

where:

- **\( Q(s, a) \)**: Current estimate of the Q-value for taking action **\( a \)** in state **\( s \)**  
- **\( \alpha \)**: Learning rate  
- **\( r \)**: Reward received after taking action **\( a \)** in state **\( s \)**  
- **\( \gamma \)**: Discount factor  
- **\( Q(s', a') \)**: Estimate of the Q-value for taking action **\( a' \)** in the next state **\( s' \)**

---

##### Comparison with Q-Learning

**SARSA** and **Q-learning** are both **Temporal Difference (TD) control** methods, but they differ in how they select the next action:

- **Q-learning** uses a **greedy policy** to select the next action, meaning it chooses the action with the highest **Q-value**.
- **SARSA** uses the **same policy** to select both the current and next actions. This means that **SARSA** follows the policy it is learning.

##### Key Differences

- **On-policy (SARSA)**: Learns from the experiences gathered while following the same policy it is learning.
- **Off-policy (Q-learning)**: Learns from experiences gathered while following a different policy (usually an **ε-greedy** policy).

This difference in policy selection leads to distinct learning behaviors and convergence properties for **SARSA** and **Q-learning**.

---
### Why is SARSA considered an on-policy algorithm and what is an on policy algorithm?

**SARSA** is considered an **on-policy** algorithm because it learns from experiences gathered while following the same policy it is learning.

#### On-Policy Algorithm Definition

An **on-policy** algorithm is a type of reinforcement learning algorithm that:

1. **Learns from its own experiences**: The algorithm learns from the experiences it gathers while following its own policy.
2. **Updates policy based on gathered experiences**: The algorithm updates its policy based on the experiences it gathers.

In an **on-policy** algorithm, the policy used to select actions is the same policy that is being learned.

#### SARSA as On-Policy

**SARSA** is an **on-policy** algorithm because:

1. **Same policy for action selection and learning**: **SARSA** uses the same policy to select actions and learn from experiences.
2. **Learns from experiences gathered while following its policy**: **SARSA** updates its policy based on the experiences gathered while following its own policy.

---
### What is the significance of the action A′ in the SARSA update rule?
The action **A′** in the **SARSA** update rule represents the next action taken in the next state **S′**.
#### Role of A′

The action **A′** plays a crucial role in the **SARSA** update rule:

1. **Next Action**: **A′** is the next action taken in the next state **S′**, which is used to compute the **Q-value** of the next state.
2. **TD Error**: The **TD error** is computed using the **Q-value** of the next state and action **A′**, which helps to update the **Q-value** of the current state and action.

#### SARSA Update Rule

The **SARSA** update rule is as follows:

**SARSA Update Rule**: $Q(s, a) ← Q(s, a) + α [r + γQ(s', a') - Q(s, a)]$

The action **A′** is essential in computing the **TD error** and updating the **Q-value** in the **SARSA** algorithm.

#### On-Policy Nature

The use of **A′** in the **SARSA** update rule makes it an **on-policy** algorithm, as it learns from the experiences gathered while following the same policy it is learning.

---
### Illustrate the pseudocode for SARSA(λ) with the help of an example.
#### Pseudocode for SARSA(λ)

The **SARSA(λ)** algorithm combines **SARSA** with **eligibility traces** to improve learning efficiency.

#### Pseudocode:

1. **Initialize**:
 * **Q(s, a)**: Initialize all state-action pairs to 0.
 * **e(s, a)**: Initialize all eligibility traces to 0.

2. **For each episode**:
 * **Choose action a**: Select action a using the current policy (e.g., ε-greedy).
 * **Initialize eligibility traces**: e(s, a) = 1 for all (s, a).
3. **Take action a, observe r and s'**: Take action a, observe reward r and next state s'.

#### SARSA(λ) Update:

* **Update eligibility traces**: e(s, a) ← λγe(s, a) + 1 for all (s, a).
* **Update Q-values**: Q(s, a) ← Q(s, a) + α[r + γQ(s', a') - Q(s, a)]e(s, a) for all (s, a).

#### Example

Consider an **episodic task** where an agent moves on a grid and receives a reward only at the end.

* **SARSA(λ) with λ=0.9**:
 * The **eligibility traces** help propagate the reward backward through time, allowing the agent to learn more efficiently.

#### Pseudocode:

```python
def sarsa_lambda(alpha, lambda_, gamma, num_episodes):
 * Initialize Q, e
 * For each episode:
     * e = 0
     * For each step in episode:
         * Select action a
         * Take action a, observe r and s'
         * Update eligibility traces: e(s, a) = lambda_ * gamma * e(s, a) + 1
         * Update Q-values: Q(s, a) = Q(s, a) + alpha * [r + gamma * Q(s', a') - Q(s, a)] * e(s, a)
```
#### Example:

- The agent takes a swing (action) and misses the ball.
- The agent gets 0 reward immediately.
- The **eligibility trace** for the **action taken** increases.
- If the agent hits the ball into the hole in the next swing, the **single reward** (+100) is propagated backward through time, updating **Q-values** based on the **eligibility traces**.

---
### Apply the concept of Eligibility traces in Reinforcement Learning using Accumulating trace, Dutch trace and Replacing trace with the help of appropriate equations
#### Eligibility Traces in Reinforcement Learning

Eligibility traces are a crucial concept in Reinforcement Learning (RL) that help improve the efficiency and stability of learning.

#### Types of Eligibility Traces

There are three main types of eligibility traces:

1. **Accumulating Trace**  
2. **Replacing Trace**  
3. **Dutch Trace** (also known as **Decaying** or **Dutch** trace)

#### Accumulating Trace

- **Update Rule**:  
  $e_t(s, a) \leftarrow \gamma \lambda e_{t-1}(s, a) + 1$ for all $(s, a)$  
- Accumulating traces **accumulate the contributions** of all visited states and actions over time.

#### Replacing Trace

- **Update Rule**:  
  $$e_t(s, a) \leftarrow  
  \begin{cases}  
  1 & \text{if } (s, a) = (s_t, a_t) \\  
  \gamma \lambda e_{t-1}(s, a) & \text{otherwise}  
  \end{cases}$$  
- Replacing traces **replace the old trace values** with new ones.

#### Dutch Trace

- **Update Rule**:  
  $e_t(s, a) \leftarrow \gamma \lambda e_{t-1}(s, a) + \sigma_t(s, a)$  
- Dutch traces **combine accumulating and replacing** traces, offering a compromise between the two.

#### Q-Value Update with Eligibility Traces

The update rule for Q-values using eligibility traces is:

$$
Q(s, a) \leftarrow Q(s, a) + \alpha \left[r_t + \gamma \max_{a'} Q(s_{t+1}, a') - Q(s_t, a_t)\right] e_t(s, a)
$$

Where:

- $\alpha$: Learning rate  
- $r_t$: Reward at time $t$  
- $\gamma$: Discount factor  
- $\max_{a'} Q(s_{t+1}, a')$: Maximum Q-value at the next state  
- $e_t(s, a)$: Eligibility trace

#### Example

Consider a simple grid world with an agent moving on a grid:

- **Accumulating trace**: The agent’s eligibility trace **accumulates over time**, helping to propagate rewards backward more efficiently.
- **Replacing trace**: The agent’s eligibility trace **replaces older values**, focusing updates on **more recent** experiences.

---