# Trader Performance vs Market Sentiment Analysis

## Project Overview
This project explores the relationship between market sentiment and trader performance using two primary datasets:  
1. **Bitcoin Market Sentiment Dataset** – contains daily market sentiment values labeled as Fear, Greed, or Neutral.  
2. **Historical Trader Data from Hyperliquid** – includes trade-level information such as account, coin, execution price, trade size, direction, PnL, and timestamp.  

The main goal is to uncover patterns between sentiment and profitability and provide actionable insights for traders.

---

## 1. Exploratory Data Analysis (EDA)

The EDA forms the major part of this analysis and includes the following steps:

### **Data Preparation**
- Merged the sentiment and trader datasets on the `date` column.  
- Created a simplified sentiment column (`sentiment_simple`) with categories: Fear, Greed, Neutral.  
- Added a binary target column `is_profit` indicating whether a trade was profitable.

### **Distribution Analysis**
- Plotted histograms and KDEs of `closed_pnl` to visualize profit/loss distributions.  
- Created boxplots of `closed_pnl` grouped by sentiment to compare performance under Fear, Greed, and Neutral market conditions.  

### **Daily Aggregation**
- Aggregated data by date and sentiment to compute total PnL, mean PnL, and trade counts per day.  
- Observed patterns in extreme sentiment days (Extreme Fear vs Extreme Greed) and their impact on profits.

### **Win Rate Analysis**
- Calculated win rate per sentiment category.  
- Visualized win rates using barplots to identify which sentiment conditions lead to higher probability of profitable trades.

### **Statistical Testing**
- Performed t-tests to compare average PnL between Fear and Greed.  
- Computed Cohen’s d to measure effect size.  
- Findings: Extreme Fear days significantly reduce profitability, while Extreme Greed days increase it slightly.

---

## 2. Predictive Analysis

To quantify the impact of sentiment and trade characteristics, a predictive model was built:

### **Model Setup**
- **Target:** `is_profit` (1 = profitable trade, 0 = loss)  
- **Features:** `sentiment_simple`, `size_usd`, `direction`  
- Categorical features were one-hot encoded.  
- Numeric features (trade size) were scaled for stability.

### **Model Training**
- Logistic Regression was used due to interpretability and simplicity.  
- Train/test split: 70% training, 30% testing.  
- Model fitted using regularization to avoid overfitting.

### **Evaluation**
- **Accuracy:** 92%  
- **ROC AUC:** 0.946  
- Feature importance analysis showed sentiment and trade size as the most significant predictors of trade profitability.  

### **Insights**
- Market sentiment strongly influences trading outcomes.  
- Larger trades in Greed periods have higher chances of profit, while Extreme Fear increases the likelihood of losses.  
- The predictive model allows traders to quantify risk and make data-driven decisions based on sentiment and trade characteristics.

---

## 3. Conclusion
The project successfully combines **exploratory analysis** with **predictive modeling** to understand the effect of market sentiment on trader performance. EDA highlights patterns and statistical differences, while the logistic regression model quantifies the predictive power of sentiment and other trade features.

---

## 4. Libraries Used
- `pandas`, `numpy` – data manipulation  
- `matplotlib`, `seaborn` – visualization  
- `scipy.stats` – statistical tests (t-test, Cohen’s d)  
- `sklearn` – predictive modeling, preprocessing, and evaluation  

---

## 5. Future Work
- Include additional features such as coin type, time-of-day effects, or leverage (if available).  
- Explore ensemble models (Random Forest, XGBoost) to improve prediction performance.  
- Incorporate aggregated daily sentiment as a predictive feature for multiple trades per day.
