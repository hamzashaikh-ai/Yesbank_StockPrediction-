# 📈 Yes Bank Stock Closing Price Prediction

![Python](https://img.shields.io/badge/Python-3.10-blue?style=flat-square&logo=python)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?style=flat-square&logo=jupyter)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-ML-yellowgreen?style=flat-square&logo=scikit-learn)
![XGBoost](https://img.shields.io/badge/XGBoost-Regressor-red?style=flat-square)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=flat-square)

> **Regression project** — Predicting the monthly closing stock price of Yes Bank using historical OHLC data (2005–2020) with Linear Regression, Decision Tree, and XGBoost.

---

## 📌 Problem Statement

Yes Bank is a well-known private sector bank in India. Since 2018, it has been in the news because of a major fraud case involving its founder Rana Kapoor. This incident had a severe impact on the bank's stock prices.

The goal of this project is to **predict the monthly closing price** of Yes Bank's stock using Open, High, and Low prices — and to understand what patterns ML models can (and cannot) learn from a dataset that includes a real-world black swan event.

---

## 📂 Dataset

| Feature | Description |
|---------|-------------|
| `Date`  | Month-Year (Jul-05 to Nov-20) |
| `Open`  | Opening stock price of the month |
| `High`  | Highest price reached during the month |
| `Low`   | Lowest price reached during the month |
| `Close` | **Target variable** — Closing price of the month |

- **185 monthly records** spanning July 2005 to November 2020
- No missing values, no duplicates
- Close price ranges from ₹9.98 to ₹367.90

---

## 🗂️ Project Structure

```
Yesbank_StockPrediction-/
│
├── Yes_Bank_Stock_Price_Prediction.ipynb   # Full ML pipeline notebook
├── data_YesBank_StockPrices.csv            # Dataset
└── README.md
```

---

## 🔄 Project Architecture

```
EDA → Clean-up → Feature Engineering → Pre-Processing → Model Implementation → Model Explainability
```

**Step-by-step:**
1. **EDA** — Candlestick trends, moving averages, visualizing relationships, hypothesis formation
2. **Clean-up** — Null/duplicate check, outlier analysis
3. **Feature Engineering** — Price Range, Open-Close Gap, High/Low Open Ratios, Year, Month
4. **Pre-Processing** — StandardScaler, chronological Train-Test Split (80/20)
5. **Model Implementation** — Linear Regression → Decision Tree → XGBoost (all with GridSearchCV tuning)
6. **Model Explainability** — Feature importance, residual analysis, final comparison

---

## 📊 Key EDA Insights

- **Closing price** grew steadily from ₹12 (2005) to a peak of ~₹368 (early 2019), then collapsed to below ₹15 after the RBI moratorium in March 2020
- **Open, High, Low** are all **>99% correlated** with Close — OHLC features are extremely strong predictors
- A **"death cross"** (6-month MA crossing below 12-month MA) appeared in late 2018 — a classical sell signal that perfectly marked the start of the crash
- Monthly **Price Range** (volatility) spiked from <₹30 to >₹50 in 2018–2019, indicating panic trading
- A ₹100 investment in 2005 grew to ~₹3,000 equivalent by 2018 and was nearly wiped out by 2020

---

## ⚙️ Feature Engineering

| Feature | Formula | Meaning |
|---------|---------|---------|
| `Price_Range` | High − Low | Monthly volatility |
| `Open_Close_Gap` | Close − Open | Bullish (+) or Bearish (−) momentum |
| `High_Open_Ratio` | High / Open | How high price peaked above open |
| `Low_Open_Ratio` | Low / Open | How low price fell below open |
| `Year` | Extracted from Date | Captures long-term trend |
| `Month` | Extracted from Date | Captures seasonality |

---

## 🤖 Models Used

| Model | Type | Tuning |
|-------|------|--------|
| Linear Regression | Baseline | StandardScaler |
| Decision Tree Regressor | Non-linear | GridSearchCV (max_depth, min_samples_split, min_samples_leaf) |
| XGBoost Regressor | Ensemble / Gradient Boosting | GridSearchCV (n_estimators, learning_rate, max_depth, subsample) |

All models evaluated with **5-Fold Cross Validation**.

---

## 📈 Results

| Model | R² | MAE (₹) | RMSE (₹) | MAPE (%) |
|-------|----|---------|---------|---------|
| Linear Regression | ~0.99 | Low | Low | <5% |
| Decision Tree (Tuned) | ~0.99 | Low | Low | <5% |
| **XGBoost (Tuned)** | **Best** | **Lowest** | **Lowest** | **<5%** |

> **XGBoost (Tuned) is the best performing model** — lowest RMSE and MAPE, best generalization on the volatile 2018–2020 test period.

---

## 💡 Business Insights

1. **Open price alone predicts Close with >99% correlation** — if you know the opening price, you can predict the close with high confidence
2. **No OHLC-based ML model can predict black swan events** — the 2018 governance fraud was a fundamental failure, not a price pattern
3. **XGBoost is the recommended production model** — handles volatility spikes better, built-in regularization prevents overfitting
4. **MAPE < 5%** across tuned models — commercially viable for portfolio valuation and risk management
5. **Engineered features add real value** — Price Range and Open-Close Gap consistently ranked as top features in tree-based models

---

## 🛠️ Tech Stack

- **Language:** Python 3.10
- **Libraries:** Pandas, NumPy, Matplotlib, Seaborn, Scikit-Learn, XGBoost, SciPy
- **Environment:** Jupyter Notebook
- **Tuning:** GridSearchCV with 5-Fold Cross Validation

---

## 🚀 How to Run

```bash
# 1. Clone the repo
git clone https://github.com/hamzashaikh-ai/Yesbank_StockPrediction-.git
cd Yesbank_StockPrediction-

# 2. Install dependencies
pip install pandas numpy matplotlib seaborn scikit-learn xgboost scipy jupyter

# 3. Launch notebook
jupyter notebook Yes_Bank_Stock_Price_Prediction.ipynb
```

---

## 👤 Author

**Muhammad Hamza Shaikh**  
B.Tech AI & ML | P.P. Savani University  
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=flat-square&logo=linkedin)](https://linkedin.com/in/muhammadhamza-shaikh-698b90381)
[![GitHub](https://img.shields.io/badge/GitHub-hamzashaikh--ai-black?style=flat-square&logo=github)](https://github.com/hamzashaikh-ai)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
