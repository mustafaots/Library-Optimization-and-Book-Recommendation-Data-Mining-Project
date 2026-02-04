# Library Borrowing Behavior Analysis Report

## Executive Summary
This report presents the key findings derived from the exploratory data analysis (EDA) of the library borrowing dataset. The analysis focuses on understanding borrowing durations, category-level borrowing patterns, and book popularity. Visual and statistical summaries were used to identify dominant trends, variability across categories, and the presence of outliers that influence overall borrowing behavior.

The dataset includes information on book titles, number of readers, borrowing categories, and borrowing duration in days. No additional preprocessing was required at this stage, as the dataset was already cleaned prior to analysis.

---

## Data Characteristics

### **Variable Overview**
- **Title**: Name of the borrowed book  
- **Reader_num**: Number of readers associated with the book  
- **Category**: Categorical identifier representing book classification  
- **Borrowing_duration**: Number of days a book is borrowed  



### **Category Mapping**
| **Category Code** | **Description** |
|------------------|-----------------|
| **0** | teachers |
| **1** | first-year students |
| **2** | second-year students |
| **3** | third-year students |
| **4** | fourth-year students |


---

## Key Findings & Patterns

### **1. Borrowing Duration Distribution**
**Critical Insight**: Borrowing durations exhibit a **strong right-skewed distribution**.

**Interpretation**:
- Most borrowings occur over **short durations (approximately 5–25 days)**
- A small number of exceptionally long borrowings significantly increase the mean
- The average borrowing duration is therefore **not fully representative** of typical behavior

---

### **2. Borrowing Frequency by Category**
**Critical Insight**: Borrowing activity is **unevenly distributed across categories**.

**Interpretation**:
- Category **1** accounts for the largest share of borrowings
- Category **2** follows, while categories **3, 4, and 0** contribute substantially fewer borrowings
- This imbalance suggests differences in category popularity or usage demand

---

### **3. Borrowing Duration by Category**
**Critical Insight**: Typical borrowing durations are similar across most categories, with notable exceptions.

**Interpretation**:
- Categories **1, 2, 3, and 4** have comparable median borrowing durations
- Category **0** displays extreme outliers, including very long borrowing durations
- These outliers explain the inflated average borrowing duration observed for this category

---

### **4. Average Borrowing Duration per Category**

| **Category** | **Average Duration (days)** | **Interpretation** |
|-------------|-----------------------------|--------------------|
| **0** | 47.89 | Heavily influenced by extreme outliers |
| **1** | 15.98 | Typical medium-term borrowing |
| **2** | 14.80 | Similar borrowing behavior to category 1 |
| **3** | 10.59 | Shortest average borrowing duration |
| **4** | 13.00 | Moderate borrowing duration |

**Interpretation Note**:  
Due to the sensitivity of the mean to extreme values, median-based measures provide a more reliable description of borrowing behavior for category 0.

---

### **5. Most Borrowed Books**
**Critical Insight**: Borrowing activity is **highly concentrated among a small number of titles**.

**Interpretation**:
- The top three most borrowed books have significantly higher borrowing counts than others
- These books are predominantly focused on **algebra and mathematical analysis**
- A sharp drop after the top titles indicates a **long-tail borrowing pattern**

---

## Overall Observations
- Borrowing behavior is predominantly **short-term**
- A small number of categories and titles dominate overall borrowing activity
- Outliers play a significant role in shaping averages and must be considered carefully during interpretation

---


# Library Borrowing Probability Distribution Analysis

## 1. Borrowing Duration Characteristics

- The borrowing duration distribution is **right-skewed (positively skewed)**, indicating that:
  - Most borrowings are **short-term**
  - A small number of borrowings extend for **very long durations**
- There is a **significant gap between the median and the mean**, with the mean pulled upward by long-duration outliers.
- **IQR-based outlier detection** identifies late returns as **extreme cases**.
- The data is **naturally bounded** between **0 and ~365+ days**, reflecting real-world borrowing constraints.

---

## 2. Distribution Fit: Comparative KS-based Results

