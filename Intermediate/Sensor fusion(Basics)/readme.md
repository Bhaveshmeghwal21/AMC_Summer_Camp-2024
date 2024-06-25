# Why Sensor fusion? #
Sensor fusion combines data from multiple sensors to obtain more accurate and reliable information than what could be achieved using individual sensors alone. This technique is crucial for improving measurement accuracy, reducing uncertainty, and providing robust performance in various conditions. It is essential in applications such as robotics, autonomous vehicles, and mobile devices, where precise and dependable data is necessary for making informed decisions and ensuring safety.

# Why to use filters ? #

Filters are used in sensor fusion to smooth out noise, correct for sensor drift, and integrate different types of sensor data in a coherent manner.

**Common Filters:**
- Complementary Filter
- Kalman Filter
- Extended Kalman Filter (EKF)
- Unscented Kalman Filter (UKF)
- Particle Filter


----------------------------------------------------------------------------------------------------------------------------------------------------------

# Complememtary Filter #

This section implements a complementary filter for sensor fusion, combining data from a gyroscope and an accelerometer to provide an accurate estimate of orientation.

## Overview

A complementary filter is a simple yet effective method for combining measurements from different sensors to estimate a system's state. It is particularly useful in applications like robotics and aerospace for estimating orientation (pitch, roll, yaw).

## How It Works

The complementary filter leverages the strengths of both the gyroscope and the accelerometer:

- **Gyroscope**: Provides accurate short-term angular velocity data but suffers from drift over time.
- **Accelerometer**: Provides good long-term orientation data but is noisy in the short term.

By blending high-frequency data from the gyroscope with low-frequency data from the accelerometer, the complementary filter provides a reliable estimate of orientation.

## Formula

The complementary filter uses the following formula:

$\theta$ = $\alpha$ $(\theta_{\text{prev}}$ + $\text{gyro} \times \Delta t$) + $(1 - \alpha) \times \text{accel}$ 

Where:
- $(\theta\)$ is the estimated angle.
- $\(\theta_{\text{prev}}\)$ is the previously estimated angle.
- $\(\text{gyro}\)$ is the angular velocity measured by the gyroscope.
- $\(\text{accel}\)$ is the angle measured by the accelerometer.
- $\(\Delta t\)$ is the time interval between measurements.
- $\(\alpha\)$ is the filter coefficient (typically between 0 and 1).

## Example Calculation

Given:
- Gyroscope reading: 0.1 rad/s
- Accelerometer reading: 0.05 radians
- Previous angle: 0.04 radians
- Time interval $\(\Delta t\)$: 0.01 seconds
- Filter coefficient $\(\alpha\)$: 0.98

The estimated angle is calculated as follows:

1. Calculate the gyroscope contribution:
\[ $\theta_{\text{gyro}} = \theta_{\text{prev}} + \text{gyro} \times \Delta t = 0.04 + 0.1 \times 0.01 = 0.041$ \]

2. Combine with the accelerometer measurement:
\[ $\theta = \alpha \times \theta_{\text{gyro}} + (1 - \alpha) \times \text{accel}$ \]

\[ $\theta = 0.98 \times 0.041 + 0.02 \times 0.05$ \]

\[ $\theta = 0.04018 + 0.001 = 0.04118$ \]

So, the estimated angle is approximately 0.04118 radians.

## Explore Further(Necessary)
1. https://youtu.be/whSw42XddsU?si=3inLG5wTCqIn4F5x
2. https://youtu.be/vknohSbR6ME?si=5314XewHJw4kOotP
3. https://vanhunteradams.com/Pico/ReactionWheel/Complementary_Filters.html
4. https://www.quora.com/What-is-a-complimentary-filter-How-does-it-differ-from-a-Kalman-filter






----------------------------------------------------------------------------------------------------------------------------------------------------------














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


## Explore Further(Necessary)
1. https://thekalmanfilter.com/covariance-matrix-explained/
2. https://thekalmanfilter.com/kalman-filter-explained-simply/   (must)
3. https://www.bzarg.com/p/how-a-kalman-filter-works-in-pictures/
4. https://youtu.be/IFeCIbljreY?si=ZG-WtDbfAV_eO6n_
5. https://youtube.com/playlist?list=PLn8PRpmsu08pzi6EMiYnR-076Mh-q3tWr&si=vUqHjIB8fodBikNR
6. https://youtu.be/bm3cwEP2nUo?si=Y9XtPVoH4jKvxHDh





**Note:**    
I know many of you didn't understand the filter in one go, it's natural if you take time.Just go through the given texts and links.

Remember learning is always a self-paced process you have to find the answer by yourself and if you didn't get anything from any of the above resources you are free to learn from web and find the needed. You all will get to learn more about sensor fusion and the task on it in advance section. 

Till then- 
**Happy Learning!!**






