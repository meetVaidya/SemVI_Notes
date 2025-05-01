### What are the main steps involved in Policy Iteration and how do they differ from Value Iteration?
Policy Iteration involves a cycle of two main steps:

#### 1. Policy Evaluation (E)

- Start with an initial (often random) state-value function.
- Iteratively update the value of each state using the **Bellman equation** for the current policy:
  $$
  V(s) \leftarrow \sum_{a} \pi(a|s) \sum_{s', r} P(s', r | s, a) \left[ r + \gamma V(s') \right]
  $$
- Repeat until the value function converges (**Iterative Policy Evaluation**).

#### 2. Policy Improvement (I)

- Use the current value function to improve the policy:
  $$
  \pi'(s) = \arg\max_{a} \sum_{s', r} P(s', r | s, a) \left[ r + \gamma V(s') \right]
  $$
- Repeat steps E and I until the policy stops changing (converges).

### Value Iteration

- Value Iteration is a **special case of Policy Iteration**.
- It **skips full convergence** of the policy evaluation step.
- Instead, it performs a single update (one sweep) per iteration using a **modified Bellman update**:
  $$
  V(s) \leftarrow \max_{a} \sum_{s', r} P(s', r | s, a) \left[ r + \gamma V(s') \right]
  $$
- This merges policy evaluation and policy improvement into one step.
- Iterations continue until the value function changes are below a small threshold.

### Key Differences

#### Evaluation Step

- **Policy Iteration**:  
  - Performs **full policy evaluation** until convergence before improving the policy.
- **Value Iteration**:  
  - Performs **only one sweep** per iteration and immediately updates the value using the max operator over actions.

#### Efficiency and Speed

- **Policy Iteration**: Slower due to full policy evaluation, but may converge in fewer overall iterations.
- **Value Iteration**: Faster updates, but may require more iterations to converge.
---
### Which method converges faster: Policy Iteration or Value Iteration, and under what conditions?
The convergence speed of **Policy Iteration** and **Value Iteration** depends on the specific problem and the properties of the Markov Decision Process (MDP).

#### Policy Iteration

- **Guaranteed Convergence**:  
  Policy Iteration is guaranteed to converge to the **optimal policy** in a **finite number of iterations**.

- **Convergence Speed**:  
  The speed depends on:
  - The number of **iterations** required for policy evaluation.
  - The time it takes for the policy to **stabilize** during improvement steps.

#### Value Iteration

- **Faster Convergence**:  
  Value Iteration typically converges faster than Policy Iteration, particularly in problems with a **large number of states**.

- **Conditions for Faster Convergence**:
  - The MDP has a **large state space**.
  - The discount factor $ \gamma $ is **small**.
  - The reward structure is **sparse** (rewards occur infrequently).

#### Comparison Summary

| Feature            | Policy Iteration                        | Value Iteration                          |
|--------------------|------------------------------------------|-------------------------------------------|
| Evaluation         | Full policy evaluation                  | One sweep (partial evaluation)           |
| Improvement        | After evaluation converges              | At every step (via max operator)         |
| Speed              | Slower in large MDPs                    | Often faster for large state spaces      |
| Convergence Type   | Finite number of iterations (guaranteed)| Iterative until value changes are small  |

- **Policy Iteration**:  
  Slower due to **full evaluation** before improvement.

- **Value Iteration**:  
  Faster by **merging evaluation and improvement** into one step.
---
### In which scenario might you prefer using Value Iteration over Policy Iteration in dynamic programming?
#### When to Prefer Value Iteration

1. **Large State Space**  
   - When the MDP has a **large number of states**, full policy evaluation in Policy Iteration becomes computationally expensive.
2. **Need for Fast Convergence**  
   - Value Iteration often provides **faster convergence**, especially in high-dimensional environments.

#### Advantages of Value Iteration

- **Faster Convergence**  
  Value Iteration typically converges more quickly than Policy Iteration in practice, especially when $|S|$ is large.

- **Simultaneous Updates**  
  Value Iteration updates the value of all states in each iteration, combining both evaluation and improvement in one step:
  $$
  V(s) \leftarrow \max_a \sum_{s', r} P(s', r | s, a) \left[ r + \gamma V(s') \right]
  $$

- **Less Computational Overhead**  
  No need to wait for full convergence of policy evaluation before improving the policy.

#### Example Scenario

In a **large-scale MDP** with:

- **Sparse rewards**  
- **Many states**
- **High computational cost for policy evaluation**

Value Iteration is more efficient because it avoids repeated full evaluations and focuses on the most promising actions during each sweep.

#### Summary Comparison

| Aspect                 | Policy Iteration                           | Value Iteration                            |
|------------------------|---------------------------------------------|---------------------------------------------|
| Evaluation Step        | Full convergence required                  | Single sweep (approximate)                  |
| Efficiency in Large MDPs | Can be slow due to evaluation cost         | More efficient for large state spaces       |
| Convergence Speed      | Fewer iterations but slower per iteration  | More iterations but faster overall          |
| Suitable Scenario      | Small to medium MDPs                        | Large MDPs or when quick approximation needed|

---
### Using a Grid World environment, explain how policy improvement works during the policy iteration process.
#### 1. Evaluate Actions Based on $v_\pi$

- For each state $s$ in the Grid World, the algorithm considers **all possible actions** $a$ (e.g., north, south, west, east).
- Each action is evaluated using the **Q-value function** under the current policy:
  $$
  q_\pi(s, a) = \sum_{s', r} P(s', r | s, a) \left[ r + \gamma v_\pi(s') \right]
  $$

#### 2. Select the Best Action

- At each state $s$, the improved policy $\pi'(s)$ selects the action $a$ that maximizes $q_\pi(s, a)$:
  $$
  \pi'(s) = \arg\max_a \, q_\pi(s, a)
  $$
- This means the new policy is **greedy** with respect to the current value function $v_\pi$.

#### 3. Example: State 2 in Grid World

- Suppose in state **2**, different actions lead to:
  - Left → terminal state (value = 0)  
  - Down → state with value = -18  
  - Right → state with value = -20  
- Since the "left" action yields the **highest value**, the improved policy selects:
  $$
  \pi'(2) = \text{left}
  $$

#### 4. Repeat for All States

- This improvement process is repeated for **every state** in the Grid World.
- For each state, the action that maximizes $q_\pi(s, a)$ is selected to form $\pi'$.

#### 5. Derive New Policy $\pi'$

- The result is a **new policy** $\pi'$ that is **greedy with respect to** $v_\pi$.
- If $\pi' \neq \pi$, the new policy is **strictly better**, and the algorithm proceeds with **another Policy Evaluation** using $\pi'$.

#### Policy Iteration Cycle

- This cycle of **Policy Evaluation → Policy Improvement** continues until the policy stops changing:
  $$
  \pi' = \pi
  $$
- At this point, the policy is **optimal**.

---
### How does the Bellman equation factor into both Policy Iteration and Value Iteration?
#### 1. Policy Iteration — Policy Evaluation Step

- The goal of the **Policy Evaluation** step is to compute the **state-value function** $v_\pi(s)$ for a **fixed policy** $\pi$.
- This is done using the **Bellman expectation equation**:
  
$$
v_{k+1}(s) = \sum_a \pi(a|s) \left[ R(s, a) + \gamma \sum_{s'} P(s' | s, a) v_k(s') \right]
$$

Where:

- $v_k(s)$: Estimate of the value function at iteration $k$  
- $\pi(a|s)$: Probability of taking action $a$ in state $s$ under policy $\pi$  
- $R(s, a)$: Expected immediate reward  
- $\gamma$: Discount factor  
- $P(s' | s, a)$: Probability of transitioning to state $s'$ given state $s$ and action $a$

- This update is repeated **iteratively** for all states until $v_k(s)$ converges to $v_\pi(s)$.

#### 2. Value Iteration — Optimal Value Function

- **Value Iteration** aims to directly compute the **optimal value function** $v^*(s)$.
- It uses the **Bellman optimality equation**, which includes a **maximization over actions**:
  
$$
v_{k+1}(s) = \max_a \left[ R(s, a) + \gamma \sum_{s'} P(s' | s, a) v_k(s') \right]
$$

- This equation updates the value function by choosing the **best possible action** at each state during each iteration.
- It effectively combines:
  - **Value estimation** (from the Bellman equation)
  - **Policy improvement** (via the $\max$ operation)
- This process continues until $v_k(s)$ converges to the **optimal value function** $v^*(s)$.

#### Summary of Key Differences

| Aspect                | Policy Iteration                       | Value Iteration                                 |
| --------------------- | -------------------------------------- | ----------------------------------------------- |
| Bellman Equation Used | Expectation equation for $v_\pi$       | Optimality equation for $v^*$                   |
| Action Selection      | Weighted by $\pi(a\|s)$                | Uses $\max_a$ to select the best action         |
| Policy Evaluation     | Performed fully until convergence      | Skipped; combined into a single step            |
| Goal                  | Evaluate current policy and improve it | Directly find the optimal policy/value function |
