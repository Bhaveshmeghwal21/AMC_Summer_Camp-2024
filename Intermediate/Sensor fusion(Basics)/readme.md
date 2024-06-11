# Kalman Filter #

The Kalman filter is an algorithm that provides estimates of some unknown variables given the measurements observed over time. It's widely used in control systems, robotics, and other autonomous systems. Imagine you're trying to track the position of a car based on noisy GPS signals. The Kalman filter helps you combine the noisy measurements with a model of the car's movement to get a more accurate estimate of its position.

### Basic Concepts:
1. **State**: The set of variables you want to estimate (e.g.,orientation, position and velocity of the car).
2. **Measurements**: The observed data you have (e.g., GPS signals).
3. **Prediction**: Using a model to predict the next state based on the current state.
4. **Update**: Correcting the prediction using the new measurements.

### Steps of the Kalman Filter:

1. **Initialization**:
   - Define the initial state estimate  $(\mathbf{x}_0)$
   - Define the initial covariance estimate $(\mathbf{P}_0\)$

2. **Prediction Step**:
   - Predict the next state $(\mathbf{x}_{k|k-1}\)$ using the current state $(\mathbf{x}_k\)$ and a model of the system's dynamics.
   - Predict the next covariance $(\mathbf{P}_{k|k-1}\)$.

3. **Update Step**:
   - Compute the Kalman Gain $(\mathbf{K}_k\)$.
   - Update the state estimate $(\mathbf{x}_k\)$ using the new measurement $(\mathbf{z}_k\)$.
   - Update the covariance estimate $(\mathbf{P}_k\)$.

### Equations:

1. **Initialization**:
  
   $\mathbf{x}_0 = \text{initial state estimate}$
  
   $\mathbf{P}_0 = \text{initial covariance estimate}$

2. **Prediction**:

   $\mathbf{x}_ {k|k-1}\$ = $(\mathbf{F}_ {k}\)$ $(\mathbf{x}_ {k-1}\)$ + $(\mathbf{B}_k)$ $(\mathbf{u}_k)$
       
   $\mathbf{P}_ {k|k-1}$ = $(\mathbf{F}_ {k}\)$ $(\mathbf{P}_{k-1})$ $(\mathbf{F}_k^\top)$ + $\mathbf{Q}_k $
   - $(\mathbf{F}_k\)$: State transition model (how the state changes).
   - $(\mathbf{B}_k\)$: Control input model (how external controls affect the state).
   - $(\mathbf{u}_k\)$: Control input.
   - $(\mathbf{Q}_k\)$: Process noise covariance (uncertainty in the model).

4. **Update**:

   $\mathbf{y}_ k$ = $(\mathbf{z}_ k)$ - $(\mathbf{H}_ k\)$ $(\mathbf{x}_{k|k-1})$
   
   $\mathbf{S}_ k$ = $(\mathbf{H}_ k)$ $(\mathbf{P}_ {k|k-1})$ $(\mathbf{H}_k^\top)$ + $\mathbf{R}_k$
   
   $\mathbf{K}_ k$ = $(\mathbf{P}_ {k|k-1})$ $(\mathbf{H}_k^\top)$ $(\mathbf{S}_k^{-1})$
  
   - $(\mathbf{y}_k\)$: Measurement residual (difference between actual and predicted measurement).
   - $(\mathbf{H}_k\)$: Measurement model (how to map the state to the measurement).
   - $(\mathbf{R}_k\)$: Measurement noise covariance (uncertainty in the measurements).
   - $(\mathbf{S}_k\)$: Residual covariance.

6. **State Update**:

   $\mathbf{x}_ k$ = $\mathbf{x}_{k|k-1}$ + $\mathbf{K}_k$ $\mathbf{y}_k$


   $\mathbf{P}_ k$ = ($\mathbf{I}$ - $(\mathbf{K}_ k)$ $(\mathbf{H}_ k\)$ ) $(\mathbf{P}_{k|k-1})$

   - $(\mathbf{I}\)$: Identity matrix.

### Simplified Explanation:

1. **Start with an initial guess** of where the drone is and how certain you are about this guess.
2. **Predict the new position** using the drone's speed and direction.
3. **Get a new GPS measurement** and see how far it is from the predicted position.
4. **Adjust the prediction** by blending it with the new measurement, weighing them by their uncertainties.
5. **Update your guess** about the drone's position and how certain you are now.

By repeating these steps, the Kalman filter continuously refines the estimate of the car's position, giving more accurate and reliable results over time.
