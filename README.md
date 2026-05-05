# DSA210 Project – Exploring the Impact of Coffee Consumption on Sleep and Lifestyle Factors

Author: Sera Sinem Baygan  
Course: DSA210 – Introduction to Data Science  
Semester: Spring 2026

---

## 📌 Project Overview

This project investigates the relationship between **coffee consumption** and lifestyle factors such as sleep duration, stress level, and screen time — using self-collected survey data, statistical hypothesis testing, and supervised machine learning.

---

## 📊 Data Collection

This project uses a self-collected dataset gathered through a structured Google Forms survey.

| | |
|---|---|
| 👥 Participants | 106 individuals |
| 🛠️ Method | Google Forms survey (all questions mandatory) |
| 📅 Collection Period | April 2026 |
| 🌍 Target Group | University students / general population |

**Variables collected:**

| Variable | Type | Description |
|---|---|---|
| `coffee` | Numerical | Cups of coffee per day (0–5) |
| `coffee_type` | Categorical | Type of coffee preferred |
| `sleep_hours` | Numerical | Hours of sleep per night |
| `sleep_quality` | Ordinal (1–5) | Self-reported sleep quality |
| `stress` | Ordinal (1–5) | Self-reported stress level |
| `screen_time` | Numerical | Hours of screen time before sleep |
| `exercise` | Categorical | Whether the participant exercises regularly |
| `age` | Numerical | Age of participant |
| `gender` | Categorical | Gender of participant |

🔗 Survey: https://docs.google.com/forms/d/e/1FAIpQLSc1MBsBbvjHbgN6CS08nhs_ZWxy2Chg-ULy-O1x_lVijnyjow/viewform?usp=publish-editor

### Data Quality Note
The survey required all questions to be answered, including `coffee_type`. Respondents who drink 0 cups/day were still forced to select a coffee type. These entries were corrected in preprocessing: all rows with `coffee = 0` have `coffee_type` set to `"Non-drinker"`.

---

## 🧪 Methodology

### Milestone 1 — EDA & Hypothesis Testing (`EDA.ipynb`)

**Exploratory Data Analysis:**
- Distribution analysis for all numerical and categorical variables
- Correlation matrix and heatmap (Pearson)
- Bivariate visualizations: scatter plots, box plots, group comparisons

**Hypothesis Testing** (significance level α = 0.05):

| # | Hypothesis | Test Used | Result |
|---|---|---|---|
| H1 | Coffee → Sleep Hours | Pearson correlation | ✅ Significant (r ≈ -0.24, p = 0.013) |
| H2 | Coffee → Stress | Spearman correlation | ❌ Not significant |
| H3 | Exercise → Sleep Hours | Mann-Whitney U | ❌ Not significant |
| H4 | Screen Time → Stress | Spearman correlation | ✅ Significant (ρ > 0, p < 0.05) |

### Milestone 2 — Machine Learning (`ML.ipynb`)

The two statistically significant findings (H1 and H4) were formalized as supervised regression problems.

**Model 1 — Predicting Sleep Hours (H1)**
- Target: `sleep_hours`
- Features: `coffee`, `stress`, `screen_time`, `age`
- Models: Linear Regression, Decision Tree Regressor
- Evaluation: R², RMSE, 5-fold cross-validation

**Model 2 — Predicting Stress Level (H4)**
- Target: `stress`
- Features: `screen_time`, `coffee`, `age`
- Models: Linear Regression, Decision Tree Regressor
- Evaluation: R², RMSE, 5-fold cross-validation

**Model selection rationale:** Linear Regression was chosen as the primary model due to interpretability and small sample size. Decision Tree was included as a comparison. Since neither model significantly outperformed the other, Linear Regression was retained as the main model.

---

## 📈 Key Findings

### EDA & Hypothesis Testing
- **Coffee → Sleep Hours:** Statistically significant negative correlation (r ≈ -0.24, p = 0.013). Higher coffee intake is associated with fewer hours of sleep.
- **Screen Time → Stress:** Statistically significant positive relationship. More screen time before sleep is associated with higher stress.
- **Coffee → Stress:** No significant relationship found.
- **Exercise → Sleep Hours:** No significant difference between groups.

### Machine Learning
- The `coffee` coefficient is **negative** in Model 1 → consistent with H1.
- The `screen_time` coefficient is **positive** in Model 2 → consistent with H4.
- Both models return a **low or negative R²**, meaning they do not predict the target better than simply guessing the mean. This is expected given the small sample size (n=106) and the self-reported nature of the data. It does not invalidate the EDA findings — a statistically significant correlation does not guarantee high R².
- Decision Tree did not outperform Linear Regression, confirming that the low predictive power is a data limitation, not a model problem.

---

## 📁 Repository Structure

```
├── EDA.ipynb                  # Milestone 1: Data cleaning, EDA, hypothesis testing
├── ML.ipynb                   # Milestone 2: Machine learning models and comparison
├── DSA210 (Responses).xlsx    # Raw survey data
└── README.md                  # Project documentation
```

---

## ⚠️ Limitations

- **Small sample size** (n=106): limits generalizability and model stability
- **Self-reported data**: subject to recall bias
- **Survey design**: all questions were mandatory, leading to forced responses (corrected in preprocessing)
- **Correlation ≠ causation**: associations found do not imply causal relationships
- **Sample bias**: participants are predominantly young university students

---

## 🔮 Future Work

- Collect more data (n > 500) for more stable ML models
- Add features: sleep environment, caffeine timing, medication, work hours
- Try non-linear and ensemble models (Random Forest, kNN) with larger data
- Use objective measurements instead of self-reported data
