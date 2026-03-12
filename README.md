# Collection Strategy Optimization using Machine Learning

## Project Overview

Collections teams in financial institutions often manage large portfolios of delinquent accounts.
However, collectors have **limited time and capacity**, which means they cannot contact every account immediately.

The goal of this project is to build a **machine learning–driven prioritization system** that helps collectors focus on accounts with the **highest expected recovery value**, thereby maximizing recovery efficiency.

This project simulates a realistic collections portfolio and demonstrates how predictive modeling can be used to improve operational decision-making.

---

## Business Problem

Assume a portfolio of **2,000 delinquent accounts**.

A collections team can contact only **~100 accounts per day**.

Traditional strategies prioritize accounts based on rules such as:

* Days Past Due (DPD)
* Balance amount
* Allocation lists

However, these approaches may not maximize recovery.

This project proposes a **data-driven prioritization strategy** using machine learning.

---

## Dataset

A synthetic dataset of **2,000 delinquent accounts** was generated with the following features:

* `dpd` – Days Past Due
* `outstanding_balance` – Current outstanding balance
* `customer_income`
* `previous_payments`
* `collection_attempts`
* `region`
* `employment_type`
* `recovered_flag` – Target variable indicating recovery

Additional engineered features were created to capture behavioral signals.

---

## Feature Engineering

Several predictive features were derived:

* **Payment Ratio**

  previous_payments / outstanding_balance

* **Debt-to-Income Ratio**

  outstanding_balance / customer_income

* **Collection Attempt Intensity**

  collection_attempts / dpd

* **DPD Buckets**

  * Early
  * Soft
  * Hard
  * Late

* **High Risk Flag**

These features represent **customer repayment behavior and financial stress**.

---

## Modeling Approach

### Champion Model

**Logistic Regression**

Used because it is:

* Interpretable
* Widely used in credit risk modeling
* Easy to explain to business stakeholders

### Challenger Model

**XGBoost**

Used to test whether a more complex model improves predictive performance.

### Model Validation

5-fold cross-validation was used with **ROC-AUC** as the evaluation metric.

| Model               | Mean ROC-AUC |
| ------------------- | ------------ |
| Logistic Regression | ~0.997       |
| XGBoost             | 1.000        |

Because the improvement was marginal and interpretability is important in financial models, **Logistic Regression was retained as the champion model**.

---

## Recovery Prioritization Strategy

The model predicts the **probability of recovery** for each account.

To prioritize accounts for collectors, we calculate:

Expected Recovery Value

Probability of Recovery × Outstanding Balance

Accounts are then ranked by expected recovery value.

This creates a **data-driven call list for collectors**.

---

## Strategy Simulation

Two strategies were compared:

### Random Calling Strategy

Collectors call accounts randomly.

Expected Recovery:
≈ **7.7M**

### Model-Based Prioritization

Collectors call accounts ranked by expected recovery value.

Expected Recovery:
≈ **24.6M**

### Improvement

Model-driven prioritization improved expected recovery by approximately:

**₹16.8M**

This demonstrates the value of **ML-based decision systems in collections operations**.

---

## Model Insights

Key factors influencing recovery probability include:

* Historical payment behavior
* Delinquency stage (DPD bucket)
* Debt-to-income ratio
* Income segment
* Collection attempt patterns

Customers with prior repayment history and lower financial stress are significantly more likely to recover.

---

## Technologies Used

* Python
* pandas
* scikit-learn
* XGBoost
* matplotlib
* Jupyter Notebook

---

## Project Structure

```
collection-strategy-optimization

├── notebooks
│   └── collection_strategy_model.ipynb
│
├── README.md
```

---

## Key Takeaways

This project demonstrates how machine learning can be applied to **operational decision-making in collections**.

Instead of simply predicting outcomes, the model helps optimize **resource allocation**, ensuring collectors focus on accounts with the highest potential recovery value.

---

## Future Improvements

Possible extensions include:

* Multi-day collector capacity simulation
* Incorporating contact success probability
* Reinforcement learning for dynamic collection strategies
* Real-world dataset validation

---

## Author

Data Analytics Project focused on **Applied Machine Learning for Financial Services**.
