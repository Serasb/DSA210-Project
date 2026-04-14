# DSA210 Project – Exploring the Impact of Coffee Consumption on Sleep and Lifestyle Factors

Author: Sera Sinem Baygan  
Course: DSA210 – Introduction to Data Science  
Semester: Spring 2026

## 📌Project Overview
This project explores the relationship between coffee consumption, sleep quality, stress levels and lifestyle factors using data analysis and machine learning techniques.

## 📊 Data Collection

This project uses a self-collected dataset gathered through a structured survey.

👥 Participants: 100+ individuals  
🛠️ Method: Google Forms survey  
📅 Collection Period: April 2026  
🌍 Target Group: University students / general population 

The dataset includes variables such as:

- Coffee consumption (cups per day)
- Sleep duration and quality
- Stress levels (ordinal scale)
- Screen time before sleep
- Exercise habits

This original dataset allows for a more customized and relevant analysis, rather than relying solely on publicly available data.

🔗 Survey Link:
https://docs.google.com/forms/d/e/1FAIpQLSc1MBsBbvjHbgN6CS08nhs_ZWxy2Chg-ULy-O1x_lVijnyjow/viewform?usp=publish-editor

### 📈 Dataset Improvement

The original proposal aimed to collect data from 20–30 participants. However, the final dataset includes over 100 responses, significantly enhancing the quality of the analysis.

This improvement allows for:
- More reliable statistical insights  
- Better generalization of findings  
- Stronger exploratory data analysis (EDA)

## 🧪 Methodology

The analysis includes:

- Exploratory Data Analysis (EDA)  
- Correlation analysis:  
  - Pearson correlation (numerical variables)
  - Spearman correlation (ordinal variables)

- Hypothesis testing:
  - H1: Coffee vs Sleep Hours (Pearson)
  - H2: Coffee vs Stress (Spearman)
  - H3: Exercise vs Sleep Hours (Mann-Whitney U)
  - H4: Screen Time vs Stress (Correlation analysis)

Significance level: α = 0.05

## 📈 Key Findings

- Coffee consumption is **negatively correlated** with sleep duration  
  *(r ≈ -0.24, p < 0.05)*  
  → Higher coffee intake is associated with less sleep  

- No statistically significant relationship was found between coffee consumption and stress  

- No significant difference in sleep duration between individuals who exercise and those who do not  

- Screen time and stress show a **weak positive relationship**  
  *(r ≈ 0.24)*  
  → Higher screen time may be associated with increased stress  
