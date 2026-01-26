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

## 2. Distribution Fit: **Beta Distribution as the Best Model**

### Normality Check
- The data **does not follow a normal distribution**.
- All applied normality tests reject normality with **p < 0.05**.

### Why Beta Distribution?
The **Beta distribution** provides the best fit among all tested distributions due to:

- **Bounded support**
  - Naturally defined on a finite interval, matching borrowing durations.
- **Skewness flexibility**
  - Accurately models both the high concentration of short-term borrowings and the long right tail.
- **Flexible shape parameters (α, β)**
  - Adapt precisely to the observed data structure.
- **Statistical validation**
  - Lowest **Kolmogorov–Smirnov (KS) statistic** among 7 tested distributions.
  - Strong p-value indicating excellent alignment with empirical data.
- **Real-world consistency**
  - Bounded domain, unimodal peak, and heavy right tail are signature features of Beta distributions.

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

### Risk Management
- Predict return dates more accurately using a **bounded Beta model**, avoiding unrealistic predictions from unbounded distributions like the normal distribution.

---


## Conclusion
The exploratory analysis reveals that library borrowing patterns are characterized by short borrowing durations, strong category imbalances, and high concentration around a limited number of popular academic titles. While average statistics provide a general overview, visual analysis highlights the importance of considering distribution shape and outliers when interpreting borrowing behavior.

Modeling borrowing durations with the **Beta distribution** provides a statistically sound and practically meaningful framework. It aligns with real-world constraints, captures skewness and outliers effectively, and supports better forecasting, planning, and decision-making in library management.

These insights provide a solid foundation for further analysis, such as user behavior modeling, demand forecasting, or policy evaluation regarding borrowing limits and category management.