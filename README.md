# FIFA World Cup Prediction & Tournament Simulation

A machine learning project for predicting international football match outcomes and estimating FIFA World Cup tournament probabilities through Monte Carlo simulation.

## Project Overview

This project combines historical international football results, team strength, recent performance, head-to-head history, and machine learning to estimate the probabilities of:

- Home win
- Draw
- Away win

The trained model is then used as the probability engine for simulating the 2026 FIFA World Cup thousands of times.

## Project Pipeline

Historical Match Data
        ↓
Data Cleaning & EDA
        ↓
Target Creation
        ↓
Elo Rating
        ↓
Recent Form
        ↓
Recent Scoring & Goal Difference
        ↓
Head-to-Head Features
        ↓
Feature Engineering
        ↓
Chronological Train / Calibration / Test Split
        ↓
Model Comparison
        ↓
Probability Calibration
        ↓
Backtesting & Final Evaluation
        ↓
2026 World Cup Match Probabilities
        ↓
Group Stage Simulation
        ↓
Knockout Stage Simulation
        ↓
10,000 Monte Carlo Simulations
        ↓
Tournament & Champion Probabilities

## Dataset

The project uses the International football results dataset containing historical international matches.

Important fields include:

- Date
- Home team
- Away team
- Home score
- Away score
- Tournament
- City
- Country
- Neutral venue indicator

Historical matches are used to calculate team strength and pre-match features.

## Feature Engineering

The model uses pre-match features designed to represent team strength and recent performance.

### Elo Rating

Elo ratings estimate the relative strength of teams based on historical results.

The implementation includes:

- Initial rating
- Home advantage
- Match outcome
- Margin of victory adjustment

### Recent Form

The last five matches are used to calculate recent form.

- Win = 1
- Draw = 0.5
- Loss = 0

### Recent Performance

Additional rolling features include:

- Goals scored
- Goals conceded
- Recent goal difference

### Head-to-Head

Recent meetings between the two teams are used to calculate a head-to-head performance signal.

### Engineered Features

The final feature set includes:

- Elo difference
- Expected home probability from Elo
- Form difference
- H2H difference
- Goals scored difference
- Goals conceded difference
- Recent goal difference
- Elo ratio
- Neutral venue
- Home advantage
- World Cup indicator

## Model Development

Three classification approaches were evaluated:

- Logistic Regression
- Random Forest
- XGBoost

The models were evaluated using a chronological split rather than a random split to better reflect real-world prediction, where future matches must not influence past predictions.

## Probability Calibration

Because the project is used for tournament simulation, probability quality is important.

The final Random Forest model was calibrated using a separate calibration period.

Evaluation includes:

- Accuracy
- Balanced Accuracy
- Macro F1
- Log Loss
- Brier Score

## Backtesting

The prediction pipeline was also evaluated using multiple historical time windows to examine how the approach performs across different periods.

## Final Model

The final tournament simulation uses the engineered calibrated Random Forest because its probability metrics were slightly better than the alternatives evaluated.

The model produces probabilities for:

- AWAY_WIN
- DRAW
- HOME_WIN

These probabilities are used as inputs to the tournament simulator.

## 2026 World Cup Simulation

The 2026 tournament is represented using:

- 12 groups
- 48 teams
- 72 group-stage matches per tournament

Each match is simulated using the model's predicted outcome probabilities.

Group standings are calculated using:

- Points
- Goals scored
- Goals conceded
- Goal difference

The knockout stages are then simulated through:

- Round of 32
- Round of 16
- Quarter-finals
- Semi-finals
- Final

## Monte Carlo Simulation

The tournament was simulated 10,000 times.

For every simulated tournament, the system records:

- Teams reaching each knockout stage
- Finalists
- Tournament champion

The resulting frequencies are converted into probabilities.

The final champion probabilities therefore represent the estimated probability of each team winning the simulated tournament under the project's model assumptions.

## Results

The `results/` directory contains:

- Final model evaluation metrics
- Final test predictions
- Final test probability estimates
- Monte Carlo raw simulation counts
- Monte Carlo tournament probabilities
- Champion probability visualization
- Tournament stage probability visualization

### Top Champion Probabilities

| Team | Champion Probability |
|---|---:|
| Argentina | 15.81% |
| Spain | 14.06% |
| Brazil | 9.90% |
| France | 8.44% |
| England | 5.66% |
| Portugal | 5.30% |
| Germany | 4.78% |
| Netherlands | 4.36% |
| Colombia | 4.03% |
| Japan | 3.52% |

These are simulation-based probabilities, not guarantees of the actual tournament outcome.

## Technologies

- Python
- Pandas
- NumPy
- Scikit-learn
- XGBoost
- Matplotlib
- Joblib
- Google Colab

## Limitations

This project is a probabilistic simulation and not a guarantee of real-world tournament outcomes.

The tournament simulation includes simplifying assumptions, including:

- A simplified knockout bracket mapping
- Poisson-based score generation
- A simplified penalty-shootout mechanism for drawn knockout matches

The model also depends on the historical data and features available at the time of training.

## Future Improvements

Possible extensions include:

- Exact FIFA knockout bracket mapping
- More advanced score modelling
- Player-level features
- Squad availability and injuries
- FIFA ranking integration
- Tournament-specific home/venue effects
- Live pre-tournament team updates
- Bayesian or neural probabilistic models

## Repository Structure

```text
FIFA-World-Cup-Prediction/
│
├── results/
│   ├── final_model_metrics.csv
│   ├── final_test_predictions.csv
│   ├── final_test_probabilities.csv
│   ├── monte_carlo_raw_counts.csv
│   ├── monte_carlo_tournament_probabilities.csv
│   ├── top10_champion_probability.png
│   └── tournament_stage_probabilities.png
│
├── FIFA_World_Cup_Prediction.ipynb
└── README.md
