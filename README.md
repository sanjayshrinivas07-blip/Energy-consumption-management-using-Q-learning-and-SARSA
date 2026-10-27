# Energy Consumption Management Using Q-Learning and SARSA

## 📌 Project Overview

This project presents a comparative study of two reinforcement learning algorithms, **Q-Learning and SARSA**, for energy consumption management using historical household electricity consumption data.

The project converts continuous household power consumption into five discrete energy states and evaluates three conceptual energy management actions. Both algorithms learn action-selection policies through a reward-based framework, and their performance is compared using training rewards, test rewards, execution time, and multiple random seeds.

The main objective is to understand how two fundamental reinforcement learning algorithms behave in a simplified energy management environment.

## 🎯 Objectives

- Analyze historical household electricity consumption data.
- Perform data cleaning and exploratory data analysis.
- Discretize energy consumption into five states.
- Define a reward-based energy management environment.
- Implement Q-Learning and SARSA.
- Compare the algorithms using consistent evaluation conditions.
- Evaluate the stability of results across multiple random seeds.
- Identify the limitations of the simplified environment and possible future improvements.

## 🛠️ Technologies Used

- **Programming Language:** Python
- **Development Environment:** Google Colab / Jupyter Notebook
- **Libraries:** NumPy, Pandas, Matplotlib, Seaborn, and scikit-learn (where used in the notebook)
- **Core Concepts:** Reinforcement Learning, Q-Learning, SARSA, EDA, Data Preprocessing, Reward Functions, and Q-Tables

## 📂 Project Structure

```text
Energy-consumption-management-using-Q-learning-and-SARSA/
│
├── Energy_Q_Learning_SARSA_Case_Study.ipynb
├── README.md
├── report.pdf                  # Optional: add your final report
└── results/                    # Optional: add result plots and tables
```

The report and results folder are optional. Add them only if you upload those files to this repository.

## 📊 Dataset Description

The project uses historical household electricity consumption data containing measurements of household power usage.

The dataset is used to study energy consumption patterns and construct a simplified reinforcement learning environment.

### Dataset statistics

| Metric | Value |
|---|---:|
| Raw records | 2,075,259 |
| Records after cleaning | 2,049,280 |
| Records removed | 25,979 |
| Training records | 1,639,424 |
| Testing records | 409,856 |
| Mean active power | 1.092 kW |
| Median active power | 0.602 kW |
| Maximum active power | 11.122 kW |

### Data preprocessing

The notebook performs data cleaning and exploratory analysis before model training. The cleaned data is divided chronologically into 80% training data and 20% testing data.

The energy-state thresholds are calculated using training data only to avoid using test data when defining the states.

**Dataset source:** [Insert the actual dataset URL used in this project]

**Dataset licence:** [Insert the applicable licence or usage terms]

> Note: Verify the dataset's original source, units, and licence before publishing. Do not assume that the dataset can be redistributed.

## ⚙️ Methodology

### 1. Data preprocessing and exploratory analysis

The raw dataset is cleaned, and its main characteristics are examined using descriptive statistics and visualizations. The data is then split chronologically into training and testing sets.

### 2. Energy state discretization

Continuous global active power values are converted into five discrete states using training-data quantiles.

| State | Description |
|---|---|
| State 0 | Very Low |
| State 1 | Low |
| State 2 | Medium |
| State 3 | High |
| State 4 | Very High |

The training-derived thresholds are approximately:

- 0.272 kW
- 0.400 kW
- 1.266 kW
- 1.742 kW

These thresholds are specific to the dataset and preprocessing used in this experiment.

### 3. Action space

The model considers three conceptual energy management actions:

1. **Reduce Consumption** — encourages lower energy usage.
2. **Maintain Consumption** — represents maintaining the current consumption level.
3. **Allow Higher Consumption** — represents allowing a higher consumption level.

These are simulated actions in the experimental framework; they do not directly control real household appliances.

### 4. Reward function

A manually designed reward function assigns scores to state-action combinations to represent the intended energy management behaviour.

The agents use these rewards to learn which action to select in each energy state. The reward is an experimental score, not a direct measurement of electricity cost savings or energy saved in kWh.

### 5. Q-Learning

Q-Learning is an off-policy, value-based reinforcement learning algorithm. It updates its action-value estimates using the maximum estimated value of the next state.

### 6. SARSA

SARSA is an on-policy, value-based reinforcement learning algorithm. It updates its action-value estimates using the action actually selected in the next state.

### 7. Performance evaluation

Both algorithms are evaluated using the same general experimental framework. The evaluation includes:

- Training reward
- Mean test reward per evaluation window
- Training execution time
- Learned greedy policies
- A robustness experiment across five random seeds

## 📈 Experimental Results

### Main experimental run

