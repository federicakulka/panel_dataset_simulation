# panel_dataset_simulation
This code generates panel data with a specified treatment effect, performs a single event study analysis, and runs multiple simulations using Monte Carlo methods. The goal is to estimate the impact of a treatment that starts at time period 10, for randomly assigned treated units and for periods ranging from -5 to +5, and visualize the treatment effects with a density plot.

### Code Structure

### 1. **`generate_data_and_log_earnings` function:**

Generates synthetic panel data and computes log-earnings based on individual characteristics and treatment status.

**Arguments:**

- `N`: Number of individuals.
- `T`: Number of time periods.
- `sigma`: Standard deviation of the error term.
- `alpha`: Intercept for the log-earnings model.
- `beta_treatment`: Coefficient for the treatment effect.
- `beta_age`: Coefficient for the effect of age.
- `beta_education`: Coefficient for the effect of education.
- `beta_experience`: Coefficient for the effect of experience.
- `seed`: Optional random seed for reproducibility.

**Key Operations:**

- Generates individual (`id`) and time (`time`) variables.
- Randomly assigns half the individuals to receive the treatment, starting at time period 10.
- Simulates individual fixed effects, time fixed effects, and random error terms.
- Computes log-earnings based on control variables and treatment status.
- Returns a DataFrame with all relevant variables (`id`, `time`, `age`, `education`, `experience`, `treatment`, and `log_earnings`).

### 2. **`run_event_study` function:**

Performs an event study regression, estimating the impact of treatment on log-earnings over event time. The coefficients estimated are relative to time t=10, when treatment is implemented.

**Arguments:**

- `df`: The DataFrame containing the generated data.
- `seed`: Optional random seed for reproducibility.

**Key Operations:**

- Creates event-time dummies relative to the treatment start (event time = 0).
- Filters data to focus on event times between -5 and +5.
- Runs a linear regression on log-earnings, including control variables (`age`, `education`, `experience`) and event-time dummies.
- Returns a summary of the model and the estimated treatment effects for each event time.

### 3. Data Simulation and Event Study Estimation

The code performs a single simulation of the panel data using the **`generate_data_and_log_earnings`** function; then, a histogram of the simulated log-earnings is generated to ensure the data follows a normal distribution. Finally, the single event study regression is run using the generated data through the **`run_event_study`** function.

### 4. **Monte Carlo Simulation Loop:**

Runs multiple iterations of the data generation and event study to simulate variability and estimate treatment effects.

**Key Operations:**

- Loops over `num_simulations` to generate new data for each iteration.
- Collects treatment effect estimates for each event time period.
- Stores results in a DataFrame and provides a summary of the estimated treatment effects.

### 5. **Analysis and Visualization:**

After running the simulations, a density plot visualizes the distribution of treatment effect estimates over different event periods.

- **Plotting:** Uses `seaborn.kdeplot` to generate density plots for event-time treatment effects.

### How to Use

1. **Set Parameters:**
    - It is possible to modify key parameters like `N` (number of individuals), `T` (number of time periods), `beta_treatment` (expected treatment effect), and `num_simulations` (number of Monte Carlo simulations) at the top of the script.
2. **Simulate Data Once and Perform Event Study:**
   - Use the provided code to generate a single dataset and run an event study.
   - Visualize the distribution of log-earnings and analyze the event study output.
3. **Run Monte Carlo Simulation:**
   - Perform multiple simulations and analyze the distribution of treatment effects.
