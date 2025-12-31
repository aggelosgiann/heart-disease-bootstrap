# Heart Disease Prediction: Robust Bootstrap Analysis

This repository contains a statistical re-evaluation of heart disease prediction models using **Bootstrap Analysis**. It serves as a rigorous follow-up to standard cross-validation approaches, focusing on **Clinical Safety (Recall)** and **Statistical Significance**.

While the original research and many standard implementations rely on simple train/test splits or cross-validation, this project uses bootstrapping ($N=1000$) to generate confidence intervals and p-values, ensuring that performance improvements are not just due to random chance.

## Reference Paper

This analysis is a methodological extension based on the primary research paper:

* **Title:** [Comparative analysis of heart disease prediction using logistic regression, SVM, KNN, and random forest with cross-validation for improved accuracy](https://www.nature.com/scientificreports/)
* **Authors:** Yagyanath Rimal, et al.
* **Journal:** *Scientific Reports* (2025) 15:13444
* **DOI:** [10.1038/s41598-025-93675-1](https://doi.org/10.1038/s41598-025-93675-1)

---

## Methodology

The notebook `Bootstrap.ipynb` implements a rigorous evaluation framework designed for medical diagnostics.

### 1. The Strategy: Safety First
In medical diagnostics, a "False Negative" (missing a sick patient) is far worse than a "False Positive". Therefore, we apply a **Recall Constraint**:
* **Constraint:** Any viable model must achieve a **Recall** of $\ge$ 90%**.
* **Optimization:** Among models meeting this safety constraint, we select the one with the highest Accuracy.

### 2. The Technique: Bootstrap ($N=1000$)
Instead of a single accuracy score, we use bootstrapping to simulate 1,000 different dataset variations. This allows us to:
* Calculate **95% Confidence Intervals (CI)** for Accuracy.
* Perform **Paired t-tests** to verify if tuned models are significantly better than baselines.

---

## Key Findings

The move to robust bootstrap analysis provided different insights compared to standard cross-validation. 

### **Winner: Logistic Regression**
In this rigorous testing environment, **Logistic Regression** was the **only** model to successfully meet the clinical safety constraint.
* **Safety Met:** It achieved a Recall of **91.19%**.
* **Performance:** Tuned Accuracy of **81.98%** (95% CI: 75.65% - 87.74%).
* **Statistical Significance:** The tuning process yielded a statistically significant improvement ($p < 0.0001$) over the baseline.

### **Excluded Models**
Despite their popularity in other contexts, the following models failed to consistently meet the 90% recall safety threshold across the 1,000 bootstrap iterations:
* **Random Forest**
* **K-Nearest Neighbors (KNN)**
* **Support Vector Classifier (SVC)**

*Note: This demonstrates that while complex models often yield higher raw accuracy, simple linear models (like Logistic Regression) can sometimes offer better robustness and control for specific clinical safety parameters.*

---

## Repository Structure

* `Bootstrap.ipynb`: The main analysis notebook. It includes:
    * Data fetching (from UCL Heart Disease Data).
    * Bootstrap implementation (manual loop with `resample`).
    * Model tuning grids.
    * Statistical reporting (Confidence Intervals & p-values).

## How to Run

1.  **Download:** Clone this repository or download `Bootstrap.ipynb`.
2.  **Execute:** Open the file in Jupyter Notebook, JupyterLab, or Google Colab and run all cells.
**Requirements:**
* The code is self-contained and fetches data automatically from the web.
* **Libraries:** `pandas`, `numpy`, `scikit-learn`, `scipy`.
