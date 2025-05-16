## Definition

- By formal definition, Reinforcement Learning is the area of machine learning in which the objective is to train the an artificial agent in a stochastic environment to perform a certain task by letting it interact with the environment repeatedly.
- The agent aims to learn from its interaction with the surrounding environment, hence there is no external “teacher” to provide correct actions to the agent. Instead a reward function is set to provide the agent the evaluation of whether it is going in the right direction

## Terms in RL

1. **Agent:** an entity that can explore the environment
2. **Environment :** a situation in which an agent is present or surrounded by; it can be stochastic in nature
3. **Action :** moves taken by the agent within the environment
4. **State** : situation made by the environment after each action taken by the agent
5. **Reward** : a feedback returned to the agent from the environment to evaluate the action
6. **Policy** : provides the probability that an agent will take an action in a given state
7. **Value**: The **expected return** (sum of future rewards) from a state **assuming the agent follows a certain policy**
8. **Q-Value** : The **expected return** from taking a specific action **`a` in state `s`**, and then following the policy

## Approaches of Implementing RL

- There are 3 ways to implement reinforcement learning in ML
	1. **Value-Based**
	2. **Policy-Based**
	3. **Model-Based**

### Value-Based
**Goal:** Learn the **value function** — how good it is to be in a given state or to take a certain action in that state.
- Uses a function like **Q(s, a)** (action-value) or **V(s)** (state-value).
- The **policy is derived** implicitly: pick the action with the **highest value**.
- No explicit policy is learned.
- Common algorithms:
    - **Q-learning**
    - **Deep Q-Network (DQN)**

> Example: The agent chooses actions that maximize expected **future rewards** based on estimated values.

### Policy-Based
**Goal**: Find the optimal policy for the maximum rewards without using the value function. The agent tries to apply such policy that the action performed in each step helps to maximize the future reward.
- Can be **stochastic** (π(a|s)) or **deterministic**.
- Optimizes policy using **gradient ascent** on expected reward (e.g., **Policy Gradient** methods).
- Doesn’t rely on a value function (though it can use one — see Actor-Critic).
- Common algorithms:
    - **REINFORCE**
    - **Proximal Policy Optimization (PPO)**
    - **Trust Region Policy Optimization (TRPO)**
> Example: The agent learns a **probability distribution** over actions and improves it directly.
### [[03 Model Free vs Model Based|Model-Based]]
**Goal**: The agent needs to make predictions of the possible rewards associated with certain actions.
- Learns:
    - **Transition function**: P(s'|s, a)
    - **Reward function**: R(s, a)
- Uses this model for **planning** and decision-making.
- Can combine with value or policy learning.
> Example: Like a **mental simulator**, the agent imagines outcomes before acting.