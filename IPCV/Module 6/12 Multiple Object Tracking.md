## Definition

*   **Multiple Object Tracking (MOT):** The task of tracking several objects (like people, cars, etc.) across frames in a video. This involves not only following each object but also maintaining their identities over time, even through occlusions or interactions.

## Two Main Parts in MOT

### 1. How Tracking is Started (Initialization Methods)

*   **Detection-Based Tracking (DBT):**
    *   **Process:**
        1.  Detect objects in each frame first using an object detector (e.g., YOLO, Faster R-CNN).
        2.  Then link these detections across frames to form trajectories and follow each object.
    *   **Example (Slide 38):**
        > A security camera detects people entering a store using a person detector. Once detected, the system assigns IDs to each person and keeps tracking them as they move. If a person leaves and re-enters, the system tries to recognize them again using detection.
    *   This is the dominant paradigm in modern MOT.

*   **Detection-Free Tracking (DFT):**
    *   **Process:**
        1.  You manually (or through some other non-detection means) give the starting location of the object(s) in the first frame.
        2.  The system then follows the object(s) in subsequent frames based on appearance, motion, etc., *without* needing an object detector in each frame.
    *   **Example (Slide 39):**
        > You are tracking a cricket ball in a video. You click manually on the ball's position in the first frame. The system then follows the ball in the next frames using its appearance and motion — without using a detector.
    *   Less common for general MOT but can be useful in specific scenarios or for single object tracking where initialization is manual.

## MOT Components

Effective MOT systems often integrate several components:

*   **Appearance Model:**
    *   **Description:** Involves visual representation and statistical measurement to compute affinity (similarity) between objects in different frames. It helps in re-identifying objects.
    *   **Features:** Can include local features like KLT (Kanade-Lucas-Tomasi) trackers, or region features like color histograms and gradient-based representations (e.g., HOG - Histogram of Oriented Gradients).
    *   **Example:**
        > A red car is tracked using its color and shape across video frames.

*   **Motion Model:**
    *   **Description:** Captures the dynamic behavior of objects to predict their future positions.
    *   **Types:**
        *   Linear motion models (e.g., constant velocity, constant acceleration) assume simpler movements.
        *   Non-linear models are used for more complex motions (e.g., Kalman filters for linear, Particle filters for non-linear).
    *   **Example:**
        > A person walking in a straight line is predicted in the next frame using their previous speed and direction.

*   **Exclusion Model:**
    *   **Description:** Ensures that two distinct objects don't occupy the same physical space or that one detection isn't assigned to multiple tracks if they are physically distinct.
    *   **Levels:** Can include detection-level (e.g., non-maximum suppression) and trajectory-level exclusion modeling.
    *   **Example:**
        > Two cars cannot be tracked as one if they are far apart—ensures no overlapping identities for spatially separated objects.

*   **Occlusion Handling:**
    *   **Description:** Strategies to manage situations where objects are temporarily hidden from view (e.g., by other objects or parts of the scene). This is a primary challenge in MOT.
    *   **Strategies:** Include part-to-whole reasoning, hypothesize-and-test, and buffer-and-recover (waiting for an object to reappear).
    *   **Example:**
        > If a person is briefly hidden behind a pole, the tracker guesses their position based on their motion model and attempts to re-associate them when they reappear.

## Basic MOT Methods

Several methods and algorithms are foundational or commonly used in MOT:

1.  **Frame-by-Frame Tracking (Data Association):**
    *   The core of DBT, where detections in the current frame are associated with existing tracks from previous frames.
2.  **Kalman Filter:**
    *   Often used for motion modeling and state prediction in linear or near-linear scenarios.
3.  **Particle Filter (Sequential Monte Carlo Method):**
    *   Used for motion modeling in non-linear, non-Gaussian scenarios.
4.  **Optical Flow:**
    *   Can be used to predict motion or to track feature points on objects.
5.  **Simple Online and Realtime Tracking (SORT):**
    *   **Description:** An algorithm that combines Kalman filtering for motion prediction and the Hungarian algorithm for data association (matching detections to tracks).
    *   **Characteristics:** Designed for online and real-time tracking scenarios and is known for its speed and simplicity.
6.  **Hungarian Algorithm (for Data Association):**
    *   **Description:** A combinatorial optimization algorithm that solves the assignment problem in polynomial time.
    *   **Use in MOT:** Used to associate current frame detections to previously established tracks efficiently by finding the optimal assignment that minimizes a cost (e.g., based on IOU or appearance similarity).
7.  **Multiple Hypothesis Tracking (MHT):**
    *   **Description:** Maintains several hypotheses (potential trajectories) for each object and selects the most likely one over time.
    *   **Characteristics:** More computationally intensive than methods like SORT but can be more robust against missed detections and false positives by deferring decisions.