### Normality Check
- The borrowing-duration data does **not** follow a normal distribution; normality tests reject normality (p < 0.05).

### Updated fit approach
- The notebook performs a comprehensive Kolmogorov–Smirnov (KS) comparison across several candidate distributions (Normal, Exponential, Gamma, Log-Normal, Chi-Square, Power Law, Beta, etc.) and ranks them by KS statistic (lower is better). The ranking can change when preprocessing or cleaning steps are modified, so re-run the comparison cell to obtain the current ranking.

### How to obtain the current best-fit
- Run the notebook cell titled **"11. COMPREHENSIVE DISTRIBUTION COMPARISON"**. It prints a ranked table of KS statistics and p-values and states the current "Best Fit" at the top.
- Use the KS statistic primarily to rank candidate models; use p-values for plausibility (p > 0.05 indicates the test does not reject the null that the samples come from the same distribution). If all p-values are < 0.05, choose the distribution with the lowest KS and consider domain constraints.

### Practical selection criteria
- Combine statistical ranking (KS, p-value) with domain knowledge:
  - Prefer bounded distributions when appropriate (borrowing durations are non-negative and practically bounded).
  - Prefer distributions that model right-skew and long-tail behavior when those properties are present.
  - Use visual checks (histogram + fitted PDF overlay, Q–Q plots) in addition to KS/p-values.

---

## 3. Reader Behavior Insights

- Reader engagement is **highly variable**:
  - Some users borrow frequently.
  - Many borrow rarely or remain inactive.
- A small group of **"super-readers"** accounts for a large share of borrowing activity (Pareto-like behavior).
- The **high standard deviation** in borrowing counts confirms unequal participation.
- A large pool of inactive or underactive readers represents a **significant growth opportunity**.

---

## 4. Book Popularity Distribution

- Book demand is **unequally distributed**:
  - A small number of books are borrowed very frequently.
  - Most books are borrowed rarely or only once.
- Many single-borrow books indicate a **diverse collection with mixed appeal**.
- This pattern aligns with the **Pareto principle (80/20 rule)**.

---

## 5. Category-Based Patterns

- Borrowing behavior varies across:
  - Different student years.
  - Teachers vs. students.
- Some categories:
  - Borrow more frequently.
  - Keep books for longer durations.
- These differences enable **targeted recommendations** and **personalized library services**.

---

## 6. Practical Implications (Using the Beta Distribution)

### Forecasting
- Use estimated Beta parameters to:
  - Predict borrowing durations.
  - Construct reliable confidence intervals.

### Inventory Planning
- Stock high-demand books more heavily.
- Archive or rotate books borrowed only once.

### Retention Strategy
- Focus engagement efforts on inactive readers.
- Convert underutilized users into active borrowers.

### Late Return Prevention
- Identify high-risk borrowings using Beta-based probabilities.
- Implement targeted reminders before expected overdue dates.

---


## Conclusion
The exploratory analysis shows that library borrowing behavior is dominated by short-duration loans, category imbalances, and a small set of frequently borrowed titles. Visual analysis and summary statistics (median, IQR, skewness) are essential because the mean is sensitive to late-return outliers.

Key takeaways about distribution modeling:
- No single parametric distribution perfectly captures the empirical borrowing-duration distribution (multiple tests often return p < 0.05).
- The notebook's KS-based ranking should be used to pick a working model: re-run **"11. COMPREHENSIVE DISTRIBUTION COMPARISON"** to obtain the current ranked results and parameters before using a parametric model in production.
- When statistical tests conflict, prioritize practical constraints (e.g., bounded support) and visual fit (histogram + PDF/Q–Q plots). A bounded, skew-capable model is often preferable in practice but must be validated on the current cleaned data.

Recommended next steps:
- Re-run the distribution-comparison cell to capture the current top-ranked model and parameters, then record those values in this report.
- If no parametric model provides an adequate fit, supplement with empirical (non-parametric) methods such as kernel density estimation or bootstrap-based prediction intervals.

These results form a practical basis for short-term forecasting, inventory planning, and late-return risk management, provided the chosen model is validated on the latest preprocessed dataset.