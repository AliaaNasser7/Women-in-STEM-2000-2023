#  Women in STEM Education: Global Analysis & Forecasting

> Analyzing gender disparities in STEM education across 6 countries using time series forecasting to reveal when we'll reach parity - and why it's taking so long.


## Project Goal

Investigate female representation in global STEM education, identify key barriers, and forecast future trends to inform policy decisions.

**Main Question:** *When will we achieve gender parity (50%) in STEM graduation rates at the current pace?*

**Answer:** **2039** - approximately 16 years from now.

---

## Dataset Overview

- **Source:** [Kaggle - Women's Representation in Global STEM Education](https://www.kaggle.com/datasets/bismasajjad/womens-representation-in-global-stem-education)
- **Records:** 344 observations
- **Countries:** 6 (China, USA, India, Germany, Canada, Australia)
- **Time Period:** 2000-2023
- **STEM Fields:** Biology, Computer Science, Engineering, Mathematics

### Variables
- Female Enrollment (%)
- Female Graduation Rate (%)
- Gender Gap Index (0-1 scale)
- STEM Field
- Country
- Year

---

## Key Findings

### 1️⃣ The Retention Crisis (Most Important Discovery)

**Enrollment ↔ Dropout: r = 0.648** 

Countries with **high female enrollment** also have **high dropout rates**! This reveals:
- Quantity ≠ Quality
- Recruitment success ≠ Retention success  
- The real problem is keeping women in STEM, not getting them in

### 2️⃣ Weak Correlations Everywhere

| Relationship | Correlation | Interpretation |
|--------------|-------------|----------------|
| Enrollment ↔ Graduation | 0.040 | Almost none! |
| Year ↔ Graduation | 0.084 | Minimal progress |
| Gender Gap ↔ Graduation | 0.000 | Zero! |
| **Enrollment ↔ Dropout** | **0.648** | **Strong!** ✓ |

**Insight:** Traditional metrics (enrollment, time) have no linear predictive power. The dropout issue is the only strong signal.

### 3️⃣ Stagnant Global Progress

- **Annual improvement:** Only +1.05% per year
- **Current rate (2023):** 32.6% female graduation
- **2030 projection:** 39.96% (still 10% below parity)
- **Timeline to 50%:** 2039 (16.6 years away)

**To reach parity by 2030:** Would need **2.4x faster** progress!

---

## Methodology

### Phase 1: Data Exploration
```python
✓ Loaded 344 records
✓ No missing values
✓ No duplicates
✓ Created Dropout_Rate feature
```

### Phase 2: Correlation Analysis
```python
✓ Tested relationships between all variables
✓ Discovered weak global correlations (<0.1)
✗ Linear Regression failed (R² = -0.017)
```
**Why Linear Regression Failed:**  
No strong feature-target correlations → Model worse than predicting the mean!

### Phase 3: Model Selection - Why Prophet?

**Attempted:**
-  Linear Regression → R² = -0.017 (failed - needs correlations)
-  Prophet → Reasonable forecasts (designed for time series)

**Why Prophet Succeeded:**
1. **Doesn't need correlations** - analyzes sequential patterns directly
2. **Built for time series** - our data is inherently temporal
3. **Provides uncertainty** - 95% confidence intervals included
4. **Interpretable** - clear trend visualization

### Phase 4: Prophet Forecasting
```python
✓ Trained on historical data (2000-2023)
✓ Projected trends through 2030
✓ Generated confidence intervals
```

---

##  Results Summary

### Global Predictions (2024-2030)

| Year | Predicted Rate | 95% Confidence Interval |
|------|----------------|------------------------|
| 2024 | 38.89% | [32.42%, 45.08%] |
| 2025 | 39.07% | [32.54%, 45.25%] |
| 2026 | 39.25% | [32.43%, 45.55%] |
| 2027 | 39.42% | [33.22%, 45.80%] |
| 2028 | 39.60% | [32.82%, 46.41%] |
| 2029 | 39.78% | [33.13%, 46.39%] |
| 2030 | 39.96% | [33.10%, 46.50%] |

### Growth Metrics
- **Current (2023):** 32.60%
- **Predicted (2030):** 39.96%
- **Total Growth:** +7.35%
- **Annual Rate:** +1.05% per year
- **Gap from Parity:** 10.04% in 2030


---

## Technologies & Tools

### Libraries Used
```python
pandas          # Data manipulation
numpy           # Numerical operations
matplotlib      # Visualizations
seaborn         # Statistical plots
prophet         # Time series forecasting
scikit-learn    # Correlation analysis, initial ML attempts
scipy           # Statistical tests
jupyter         # Interactive analysis
```


