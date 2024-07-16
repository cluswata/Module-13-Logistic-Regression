**Taiwanese Companies Bankruptcy Prediction using Logistic Regression**

**Business Understanding**
Bankruptcy prediction is critical for financial stability and risk management. By accurately identifying companies at risk of bankruptcy, stakeholders can take proactive measures to mitigate financial losses and protect investments.

**Objective:**
The objective of this project is to predict the likelihood of bankruptcy of Taiwanese companies based on financial and accounting data. The prediction will help financial institutions, investors, and stakeholders assess the risk associated with potential investments or existing clients.


**Data Understanding**
**Data Source:**
The dataset used for this project is sourced from the UCI Machine Learning Repository (ID: 572). It includes financial ratios and accounting-based metrics from Taiwanese companies, labeled with binary indicators (0 for non-bankrupt, 1 for bankrupt).

**Variables:**
**Features (X):** Financial ratios and metrics such as liquidity ratios, profitability ratios, leverage ratios, and operational ratios.<br>
**Target (y):** Binary indicator (0 or 1) representing bankruptcy status.

**Data Exploration:**
**Exploratory Data Analysis (EDA):** Carreid out to understand the distribution of features, detect outliers, and assess correlations between variables.
**Visualization:** bar plot, pair plots, correlation matrices, confusion matrices, and area under the ROC (ROC-AUC) plotted in order to gain insights into the data.

**Data Preparation and Feature Engineering:**
**Data Cleaning:** Missing values, duplicated records, outliers, and inconsistencies in the dataset assesed.<br>
**Transformations:** Features were normalized or standardized prior to modelling. L2 regularization for handling any multicollinear features. Due to shortage of time, no new features nor complex interactions between features were derived.<br>
**Dataset:** Because of the low bankruptcy rate (220/6819), a sample of 1 record from X where y=1 for every 4 records from X where y=0 was selected (220/1100).<br>
**Train-Test Split:** Total sample size (N = 1100) was split into training (75%) and testing (25%) sets after shuffling.<br>
**Feature Selection:** Permutation importance with logistic regression was used to identify and keep only the most important 10 features.

**Modeling**
**Model Selection:** Logistic Regression chosen for its interpretability, ability to handle binary classification, and efficiency with structured data.<br>
**Model Training:** The logistic regression model was fit on the training data.
Tune hyperparameters if necessary (e.g., regularization strength) using cross-validation techniques.

**Evaluation**
**Model Evaluation Metrics:** Assessed accuracy, precision, recall, F1-score and ROC-AUC to understand model performance. The confusion matrix was assessed to understand true positives, true negatives, false positives, and false negatives.


**Model Equation:**
 log(p / (1 - p)) = -2.0855 + (0.2130 *  Fixed Assets Turnover Frequency) + (-0.1068 *  Interest-bearing debt interest rate) + (0.3075 *  Cash/Current Liability) + (-0.0508 *  Long-term Liability to Current Assets) + (0.1587 *  Quick Asset Turnover Rate) + (-0.0917 *  Interest Expense Ratio) + (-0.0935 *  Regular Net Profit Growth Rate) + (-0.1425 *  Continuous Net Profit Growth Rate) + (0.1180 *  Net Value Growth Rate) + (-0.9108 *  Total Asset Return Growth Rate Ratio) + (-0.0150 *  Cash Reinvestment %) + (-2.8550 *  Current Ratio)

Log-Likelihood: 0.8460606060606061
Number of Observations (N): 825
LR Chi-squared: 1396.0
Prob > Chi-squared: 1.013130006148348e-291

Hosmer-Lemeshow Test:
HL Chi-squared: 5474.6639
HL Degrees of Freedom: 8
HL p-value: 0.0000

Model Evaluation on Test Set:
Accuracy: 0.8255
Precision: 0.6842
Recall: 0.2364
F1-score: 0.3514
ROC-AUC: 0.8069

Classification Report:
              precision    recall  f1-score   support

           0       0.84      0.97      0.90       220
           1       0.68      0.24      0.35        55

    accuracy                           0.83       275
   macro avg       0.76      0.60      0.63       275
