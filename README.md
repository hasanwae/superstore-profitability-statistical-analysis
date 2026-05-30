# SuperStore Profitability & Discount Analysis (ANOVA & Post-Hoc)

## 📌 Project Overview
This project performs a rigorous statistical analysis on **51,000+ rows** of retail data to investigate the impact of different discount levels on overall product profitability. The analysis transitions from visual exploratory data analysis (EDA) to formal hypothesis testing to provide actionable business recommendations.

## 📊 Methodology & Workflow

### 1. Data Cleaning & Feature Engineering
* Handled missing/bad rows during the parsing stage using specialized encoding (`latin1`) and robust line tokenization handlers (`on_bad_lines='skip'`).
* Cleaned hidden whitespaces from column names to ensure stable indexing.
* Engineered a categorical feature named `Discount_Group` based on business thresholds:
  * **No Discount:** Exactly 0% discount.
  * **Low Discount:** Promotions up to 20% (0% < Discount <= 20%).
  * **High Discount:** Aggressive promotions exceeding 20% (Discount > 20%).

### 2. Exploratory Data Analysis (EDA)
* Implemented a **Box Plot** visualization using `seaborn` and `matplotlib` to inspect the distribution of `Profit` across the newly created discount groups.
* **Visual Observation:** Detected significant variance, severe dispersion, and dense clusters of extreme values (**Outliers**) across all groups. The "High Discount" group visually showed a massive shift below the zero-profit line, indicating systemic losses.

### 3. Hypothesis Testing (One-Way ANOVA)
To scientifically validate if the visual differences in profit averages across the three discount groups were statistically significant or merely due to random chance, a **One-Way ANOVA** test was conducted:
* **Null Hypothesis ($H_0$):** $\mu_{\text{No Discount}} = \mu_{\text{Low Discount}} = \mu_{\text{High Discount}}$ (Discounts have no impact on profit means).
* **Alternative Hypothesis ($H_1$):** At least one discount group has a significantly different profit mean.

### 4. Post-Hoc Analysis (Tukey's HSD)
Since the ANOVA test confirmed a significant difference, **Tukey's Honestly Significant Difference (HSD)** test was applied to perform pairwise comparisons and isolate which exact strategies drive or destroy value.

---

## 🔑 Key Findings & Statistical Results

### 📉 1. One-Way ANOVA Test Result
* **F-Statistic:** `2701.33`
* **P-Value:** `0.0`
* **Conclusion:** Since the $P\text{-value} < 0.05$, we **reject the null hypothesis ($H_0$)** with 95% confidence. There is an overwhelmingly strong, statistically proven impact of discount strategies on corporate profitability.

### 🔍 2. Tukey's HSD Pairwise Comparison Result
The multiple comparisons matrix yielded the following insights (all comparisons rejected the null hypothesis with `reject = True`):

| Group 1 (Comparison) | Group 2 (Comparison) | Mean Difference (`meandiff`) | Reject $H_0$ | Business Interpretation |
| :--- | :--- | :---: | :---: | :--- |
| **High Discount** | **Low Discount** | `+118.61` | **True** | Low discount strategies outperform high discounts by an average of 118 units per transaction. |
| **High Discount** | **No Discount** | `+132.96` | **True** | Selling at full price yields the highest recovery, beating aggressive discounts by ~133 units on average. |
| **Low Discount** | **No Discount** | `+14.35` | **True** | Even mild promotions (under 20%) cause a statistically significant drop in average profit compared to no discounts. |

---

## 💡 Strategic Business Recommendations

1. **Immediate Elimination of High Discounts:** Aggressive promotional discounting (>20%) is mathematically proven to destroy value in this ecosystem. It does not drive profitable volume; instead, it deepens transactional losses.
2. **Strict Promotion Thresholds:** If discounts are necessary for customer acquisition or inventory clearance, they must be strictly capped at a maximum of **20% (Low Discount Group)**, as it preserves a healthier bottom line compared to deeper cuts.
3. **Optimize Full-Price Sales:** Prioritize marketing and sales pipelines toward the `No Discount` model, which represents the optimal baseline for maximizing total profitability.

---

## 🛠️ Tech Stack & Libraries Used
* **Language:** Python 3.12 (Google Colab Environment)
* **Data Manipulation:** `pandas`, `numpy`
* **Data Visualization:** `seaborn`, `matplotlib`
* **Statistical Modeling:** `scipy.stats` (ANOVA), `statsmodels.stats.multicomp` (Tukey HSD)

## 📂 Project Structure
* `superstore_statistical_analysis.ipynb` -> The complete Python notebook containing data loading, cleaning, plotting, and statistical testing.
* `SuperStore_Cleaned_with_Groups.csv` -> The finalized, cleaned dataset containing the engineered statistical groups.
* `README.md` -> Portfolio documentation and executive summary.
