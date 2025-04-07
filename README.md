# 🏀 March Mania 2025 – Baseline Seed-Based Predictor

This project provides a simple seed-based model for predicting NCAA tournament matchups in the [March Machine Learning Mania 2025](https://www.kaggle.com/competitions/march-machine-learning-mania-2025/data) competition on Kaggle. It uses historical seed rankings to estimate the likelihood of one team beating another.

---

## 🎯 Objective

Given a matchup between two teams in a specific year, the goal is to predict the probability that the **first-listed team** (TeamID1) will win.

Each row in the dataset includes a matchup identifier in the format:

<YEAR><TEAMID1><TEAMID2>


### Example

For the matchup ID `2023_1218_1342`:
- **Year**: 2023  
- **Teams**: Team 1218 vs Team 1342  
- A prediction of `0.68` implies a 68% probability that **Team 1218** wins.

---

## 🧠 Approach

This baseline model uses **seed difference as a proxy for team strength**. It assumes that teams with better (lower) seeds are more likely to win. The prediction formula is:

**Predicted Probability = 0.5 + 0.03 × (Seed2 - Seed1)**

- If TeamID1 is seeded better than TeamID2 → prediction > 0.5  
- If TeamID2 is seeded better → prediction < 0.5  
- Probabilities are bounded between 0.05 and 0.95 for stability.

---

## ⚙️ Key Features

- **Seed Extraction via Regex**: Parses raw seed strings (e.g. `'W05'`, `'X12'`) to get numeric values.
- **Robust Merging**: Joins seed data from both men’s and women’s tournaments to every matchup.
- **Fallback Handling**: Defaults missing seeds to 16, the lowest possible rank.
- **Clipped Predictions**: Ensures predictions are never too extreme.

---

## 📊 Evaluation

Though the true outcomes are not known at prediction time, we simulate evaluation using the **Brier Score**. This helps estimate how confident and well-calibrated the predictions are.

**Brier Score = (1/N) × Σ (pᵢ - yᵢ)²**

Where:
- `pᵢ` = predicted probability
- `yᵢ` = actual outcome (1 if TeamID1 wins, 0 if not)
- `N` = number of matchups

A lower score indicates better predictive performance.

---

## 📁 Files Included

- `march_mania_2025_baseline.ipynb` – the full notebook with comments
- `submission.csv` – output file formatted for Kaggle submission
- Code relies on datasets found [here](https://www.kaggle.com/competitions/march-machine-learning-mania-2025/data)

---

## 🚧 Limitations & Improvements

This is a **naive baseline** that only uses seed rankings. It does not incorporate:

- Win/loss history
- Team statistics (offense, defense, player ratings)
- Matchup-specific context or momentum

Future enhancements could include:
- Incorporating advanced team metrics
- Training a logistic regression or gradient boosting model
- Using prior tournament performance as additional features

---

## 💬 License & Acknowledgments

Built for learning and experimentation.  
Seed data courtesy of Kaggle's March Mania 2025 competition.