weighted avg       0.81      0.83      0.79       275

[[214   6]
[ 42  13]]

**Model Interpretation Summary:**<br>

The logistic regression model shows a high log-likelihood and significant LR chi-squared statistic, indicating a good fit to the data and statistical significance of the predictors. However, the HL test suggests a lack of fit, indicating that predicted probabilities do not match observed frequencies well across groups.

The model's performance metrics on the test set (accuracy, precision, recall, f1-score, ROC-AUC) show promising results, with accuracy of 0.8255 indicating overall good predictive performance, especially for class 0 (non-bankrupt companies).

Overall, while the model demonstrates statistical significance and reasonable predictive performance, the discrepancy highlighted by the Hosmer-Lemeshow (HL) test warrants further investigation into potential model refinement or data considerations.

**Interpretation of parameter estimates:**<br> <br>
**Fixed Assets Turnover Frequency:** A higher turnover frequency of fixed assets (Coef. = 0.2130) is associated with an increased log-odds of bankruptcy (p< 0.001). Companies with more frequent turnover of fixed assets are more likely to be predicted as bankrupt.

**Interest-bearing debt interest rate:** A higher interest-bearing debt interest rate (Coef. = -0.1068) is associated with a decreased log-odds of bankruptcy (p = 0.002). Companies with higher interest rates on their debt are less likely to be predicted as bankrupt. This could indicate that despite higher costs of borrowing (higher interest rates), these companies are able to secure financing to cover their obligations, thereby reducing the likelihood of bankruptcy.

**Cash/Current Liability:** A higher ratio of cash to current liabilities (Coef. = 0.3075) is associated with an increased log-odds of bankruptcy (p > < 0.001). Companies with higher cash reserves relative to their current liabilities are more likely to be predicted as bankrupt. Maintaining excessively high cash reserves may indicate operational inefficiencies or lack of effective financial planning. Companies might hoard cash due to uncertainties or inability to deploy funds into productive investments or growth opportunities.

**Long-term Liability to Current Assets:** A higher ratio of long-term liabilities to current assets (Coef. = -0.0508) shows a slight decrease in the log-odds of bankruptcy, but this effect is not statistically significant (p = 0.145).

**Quick Asset Turnover Rate:** A higher rate of turnover for quick assets (Coef. = 0.1587) is associated with an increased log-odds of bankruptcy (p > < 0.001). Companies that efficiently turn over their quick assets are more likely to be predicted as bankrupt. High turnover of quick assets might involve liquidating these assets frequently to fund operations or pay debts. While this can provide short-term relief, frequent asset liquidation could signal an inability to generate sustainable revenue or profitability through core business operations.

**Interest Expense Ratio:** A higher interest expense ratio (Coef. = -0.0917) is associated with a decreased log-odds of bankruptcy (p = 0.009). Companies with lower interest expenses relative to their earnings are less likely to be predicted as bankrupt.

**Regular Net Profit Growth Rate, Continuous Net Profit Growth Rate, Net Value Growth Rate: Higher growth rates** (Coef. = -0.0935, -0.1425, 0.1179 respectively) indicate mixed effects on bankruptcy prediction, with the regular and continuous net profit growth rates showing slight decreases in the log-odds (p < 0.05), while net value growth rate shows a slight increase (p = 0.001).

**Total Asset Return Growth Rate Ratio:** A higher ratio of total asset return growth rate (Coef. = -0.9108) is strongly associated with a decreased log-odds of bankruptcy (p < 0.001). Companies with higher returns on their total assets are significantly less likely to be predicted as bankrupt.

**Cash Reinvestment %:** The percentage of cash reinvestment (Coef. = -0.0150) shows a negligible effect on bankruptcy prediction (p = 0.675). This feature is not statistically significant.

**Current Ratio:** A higher current ratio (Coef. = -2.8550) is strongly associated with a decreased log-odds of bankruptcy (p < 0.001). Companies with higher current ratios are significantly less likely to be predicted as bankrupt.
