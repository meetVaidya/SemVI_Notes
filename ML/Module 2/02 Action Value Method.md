## Initial Strategies and Their Problems

### Strategy 1 (Explore-then-Exploit)

If we knew the average reward for each lever, the problem would be easy: always pull the lever with the highest average reward.
One possible approach:
1.  First, use some pulls to figure out which lever has the highest average reward (exploration phase).
2.  Then, only pull on that lever (exploitation phase).

To figure out the best lever, we need to try all levers multiple times because individual pulls are random, even if the average is fixed. We can then average the pulls for each lever.

**Algorithm 1 (Simplified):**
1.  Pull each lever `n` times, and average the `n` rewards from each lever.
2.  Whichever lever has the highest average is considered the best. Pull that one exclusively from now on.

**Problem with Strategy 1:**
*   We don't know how to set `n`.
*   If `n` is too small (e.g., `n=3`), our estimate of the average reward might be inaccurate due to luck (e.g., a lever with a true average of 5 gives rewards 14, 15, 16, averaging to 15). We might then wrongly exploit a suboptimal lever.
*   If `n` is too large, we waste too many pulls during the exploration phase, especially if we have a limited number of total pulls.

### Strategy 2 (Pure Greedy based on Running Average)

**Algorithm 2:**
1.  Before doing any pulls, set the running average of each lever to 0.
2.  For each timestep:
    *   Pick the lever with the highest current running average. If there is a tie, pick randomly between the tied levers.
    *   Pull the chosen lever, observe the reward, and update the running average for that lever.

**Problem with Strategy 2:**
*   Theoretically, the running average gets closer to the true average for each lever *that is pulled*.
*   However, this strategy has **no explicit exploration**. If an optimal lever initially gives a poor reward by chance, and a suboptimal lever gives a good reward, the algorithm might get stuck exploiting the suboptimal lever forever, never trying the optimal one again.
*   **Issue: No Exploration!**

### Strategy 3 (Introducing Epsilon for Exploration)

One fix for the problem of no exploration is to use a parameter, **epsilon (ε)**, that controls whether we pull the lever with the highest running average (exploit) or pull a random lever (explore). This leads to the ε-greedy method.

## Value Action Based Method (Sample Average)

To formalize these ideas, we estimate the value of each action (arm).

*   Let `Q*(a)` be the true (actual) value of action `a`.
*   Let `Q_t(a)` be the estimated value of action `a` at time step `t`.
*   The true value of an action is the mean reward received when that action is selected.

If at the `t`-th play, action `a` has been chosen `k_a` times prior to `t`, yielding rewards `r_1, r_2, ..., r_{k_a}`, then its value is estimated as the **sample average**:

`Q_t(a) = (r_1 + r_2 + ... + r_{k_a}) / k_a`

(Image context: Formula for Q_t(a) as a sum of rewards divided by k_a.)

This can also be written as:
`Q_t(a) = (Σ_{i=1}^{N_t(a)} R_i) / N_t(a)`
where `N_t(a)` is the number of times action `a` has been selected prior to time `t`, and `R_i` are the rewards received from action `a`.

(Image context: Alternative formula for Q_t(a) using N_t(a).)

By the law of large numbers, as `k_a → ∞` (or `N_t(a) → ∞`), `Q_t(a) → Q*(a)`.
`lim_{k_a→∞} Q_t(a) = Q*(a)`

(Image context: Limit expression showing convergence.)

### Sample Average Method Details

*   If an action `a` has never been chosen (`k_a = 0` or `N_t(a) = 0`), then `Q_t(a)` is often defined as some default value, such as `Q_1(a) = 0`.
*   This method is called the **sample-average method** because each estimate is a simple average of the sample of relevant rewards.
*   The algorithm updates action values using the sample mean of observed rewards.
*   Over time, as the number of samples for an action grows, its estimated value converges to the true expected reward for that action.