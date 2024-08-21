
# Approximate Bayesian Computation (ABC) for COVID-19 Parameter Inference

## Overview

This repository contains an implementation of an Approximate Bayesian Computation (ABC) algorithm to infer parameters of a model simulating the spread of COVID-19 in Italy.

### Model Definition and Simulation
- The code defines a simulation of the COVID-19 spread based on an SIR (Susceptible-Infected-Recovered) model, where:
  - `S_store`, `I_store`, `A_store`, `R_store`, `D_store`, and `Ru_store` represent the susceptible, infected, asymptomatic, recovered, deceased, and unreported cases, respectively.
- The model evolves over time, and for each day, the number of new cases is calculated using a set of parameters (`param_vector`), which are drawn from uniform distributions.

### Sampling from the Prior Distribution
- The parameters of the model (e.g., infection rate, recovery rate) are sampled from predefined uniform distributions, representing the prior belief about these parameters before observing any data.

### Running the Simulation
- The simulation is run for a number of days (`num_days`), generating synthetic data based on the sampled parameters.

### Distance Calculation
- After running the simulation, the code calculates the distance between the simulated data (`t_summary`) and the actual observed data (`country_data_train`). This distance is computed using a norm (e.g., Euclidean distance) and is stored in `distances`.
- The `reduced_distances` variable sums these distances across all days for each set of parameters.

### Acceptance Step
- ABC accepts or rejects parameter sets based on their distance from the observed data. If the distance (`reduced_distances`) is less than a predefined tolerance (`tolerance`), the parameters are accepted as plausible given the observed data.
- This is implemented in the line `acceptance_vector = reduced_distances <= tolerance`, where the `acceptance_vector` determines which parameter sets are accepted.

### Parameter Inference
- The accepted parameters are stored, and the algorithm continues running until a sufficient number of samples (`samples_target`) are collected.
- The accepted parameters represent the posterior distribution of the model parameters, given the observed data.

### Post Processing
- After enough samples are collected, the code post-processes the accepted samples, returning the parameter sets that best match the observed data.

## Summary of ABC in the Code:
**ABC** is used here to estimate the parameters of the COVID-19 spread model by comparing simulated data against real-world data from Italy. The main steps involve generating simulated data based on sampled parameters, comparing this data with the observed data, and accepting or rejecting the parameter sets based on how well the simulation matches the real data. This allows for inference on the model parameters that are most consistent with the observed epidemic data.
