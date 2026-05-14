# A/B Testing Analysis of Digital Campaigns: Evaluating Conversion Rates and Business Impact

## Overview
Statistical analysis of a 588K-user marketing campaign comparing ad vs. PSA conversion
rates using hypothesis testing and confidence intervals. This project demonstrates
end-to-end A/B test analysis including pre-analysis sample size validation, a
two-proportion z-test, and confidence interval estimation.

---

## Dataset
- **Source:** [Marketing A/B Testing — Kaggle (FavioVázquez)](https://www.kaggle.com/datasets/faviovaz/marketing-ab-testing)
- **License:** CC0 Public Domain
- **Size:** ~588,000 user records
- **Features:**
  - `test group` — whether the user saw an ad or a public service announcement (PSA)
  - `converted` — whether the user made a purchase
  - `total ads` — number of ads seen
  - `most ads day` — day with the highest ad exposure
  - `most ads hour` — hour with the highest ad exposure

---

## Objectives
1. Validate that sufficient sample sizes exist in both groups before drawing conclusions
2. Compare conversion rates between the ad group (treatment) and PSA group (control)
3. Determine whether any observed difference is statistically significant
4. Quantify the business impact of the difference using confidence intervals

---

## Requirements
```
pip install pandas numpy statsmodels jupyter
```

## Project Structure
```
├── 📁 data
│
│   ├── 🐍 data.py
│   └── 📄 marketing_AB.csv
├── 📄 AB_Testing.ipynb
├── 📝 README.md
└── 📄 requirements.txt
```

---

## Methodology

### 1. Data Cleaning and Preparation
- Loaded the dataset and stripped whitespace from column names
- Encoded `test group` as a binary `ad` column (1 = ad, 0 = PSA)
- Checked for missing values and group imbalance
- Found a heavily imbalanced split: ~96% ad group, ~4% PSA group

### 2. Sample Size Validation
Before analyzing results, the required sample size was calculated as if designing
the experiment from scratch using a two-proportion z-test power analysis:
- **Significance level:** α = 0.05 (95% confidence)
- **Statistical power:** 80%
- **Group ratio:** r = n_PSA / n_ad ≈ 0.0417 (unequal group design)
- **Effect size:** Standardized difference relative to the control group standard deviation

Both the individual group sizes and the combined total exceeded the required
minimums, confirming the dataset is statistically sufficient.

### 3. Two-Proportion Z-Test
- **Null hypothesis (H₀):** Conversion rates are equal between the ad and PSA groups
- **Alternative hypothesis (H₁):** Conversion rates differ between the two groups
- Performed using `statsmodels.stats.proportion.proportions_ztest`

### 4. Confidence Interval Analysis
Calculated a 95% confidence interval for the difference in conversion rates
between the ad and PSA groups using the standard error of two proportions.

---

## Key Findings
- The ad group conversion rate was higher than the PSA group by approximately **0.7%**
- The p-value was below 0.05, leading to **rejection of the null hypothesis**
- The 95% confidence interval did **not include 0**, confirming the difference
  is statistically significant and unlikely due to random chance
- Given the scale of the campaign (~564K users in the ad group), even a small
  lift in conversion rate represents a meaningful business opportunity

---

## How to Run
1. Clone the repo
2. Place `marketing_AB.csv` inside the `data/` folder
3. Open `ab_testing_analysis.ipynb` in Jupyter or VS Code
4. Run all cells in order

---

## Author
Aaron Villegas — [GitHub](https://github.com/AaronVillegas5)