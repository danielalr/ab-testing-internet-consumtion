# ab-testing-internet-consumtion
## Introduction
This project analyzes the results of an A/B test to evaluate the performance of two website versions (Group A as control and Group B as treatment). The goal is to determine whether the new version (Group B) improves user conversions, engagement, and revenue compared to the existing version.

## Data
The dataset used in this project is ab_test_data.csv and contains 2,000 user observations with the following fields:

- user_id: Unique identifier for each user.
- group: Experimental group assignment.
- time_on_page_seconds: Time (in seconds) each user spent on the webpage.
- converted: Whether the user converted.
- revenue: Revenue generated per user.

## Quick Statistics:

- Users are almost evenly split: ~1,016 in group A and ~984 in group B.
- Average time on page: ~82.6 seconds (with wide variation).
- Average conversion rate: ~13.5%.
- Average revenue per user: ~6.85 units (mostly concentrated among converters).

## Methodology

- Several statistical tests and analyses were conducted to assess the experiment results:
- Exploratory Data Analysis (EDA):
- Distribution of users across groups.
- Conversion rate by group.
- Time on page comparison (boxplots and barplots).

Hypothesis Testing:

Proportion Z-Test: Compared conversion rates between Group A and Group B.

Two-Sample T-Test: Tested whether average revenue per user differs between groups.

Example code for the Z-Test and ROI calculation:

```py
import pandas as pd
from statsmodels.stats.proportion import proportions_ztest

# Load dataset
df = pd.read_csv("ab_test_data.csv")

# Split groups
conv_A = df[df["group"] == "A"]["converted"]
conv_B = df[df["group"] == "B"]["converted"]

# Run a proportions z-test
successes = [conv_A.sum(), conv_B.sum()]
samples = [len(conv_A), len(conv_B)]
z, p = proportions_ztest(successes, samples)

print(f"Z = {z:.2f}, p-value = {p:.4f}")

# ROI calculation
conversion_value = 50
implementation_cost = 2000

revenue_A = conv_A.sum() * conversion_value
revenue_B = conv_B.sum() * conversion_value

roi = (revenue_B - revenue_A - implementation_cost) / implementation_cost
print(f"ROI of implementing Group B: {roi:.2%}")
```


Business Impact Analysis:

Calculated additional revenue from conversions in Group B compared to Group A.

Estimated ROI (Return on Investment) by considering the implementation cost of the new version.

## Results

- Conversion Rate: Statistical testing determined whether the difference in conversion rates between groups is significant.
- Revenue Comparison: The t-test provided insights into whether revenue per converted user significantly differs between A and B.
- ROI: The return on investment of implementing Group B over Group A was computed to support the business decision.

## Conclusion

The experiment combined statistical evidence with business impact analysis.
Based on the test results:

If the p-values < 0.05, the differences are statistically significant.

If ROI is positive, adopting Group B leads to higher profitability despite implementation costs.

This project demonstrates how data-driven decisions can be made by integrating statistical testing with business KPIs.
