# DSA210 Project – Exploring the Impact of Coffee Consumption on Sleep and Lifestyle Factors

Author: Sera Sinem Baygan  
Course: DSA210 – Introduction to Data Science  
Semester: Spring 2026

---

## 📌 Project Overview

This project investigates the relationship between **coffee consumption** and lifestyle factors such as sleep duration, stress level, and screen time — using self-collected survey data, statistical hypothesis testing, and supervised machine learning.

---

## 📊 Data Collection

| | |
|---|---|
| 👥 Participants | 106 individuals |
| 🛠️ Method | Google Forms survey (all questions mandatory) |
| 📅 Collection Period | April 2026 |
| 🌍 Target Group | Primarily university students and young adults |

**Variables collected:**

| Variable | Type | Description |
|---|---|---|
| `coffee` | Numerical | Cups of coffee per day (0–5) |
| `coffee_type` | Categorical | Type of coffee preferred |
| `sleep_hours` | Numerical | Hours of sleep per night |
| `sleep_quality` | Ordinal (1–5) | Self-reported sleep quality |
| `stress` | Ordinal (1–5) | Self-reported stress level |
| `screen_time` | Numerical | Screen time before sleep (hours) |
| `exercise` | Categorical | Exercises regularly? (Yes/No) |
| `age` | Numerical | Age of participant |
| `gender` | Categorical | Gender of participant |

🔗 Survey: https://docs.google.com/forms/d/e/1FAIpQLSc1MBsBbvjHbgN6CS08nhs_ZWxy2Chg-ULy-O1x_lVijnyjow/viewform?usp=publish-editor

**Data Quality Note:** The survey required all questions to be answered, including `coffee_type`. Respondents who drink 0 cups/day were still forced to select a coffee type. These entries were corrected in preprocessing: all rows with `coffee = 0` have `coffee_type` set to `"Non-drinker"`. Email addresses collected during the response phase to prevent duplicate submissions were removed before analysis. The final dataset is fully anonymized.

---

## 🧪 Methodology

### Milestone 1 — EDA & Hypothesis Testing (`EDA.ipynb`)

**Exploratory Data Analysis:**
- Distribution analysis for all numerical and categorical variables
- Pearson correlation matrix and heatmap
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
- Models: Dummy (baseline), Linear Regression, Ridge (α=1), KNN (k=5), Decision Tree (d=3)
- Evaluation: R², RMSE, 5-fold cross-validation

**Model 2 — Predicting Stress Level (H4)**
- Target: `stress`
- Features: `screen_time`, `coffee`, `age`
- Models: Dummy (baseline), Linear Regression, Ridge (α=1), KNN (k=5), Decision Tree (d=3)
- Evaluation: R², RMSE, 5-fold cross-validation

**Model selection rationale:** Linear Regression was chosen as the primary model due to interpretability and suitability for small datasets. A Dummy Regressor (predicts the mean) was included as the true baseline. Since no model consistently outperformed the Dummy baseline, the weak predictive performance is attributed to insufficient feature informativeness rather than model choice — a finding that reflects the limitations of the survey design.

---

## 📈 Key Findings

### EDA & Hypothesis Testing
- **Coffee → Sleep Hours:** Significant negative correlation (r ≈ -0.24, p = 0.013). Higher coffee intake is associated with fewer hours of sleep.
- **Screen Time → Stress:** Significant positive relationship (ρ > 0, p < 0.05). More screen time before sleep is associated with higher stress.
- **Coffee → Stress:** No significant relationship found.
- **Exercise → Sleep Hours:** No significant difference between groups.

### Machine Learning
- The `coffee` coefficient is **negative** in Model 1 → consistent with H1.
- The `screen_time` coefficient is **positive** in Model 2 (β = +0.369) → consistent with H4.
- All models — including Ridge, KNN, and Decision Tree — fail to outperform the Dummy Regressor. This confirms that the issue is not model complexity but **feature informativeness**: the survey did not capture enough predictive signal for sleep hours or stress.
- The survey was intentionally kept short to maximize participation, but this reduced feature depth. Key predictors such as caffeine timing, academic workload, and sleep environment were not collected.

---

## 📁 Repository Structure

```
├── EDA.ipynb                              # Milestone 1: Data cleaning, EDA, hypothesis testing
├── ML.ipynb                               # Milestone 2: Machine learning models and comparison
├── Final_Report.pdf                       # Milestone 3: Final report  
├── DSA210 (Responses).xlsx                # Raw survey data
├── DSA210 Project Proposal.pdf            # Initial project proposal
├── requirements.txt                       # Python dependencies
├── README.md                              # Project documentation
├── eda_fig1_distributions_numerical.png
├── eda_fig2_distributions_categorical.png
├── eda_fig3_boxplots.png
├── eda_fig4_coffee_vs_variables.png
├── eda_fig5_group_comparisons.png
├── eda_fig6_correlation_heatmap.png
├── eda_fig7_h1_coffee_sleep.png
├── eda_fig8_h4_screen_stress.png
├── ml_fig1_model1_diagnostics.png
├── ml_fig2_simple_regression.png
├── ml_fig3_model2_diagnostics.png
├── ml_fig4_decision_tree_structure.png
├── ml_fig5_model_comparison.png
└── ml_fig6_model_comparison_extended.png
```

---

## ▶️ How to Run

```bash
# Install dependencies
pip install -r requirements.txt

# Run notebooks in order
jupyter notebook EDA.ipynb   # Milestone 1
jupyter notebook ML.ipynb    # Milestone 2
```

Place `DSA210 (Responses).xlsx` in the same directory as the notebooks before running.

---

## ⚠️ Limitations

- **Small sample size** (n=106): limits generalizability and model stability
- **Self-reported data**: subject to recall bias and social desirability effects
- **Survey design**: kept intentionally short to maximize participation, reducing feature depth
- **Missing predictors**: caffeine timing, sleep environment, academic workload, and stress causes were not collected
- **Sample bias**: participants are predominantly young university students
- **Correlation ≠ causation**: associations found do not imply causal relationships

---

## 🔮 Future Work

- Collect more data (n > 500) for stable machine learning models
- Add features: caffeine timing, sleep environment, medication, work and study hours
- Use objective measurements (actigraphy, wearables) instead of self-reported data
- Explore ensemble models (Random Forest, XGBoost) and kNN with a larger dataset
- Apply time-series analysis if longitudinal data becomes available

---

## 🤖 AI Usage Disclosure

Claude AI and ChatGPT were occasionally used during this project for debugging Python code, improving markdown formatting, refining report language, and receiving feedback on data analysis workflows. All preprocessing steps, hypothesis formulations, model selections, interpretations, and conclusions were independently designed, implemented, and verified by the author. AI tools were used only to support productivity and editing, not to replace analytical understanding or decision-making.
