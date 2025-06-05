# 💳 Credit Card Fraud Detection with PySpark & Random Forest

This project involves detecting fraudulent credit card transactions from over 1 million synthetic records. It covers exploratory data analysis (EDA), feature engineering, model development (logistic regression & random forest), and simulation of real-world deployment.

---

## 📊 Dataset Summary

The dataset contains anonymized credit card transactions with the following key fields:

- Transaction details: `amt`, `trans_date_trans_time`, `category`, `merchant`
- User profile: `age`, `gender`, `job`, `location`, `city_pop`
- Location metadata: `lat/long`, `merch_lat/merch_long`
- Label: `is_fraud` (0 or 1)

---

## 🧪 Exploratory Data Analysis

### ✅ Key Insights:
- **Fraud by Hour:** Peaks around early morning hours
- **Fraud by Month/Day:** Evenly distributed
- **Fraud by Gender:** Slightly higher in males
- **Fraud by Category:** Highest in `shopping_net`, `misc_net`, `grocery_pos`
- **Fraud by State:** Delaware (DE) had anomalous 100% fraud rate
- **Fraud by Age Group:** Highest fraud rate in `50-64` and `65+` groups
- **Fraud by Job:** Suspicious spikes with small sample sizes (100% fraud in rare jobs)

---

## 🛠️ Feature Engineering

Over 10 new features were created, including:

| Feature | Description |
|--------|-------------|
| `hour`, `day_of_week`, `month`, `year` | Extracted from timestamp |
| `age`, `age_group` | Derived from `dob` |
| `distance_km`, `is_distance_suspicious` | Geo-distance between user & merchant |
| `user_txn_count`, `user_avg_amt`, `user_std_amt` | Aggregated behavioral features |
| `is_high_spender`, `is_low_variance_spend` | Spending patterns |
| `is_high_risk_category`, `is_high_risk_state`, `is_flagged_merchant` | Domain-driven risk flags |

---

## 🧠 Models & Evaluation

### 1. **Logistic Regression (Baseline)**

| Metric | Value |
|--------|-------|
| Precision | 0.623 |
| Recall | 0.105 |
| F1 Score | 0.18 |

---

### 2. **Random Forest Classifier**

| Metric (Threshold = 0.5) | Value |
|--------------------------|-------|
| AUC | 0.990 |
| Precision | 0.978 |
| Recall | 0.548 |
| F1 Score | 0.703 |

#### 🔁 Threshold Tuning Results:

| Threshold | Precision | Recall | F1 Score |
|-----------|-----------|--------|----------|
| 0.50 | 0.978 | 0.548 | 0.703 |
| 0.40 | 0.961 | 0.601 | 0.739 |
| 0.30 | 0.938 | 0.700 | 0.802 |
| 0.20 | 0.860 | 0.776 | 0.816 |
| 0.10 | 0.623 | 0.826 | 0.710 |

🔍 **Selected threshold: 0.2** (optimized for recall and F1)

---

## 📊 Feature Importances (Top 5)

| Feature | Importance |
|---------|------------|
| `user_avg_amt` | High |
| `hour` | High |
| `category_index` | Medium |
| `distance_km` | Medium |
| `user_std_amt` | Medium |

---

## 🚀 Future Scope

### ✅ Model Deployment

- Serve model with **FastAPI** or **Flask**
- Containerize with **Docker**

### ✅ Kubernetes Integration (Planned)

- Deploy inference API via **Kubernetes Deployment**
- Autoscale using **Horizontal Pod Autoscaler**
- Add monitoring with **Prometheus + Grafana**
- Integrate streaming via **Kafka or Kinesis**

### ✅ Synthetic Data Generator

- Simulate real-time transactions
- Feed into live API or message queues

---

## 📂 How to Run

```bash
git clone https://github.com/kumarbaibhav6/Credit-Card-Fraud-Detection-.git
cd Credit-Card-Fraud-Detection-

# Create env and install dependencies
pip install -r requirements.txt

# Launch notebook
jupyter notebook
