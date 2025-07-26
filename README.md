# Analysis of Epidemic Spread Using Mathematical and Computational Models

This project explores the dynamics of disease spread using a combination of mathematical and computational modeling techniques. It leverages various models to simulate how an infectious disease, referred to as "SHU Flu," propagates through a population, and evaluates different intervention strategies.

## Author

Jonah Zembower

## Date

May 11, 2024

## Project Overview

The primary goal of this project is to analyze and predict disease trajectories under various conditions by applying both deterministic and stochastic models, as well as neural networks. The study also investigates the effectiveness of different public health interventions.

## Data

The project utilizes two primary datasets:

* **`Disease_Spread.csv`**: This dataset contains daily records of a simulated disease spread, including:
    * **Day**: The day number in the simulation.
    * **Susceptible**: The number of individuals susceptible to infection.
    * **Infected**: The number of currently infected individuals.
    * **Recovered**: The number of individuals who have recovered and are assumed immune.

* **`Population_Contact_Network.csv`**: This dataset represents social interactions within a population, suitable for constructing a network graph where `Person1` and `Person2` indicate a contact between individuals that could lead to disease transmission.

### Data Preprocessing

Both datasets were checked for missing values, negative counts in disease spread data, and duplicate network interactions. No anomalies were found, indicating the data is well-prepared for analysis and modeling.

## Methodology

### 1. Deterministic SIR Model

The Susceptible-Infected-Recovered (SIR) model, a system of differential equations, was used to understand the basic dynamics of the epidemic. This model tracks the change in the number of susceptible, infected, and recovered individuals over time, based on assumed infection (β) and recovery (γ) rates. The simulation shows the characteristic peak in infected individuals followed by a decline as individuals recover. Different `beta` and `gamma` values were tested to observe their impact on the epidemic curve, revealing that higher `beta` values lead to quicker, broader spreads, while higher `gamma` values reduce infection duration and peak infection rates.

### 2. Stochastic SIR Model

To account for the inherent randomness in disease transmission and recovery, a stochastic SIR model was implemented using the Gillespie algorithm. This discrete-event simulation method provides a more realistic and nuanced understanding of how disease spread might fluctuate. The stochastic model's infected curve exhibits a jagged nature, reflecting random events, and shows variability in peak timing and epidemic duration, which contrasts with the smoother deterministic curves.

### 3. Neural Network Predictions

Neural networks, including Long Short-Term Memory (LSTM) and Bidirectional LSTM (Bi-LSTM) layers, were employed to predict future disease spread. The data was scaled using `MinMaxScaler`, and `TimeseriesGenerator` was used to prepare input sequences. A `TimeSeriesSplit` cross-validation strategy was utilized for robust model evaluation.

* **Model Architecture**: The neural network models typically included LSTM or Bi-LSTM layers followed by Dense layers.
* **Evaluation**: The models were evaluated using Mean Squared Error (MSE) and Mean Absolute Error (MAE).
    * Mean Squared Error: 120.016
    * Mean Absolute Error: 10.949
    While the models provided predictions, the results suggested a need for further improvement.

### 4. Graph Theory Analysis and Network-Based SIR Model

The `Population_Contact_Network.csv` was used to build a contact network graph. This network was then integrated into an SIR model to simulate disease spread on a realistic social structure, allowing for the observation of how network topology influences transmission.

### 5. Comparing Intervention Strategies

The project also included an analysis of different intervention strategies to compare their effectiveness in mitigating disease spread:

* **Targeted Vaccination**: Focused on vaccinating highly connected individuals, found to be effective but resource-dependent.
* **Social Distancing**: Reduced the overall transmission rate, leading to a flatter epidemic curve.
* **Lockdown**: A more stringent intervention, resulting in the most drastic reduction in infection peak and a significant delay in disease spread.

## Technologies Used

The project was developed in Python and utilized the following key libraries:

* **pandas**: For data loading and manipulation.
* **numpy**: For numerical operations, especially with array handling.
* **matplotlib.pyplot** & **seaborn**: For data visualization and plotting simulation results.
* **networkx**: For creating and analyzing contact networks in graph theory.
* **scipy.integrate**: Specifically `solve_ivp` for solving the differential equations in the deterministic SIR model.
* **scikit-learn (sklearn)**: For data preprocessing (`MinMaxScaler`), and model evaluation (`mean_squared_error`, `mean_absolute_error`).
* **keras** (from tensorflow.keras): For building and training neural networks, including `TimeseriesGenerator`, `Sequential`, `LSTM`, `Dense`, `Dropout`, and `Bidirectional` layers.

## Files in the Repository

* `Disease_Spread.csv`: Dataset containing daily counts of susceptible, infected, and recovered individuals.
* `Population_Contact_Network.csv`: Dataset detailing social contacts within a population, used for network modeling.
* `Final_Project.ipynb`: The main Jupyter Notebook containing all the code for data loading, preprocessing, model implementation (deterministic SIR, stochastic SIR, neural networks, network-based SIR), analysis, and visualization.
* `Final Project.pptx`: A presentation summarizing the project's methodologies, findings, and conclusions.
* `README.md`: This README file.
