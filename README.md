# Explainable Credit Risk PD Modelling with WOE-Engineered Features
## Desciption
This project developed a credit risk model to estimate the Probability of Default (PD) for loan applicants. The objective was to identify key borrower characteristics associated with credit default and construct an interpretable model for credit risk assessment.  

A logistic regression model was developed using features transformed with the Weight of Evidence (WOE) technique. The advantages of WOE included improved model interpretability, efficient transformation of categorical variables without generating numerous dummy variables, and reduced sensitivity to outliers through binning. However, WOE binning did not always guarantee a monotonic relationship between numerical predictors and the probability of default. To address this limitation, the Pool Adjacent Violators Algorithm (PAVA) was applied to enforce monotonicity and produce more stable predictors.  

Based on the final logistic regression model, a credit scorecard was constructed, which demonstrated significantly better predictive performance than the original credit score provided in the dataset.

## Data Setup
The dataset contains borrower demographic information, loan characteristics, and credit-related variables used to predict loan defaults. It can be downloaded using the following methods:
### Option 1: Kaggle API
Install the Kaggle API and download the dataset.
```
pip install kaggle
kaggle datasets download -d udaymalviya/bank-loan-data
unzip bank-loan-data.zip
```

### Option 2: Manual Download
Download the dataset manually from Kaggle:  
https://www.kaggle.com/datasets/udaymalviya/bank-loan-data  

## Methodology
The modelling pipeline follows a traditional credit scoring framework widely used in financial risk modelling.
1. **Exploratory Data Analysis (EDA)**  
   Exploratory analysis was first conducted to examine the distribution of variables and their relationship with loan default. Visualisation tools such as boxplots and bar charts were employed to identify potential outliers, missing values, and general data patterns.
2. **Feature Screening**  
   Two statistical tests were implemented to assess the predictive relevance of individual variables. Univariate logistic regression was applied to numerical variables, while chi-square tests were used to evaluate the association between categorical variables and loan default.

3. **WOE Transformation and PAVA**  
  To enhance model interpretability, predictor variables were transformed using the Weight of Evidence (WOE) technique. The Pool Adjacent Violators Algorithm (PAVA) was incorporated during the binning process to enforce monotonic relationships between predictors and the probability of default. After transformation, Variance Inflation Factor (VIF) and correlation analysis were examined to detect potential multicollinearity among variables.

4. **Logistic Regression Model**  
  A logistic regression model was then constructed to estimate the log-odds of the probability of default. The Wald test was subsequently applied to evaluate the statistical significance of predictors selected through LASSO regularisation.

5. **Discrimination Analysis**  
  Model discrimination was assessed using several metrics, including the Receiver Operating Characteristic (ROC) curve, Area Under the Curve (AUC), Gini Index, and the Kolmogorov–Smirnov (KS) statistic. Additional evaluation tools such as the confusion matrix, decile analysis, and gain and lift charts provided further insights into classification performance across different borrower risk segments. 

6. **Calibration Analysis**  
  Calibration analysis focused on the alignment between predicted probabilities and observed default outcomes. The calibration curve visualised this relationship, while the Brier score summarised the overall accuracy of the probability estimates. The Hosmer–Lemeshow test was also conducted to examine the goodness-of-fit of the logistic regression model across different risk groups.

7. **Internal Stability Analysis**  
   Internal stability was examined by comparing model performance across different borrower segments, including gender and education level. This step ensured that the model produced consistent predictions across subgroups and did not exhibit systematic bias toward specific populations.

8. **Credit Scorecard Construction**   
   The final logistic regression model was converted into a credit scorecard to provide an interpretable scoring system for credit risk assessment.