| Evaluation metric | Q-Learning | SARSA |
|---|---:|---:|
| Last 50 training episodes: mean reward | 318.520 | 319.890 |
| Mean test reward per window | 288.920 | 288.920 |
| Test reward standard deviation | 90.1 | 90.1 |
| Training time | 3.897 seconds | 3.487 seconds |

In the main run, both algorithms achieved the same mean test reward and test reward standard deviation. SARSA had a slightly higher average training reward over the final 50 episodes and a shorter measured training time in this run.

### Five-seed robustness experiment

| Metric | Q-Learning | SARSA |
|---|---:|---:|
| Mean test reward across seeds | 319.332 | 323.972 |
| Standard deviation across seed-level test means | 61.933 | 65.110 |

Across five random seeds, SARSA achieved a mean test reward 4.640 points higher than Q-Learning. However, the difference is small compared with the variability across seeds, so these results do not establish that SARSA is definitively superior.

### Learned greedy policy

The main run produced the following policies for both algorithms:

| Energy state | Selected action |
|---|---|
| Very Low | Maintain Consumption |
| Low | Maintain Consumption |
| Medium | Reduce Consumption |
| High | Reduce Consumption |
| Very High | Maintain Consumption |

Both algorithms learned the same greedy policy in the main run.

The results should be interpreted within the assumptions of the simplified environment and its manually designed reward function.

## 🔍 Key Findings

- Both algorithms achieved identical mean test rewards in the main experimental run.
- SARSA had a slightly higher training reward over the last 50 episodes.
- SARSA recorded a shorter training time in the main run.
- SARSA achieved a modestly higher mean test reward across five seeds, but variability was substantial.
- Both algorithms learned the same greedy policy in the main run.
- The experiment demonstrates a comparative implementation of tabular reinforcement learning, not verified real-world energy savings.

## ⚠️ Limitations

- **Simplified environment:** The environment uses historical consumption data and does not fully simulate household behaviour.
- **Action-independent transitions:** The next state is replayed from historical data independently of the selected action. Therefore, the actions do not cause the simulated energy consumption to change.
- **Manually designed reward:** The reward function represents an experimental scoring system rather than actual electricity bills or measured energy savings.
- **Limited validation:** The experiment does not demonstrate performance in a real household or a validated action-dependent simulator.
- **Limited action space:** Only three conceptual actions and five energy states are considered.
- **Computational scope:** The study focuses on tabular Q-Learning and SARSA rather than more complex reinforcement learning methods.

## 🚀 Future Enhancements

- Develop an action-dependent environment in which actions influence future energy consumption.
- Design reward functions using electricity tariffs, peak-demand penalties, carbon emissions, or measured energy usage.
- Test the algorithms on multiple households and different time periods.
- Compare additional reinforcement learning algorithms after validating the environment.
- Evaluate the learned policies using realistic simulations and appropriate baselines.
- Investigate how policy performance changes with different reward functions and state discretization strategies.

## ▶️ How to Run the Project

### Option 1: Google Colab

1. Open the notebook in this repository.
2. Click **Open in Colab** if available, or download the notebook and upload it to Google Colab.
3. Obtain the dataset from its original source.
4. Update the dataset file path in the notebook if necessary.
5. Run the notebook cells in order.
6. Review the preprocessing outputs, visualizations, training results, and comparison tables.

### Option 2: Jupyter Notebook

1. Clone or download this repository.
2. Install Python and Jupyter Notebook.
3. Install the libraries imported by the notebook.
4. Download the dataset from its verified source.
5. Update the dataset path in the notebook.
6. Execute the cells sequentially.

Example commands:

```bash
git clone https://github.com/sanjayshrinivas07-blip/Energy-consumption-management-using-Q-learning-and-SARSA.git

cd Energy-consumption-management-using-Q-learning-and-SARSA

pip install jupyter numpy pandas matplotlib seaborn scikit-learn

jupyter notebook
```

Install any additional dependencies imported by the notebook. The dataset must be obtained separately unless you have permission to redistribute it.

## 📚 Concepts Demonstrated

- Reinforcement Learning
- Q-Learning and SARSA
- State and action representation
- Reward function design
- Q-table updates
- Data cleaning and preprocessing
- Chronological train-test splitting
- Exploratory Data Analysis
- Algorithm comparison
- Reproducibility across random seeds
- Critical evaluation of experimental limitations

## 👨‍💻 Author

**Sanjay Shrinivas**

M.Sc. Data Science Student

GitHub: [sanjayshrinivas07-blip](https://github.com/sanjayshrinivas07-blip)

## 📄 Academic Disclaimer

This repository is an academic case study developed for learning and comparing reinforcement learning algorithms. The results are specific to the implemented experimental setup. They should not be interpreted as evidence of actual electricity savings or as a production-ready energy management controller.

## 📜 License

No open-source licence has been specified for this repository yet. Unless a licence is added, the code should not be assumed to be available for unrestricted reuse. Add an appropriate licence only after confirming that you have the right to license all included material.
