
## 📊 Dataset

The analysis uses the **Telco Customer Churn** dataset (7,043 customers), which includes demographic details (gender, senior citizen status, partner/dependents), account information (tenure, contract type, payment method, billing), subscribed services (phone, internet, streaming, security add-ons), and the churn label.

## 🔍 Project Workflow

1. **Data Pre-Processing** — inspected data structure, handled encoding of binary and categorical columns.
2. **Exploratory Data Analysis**
   - Univariate analysis of numeric features (tenure, monthly charges, total charges), including normality checks via histograms, boxplots, and Q-Q plots.
   - Distribution analysis of phone, internet, and add-on services.
   - Bivariate/multivariate analysis of churn rate across customer segments.
3. **Hypothesis Testing**
   - **Chi-square test**: confirmed a statistically significant association between contract type and churn (χ²(2) = 1184.60, p < 0.001, Cramér's V = 0.41 — moderate association).
   - **Shapiro-Wilk & Levene's tests**: confirmed monthly/total charges are non-normally distributed with unequal variances across churn groups.
   - **Mann-Whitney U test**: found a statistically significant difference in monthly and total charges between churned and retained customers (p < 0.001).
   - **Chi-square test**: found a statistically significant, moderate association between combined internet service/payment method categories and churn.
4. **Logistic Regression Model**
   - Modeled churn as a function of tenure, monthly/total charges, contract type, payment method, internet service, and demographic variables.
   - Checked multicollinearity via VIF and removed `TotalCharges` (VIF ≈ 16, redundant with tenure and monthly charges) to arrive at a final, more stable model.

## 📈 Key Findings

Based on the final logistic regression model (odds ratios, holding other variables constant):

| Factor | Odds Ratio | Effect on Churn |
|---|---|---|
| Fiber optic internet | 2.44 | Increases odds of churn |
| Electronic check payment | 1.53 | Increases odds of churn |
| Senior citizen | 1.36 | Increases odds of churn |
| Two-year contract | 0.22 | Strongly reduces odds of churn |
| One-year contract | 0.47 | Reduces odds of churn |
| No internet service | 0.46 | Reduces odds of churn |
| Longer tenure | 0.97 per month | Reduces odds of churn |
| Having dependents | 0.81 | Reduces odds of churn |

**Takeaways:**
- **Contract length is the strongest retention lever** — customers on month-to-month contracts are far more likely to churn than those on one- or two-year contracts.
- **Fiber optic internet customers churn more**, despite (or perhaps because of) being a premium service tier — worth investigating pricing or service-quality drivers.
- **Electronic check payers churn more** than customers using automatic payment methods, suggesting friction or lower commitment in that group.
- **Tenure and having dependents are protective** — longer-standing customers and those with dependents are less likely to leave.
- Gender, partner status, and monthly charges (once controlling for other variables) were **not** statistically significant predictors of churn.

## 🛠️ Tools & Libraries

- **Python**: pandas, numpy
- **Visualization**: seaborn, matplotlib
- **Statistics**: scipy, statsmodels (logistic regression, VIF)

## 🚀 Getting Started

```bash
git clone https://github.com/miriammwongela1/Customer-Churn-Analysis-Prediction.git
cd Customer-Churn-Analysis-Prediction
pip install pandas numpy seaborn matplotlib scipy statsmodels
jupyter notebook notebook/customer_churn_analysis.ipynb
```

## 📑 Presentation

See the `presentation/` folder for a slide deck summarizing the methodology and key findings for a non-technical audience.

## 💡 Business Recommendations

- Incentivize migration from month-to-month to longer-term contracts (e.g., discounts for annual commitment).
- Investigate fiber optic customer experience — pricing, reliability, or support issues may be driving churn.
- Encourage automatic payment methods over electronic check to reduce churn risk.
- Prioritize retention outreach for newer, high-monthly-charge, month-to-month customers, who represent the highest-risk segment.
