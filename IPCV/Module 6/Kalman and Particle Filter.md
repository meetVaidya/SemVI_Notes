## Kalman Filter

The Kalman Filter is an algorithm used for estimating the state of a dynamic system from noisy measurements over time, particularly effective in linear systems with Gaussian noise. It operates in two steps:

- **Prediction Step**: Uses a model of the system to predict the next state and its uncertainty based on the current state.
    
- **Update Step**: Incorporates new measurements to refine the predicted state, calculating a Kalman Gain to balance the weight of the prediction and the new data, thus reducing uncertainty.
    

**Key Features**:

- Efficient and recursive, updating estimates as new data arrives.
    
- Ideal for simpler, linear systems (e.g., GPS tracking a vehicle’s position).
    
- **Example**: Tracking a car in a traffic video by predicting its next position based on speed and direction, adjusting with new camera data.
    

## Particle Filter (Sequential Monte Carlo Method)

The Particle Filter is a probabilistic method for state estimation in non-linear systems with unpredictable noise, using a set of particles to represent possible states. It works through:

- **Sampling**: Generates multiple particles, each representing a hypothesis of the system’s state.
    
- **Weighting**: Assigns importance to each particle based on how well it matches observed data.
    
- **Resampling**: Focuses on high-weight particles, discarding unlikely ones to refine the estimate.
    

**Key Features**:

- Handles complex, non-linear systems better than Kalman Filter.
    
- Computationally intensive due to managing multiple particles.
    
- **Example**: Localizing a robot in a cluttered environment by testing various position hypotheses and updating based on sensor data.