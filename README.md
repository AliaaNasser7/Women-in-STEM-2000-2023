# 👩‍🔬 Women in STEM Education: Global Analysis & Forecasting

> Analyzing gender disparities in STEM education across 6 countries using time series forecasting to reveal when we'll reach parity - and why it's taking so long.

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![Prophet](https://img.shields.io/badge/Prophet-1.1+-green.svg)](https://facebook.github.io/prophet/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)

## 🎯 Project Goal

Investigate female representation in global STEM education, identify key barriers, and forecast future trends to inform policy decisions.

**Main Question:** *When will we achieve gender parity (50%) in STEM graduation rates at the current pace?*

**Answer:** **2039** - approximately 16 years from now.

---

## 📊 Dataset Overview

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

## 🔍 Key Findings

### 1️⃣ The Retention Crisis (Most Important Discovery)

**Enrollment ↔ Dropout: r = 0.648** ⚠️

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

## 🛠️ Methodology

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
- ❌ Linear Regression → R² = -0.017 (failed - needs correlations)
- ✅ Prophet → Reasonable forecasts (designed for time series)

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
✓ Per-country forecasts
```

---

## 📈 Results Summary

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

## 📊 Key Visualizations

### Prophet Forecast
![Prophet Forecast](outputs/prophet_global_forecast.png)

**What it shows:**
- Black dots = Historical data (2000-2023)
- Blue line = Forecast trend
- Light blue = 95% confidence interval (uncertainty)
- Green dashed line = Parity goal (50%)

**Message:** Progress is happening but **too slow** - won't reach parity by 2030.

### Correlation Heatmap
![Correlation Matrix](outputs/correlation_matrix.png)

**What it shows:**
- Most correlations near zero (≈0.04-0.08)
- **Exception:** Enrollment ↔ Dropout = 0.648 (strong!)

**Message:** The retention problem is the real story.

---

## 💡 Strategic Insights

### ❌ What's NOT Working
1. **Enrollment-focused strategies** - weak correlation (0.040) with graduation
2. **Time alone** - minimal improvement over 20+ years (r=0.084)
3. **Current interventions** - insufficient acceleration

### ✅ What Matters
1. **Retention/Dropout** - strongest correlation (0.648)
2. **Quality over quantity** - high enrollment ≠ high graduation
3. **Country-specific approaches** - each has unique patterns

### 🎯 Recommendations
1. **Shift focus** from recruitment to retention
2. **Reduce dropout** in high-enrollment countries
3. **Accelerate progress** by 2.4x to meet 2030 goals
4. **Learn from** low-dropout success stories
5. **Target** high-dropout fields (Engineering, CS)

---

## 🚀 Technologies & Tools

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

### Why Prophet Over Other ML Models?
- **Linear Regression:** Failed (R²=-0.017) - needs strong correlations
- **Random Forest/XGBoost:** Would also fail - same correlation problem
- **Prophet:** Succeeded - designed for sequential patterns, not correlations

---

## 📁 Repository Structure

```
women-stem-analysis/
├── data/
│   └── women_in_stem.csv              # Original dataset
├── notebooks/
│   ├── 01_data_exploration.ipynb      # Initial EDA
│   ├── 02_correlation_analysis.ipynb  # Correlation studies
│   └── 03_prophet_forecasting.ipynb   # Time series forecasting
├── outputs/
│   ├── prophet_global_forecast.png
│   ├── prophet_components.png
│   ├── correlation_matrix.png
│   ├── prophet_predictions_2024_2030.csv
│   └── prophet_country_forecasts_2030.csv
├── requirements.txt
└── README.md
```

---

## 🔧 Installation & Usage

### Prerequisites
```bash
Python 3.8 or higher
```

### Setup
```bash
# Clone repository
git clone https://github.com/yourusername/women-stem-analysis.git
cd women-stem-analysis

# Install dependencies
pip install -r requirements.txt

# Launch Jupyter
jupyter notebook
```

### Requirements.txt
```
pandas>=1.3.0
numpy>=1.21.0
matplotlib>=3.4.0
seaborn>=0.11.0
prophet>=1.1.0
scikit-learn>=0.24.0
scipy>=1.7.0
jupyter>=1.0.0
```

---

## 📚 Key Lessons Learned

### 1. Model Selection Matters
- **Wrong model:** Linear Regression (R²=-0.017) ❌
- **Right model:** Prophet (reasonable forecasts) ✅
- **Lesson:** Match algorithm to data structure, not data to algorithm

### 2. Correlations Tell a Story
- Weak global correlations revealed systemic complexity
- Dropout correlation (0.648) identified the real problem
- Sometimes "no relationship" IS the insight

### 3. Forecasting ≠ Prediction
- Prophet forecasts **trends**, not outcomes from features
- Works when correlations are weak but patterns exist
- Provides honest uncertainty estimates

---

## 🎓 Academic Context

This analysis reveals:
- **Policy implications:** Current strategies insufficient
- **Research gap:** Focus on retention, not just enrollment
- **Methodological insight:** Time series analysis > cross-sectional correlation when relationships are weak
- **Practical value:** 16-year timeline informs resource allocation

---

## 📝 Citation

If you use this analysis, please cite:

```bibtex
@misc{women_stem_analysis_2024,
  title={Women in STEM Education: Global Analysis and Forecasting},
  author={Your Name},
  year={2024},
  publisher={GitHub},
  url={https://github.com/yourusername/women-stem-analysis}
}
```

---

## 👤 Author

**Your Name**
- GitHub: [@yourusername](https://github.com/yourusername)
- LinkedIn: [Your Profile](https://linkedin.com/in/yourprofile)
- Email: your.email@example.com

---

## 📄 License

This project is licensed under the MIT License - see [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- Dataset: [Bisma Sajjad on Kaggle](https://www.kaggle.com/datasets/bismasajjad/womens-representation-in-global-stem-education)
- Prophet: Facebook Research
- Inspiration: The need for data-driven gender equity policy

---

## 🔮 Future Work

- [ ] Expand to more countries (if data becomes available)
- [ ] Field-specific deep dives (why does Engineering have higher dropout?)
- [ ] Policy impact analysis (what interventions worked in low-dropout countries?)
- [ ] Interactive dashboard for exploring predictions
- [ ] Scenario modeling ("What if we reduce dropout by 5%?")

---

**⭐ Star this repository if you found it insightful!**

**🔁 Fork to build upon this analysis**

**💬 Open an issue for questions or suggestions**

---

*Last Updated: December 2024*
