## The Exploration vs. Exploitation Dilemma

*   A key question in reinforcement learning is the dilemma between **exploration** and **exploitation**.
    *   **Explore:** To find profitable actions by trying out different options, even those not currently believed to be the best. This helps gather information.
    *   **Exploit:** To act according to the best observations already made, choosing the action currently believed to yield the highest reward.
*   **Bandit problems** are a simplified framework that encapsulates this 'Explore vs Exploit' dilemma.

## The Multi-Armed Bandit (MAB) Problem

*   The Multi-Armed Bandit (MAB) problem serves as a foundational concept, illustrating the challenges and strategies of **decision-making under uncertainty**.

## What is a Bandit Problem?
*   **Bandit:** Defined as someone (or something, like a slot machine) that "steals" your money.
*   **One-armed bandit:** A simple slot machine where you insert a coin, pull a lever (arm), and get an immediate reward.
*   **Why "bandit"?** Casinos historically configured slot machines so that gamblers would, on average, end up losing money.

## Multi/N/K - Armed Bandit Problem

This refers to a scenario with multiple "arms" or choices, each with an unknown reward distribution.

## What is a K-armed Bandit Problem?

*   Imagine the bandit as a slot machine with **k arms** (levers).
*   Pulling one of the k levers yields a positive reward.
*   **Goal:** Maximize your total reward over a fixed number of pulls (e.g., 1000 pulls).
*   **Prior Information (Stationary Case):** The only prior information is that the average reward for each lever doesn't change over time (i.e., the reward distributions are stationary).

## Core Challenge in MAB

The core challenge in the MAB problem is **balancing exploration and exploitation**.

*   **Exploration:** Involves trying different arms to gather information about their rewards.
*   **Exploitation:** Means leveraging known information to choose the arm believed to offer the highest reward.

## K-Armed Bandit Interaction Loop

(Image context: A diagram showing the interaction loop:
Agent -> (Select Arm) -> Bandit -> (Reward) -> Agent.
The Bandit is labeled "k-Armed Bandit".)