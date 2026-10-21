# Project Report: Used Car Price Prediction in India

**Course:** Data Science Laboratory (BIT23VS01)  
**Project type:** Mini-project — supervised regression  
**Language and libraries:** Python, Pandas, NumPy, Matplotlib, Seaborn, SciPy, Scikit-learn

## 1. Abstract
This project demonstrates a data-science workflow for estimating used-car prices from vehicle characteristics. It includes CSV data loading, quality checks, duplicate removal, missing-value handling, exploratory analysis, a hypothesis test and a comparison of Linear Regression with Random Forest Regression. Models are evaluated with a held-out test set using Mean Absolute Error (MAE), Root Mean Squared Error (RMSE), R-squared (R²) and Mean Absolute Percentage Error (MAPE). The included dataset is synthetic and is intended for reproducible laboratory learning rather than real market pricing.

## 2. Problem statement
Buyers and sellers need a consistent way to understand how a vehicle's age, distance driven, brand, category, fuel type, transmission, engine/power and location relate to its asking price. The project demonstrates how regression methods can model such relationships.

## 3. Aim
To perform data cleaning and exploratory data analysis and build/evaluate regression models for used-car price estimation in Python.

## 4. Objectives
1. Load and inspect tabular data with Pandas.
2. Identify missing values and duplicates, validate numeric ranges, and engineer car age.
3. Use charts and summary statistics to examine the data.
4. Run a Welch two-sample t-test comparing Petrol and Diesel listing prices.
5. Train and compare Linear Regression and Random Forest Regression.
6. Explain model evaluation metrics and demonstrate a sample prediction.

## 5. Dataset description
The supplied CSV contains 1,614 rows before cleaning (1,600 generated records plus 14 repeated rows) and 15 columns. It includes deliberate missing values and duplicate records so preprocessing has a clear purpose. It is generated educational data with market-like value ranges—not a record of real listings.

| Column | Description |
|---|---|
| Car_ID | Identifier; excluded from modelling |
| Brand | Manufacturer |
| Model_Category | Broad class such as Hatchback, Sedan or SUV |
| Year | Year of manufacture |
| Kms_Driven | Distance driven in kilometres |
| Fuel_Type | Fuel/energy category |
| Transmission | Manual or automatic |
| Owner | Previous-owner category |
| Mileage_kmpl | Approximate mileage field |
| Engine_CC | Engine-size feature; electric entries use an illustrative proxy |
| Max_Power_BHP | Approximate maximum power |
| Seats | Seating capacity |
| City | Listing city |
| Seller_Type | Individual/dealer category |
| Selling_Price_INR | Prediction target in Indian rupees |

## 6. Tools and environment
Python 3, Jupyter Notebook/JupyterLab, Pandas, NumPy, Matplotlib, Seaborn, SciPy and Scikit-learn. `joblib` saves the final fitted pipeline.

## 7. Methodology / algorithm
1. Import the CSV and inspect dimensions, types, missing values, duplicates and descriptive statistics.
2. Remove exact duplicate records and normalize text fields.
3. Convert the target to numeric, remove records without positive target prices, filter clearly invalid values, and derive `Car_Age`.
4. Identify possible target-price outliers using the IQR rule; flag rather than automatically remove them because premium cars may legitimately have high prices.
5. Fill missing numeric and categorical predictors within the train-fitted preprocessing pipeline. Standardize numeric columns and one-hot encode categorical features.
6. Split records into 80% training and 20% test sets with a fixed random state.
7. Fit Linear Regression and Random Forest Regression.
8. Compare test-set MAE, RMSE, R² and MAPE, and perform three-fold cross-validation on the selected model.
9. Plot predicted versus actual values, residuals and Random Forest feature importance. Save the entire best pipeline.

## 8. Mathematical background
### Linear Regression
A linear model estimates the target as:

`ŷ = β₀ + β₁x₁ + β₂x₂ + ... + βₚxₚ`

where `ŷ` is predicted price, `x` are input features and `β` are learned coefficients.

### Random Forest Regression
A Random Forest combines predictions from many decision trees. Each tree is fit using randomized samples/features; the final regression prediction is an average across trees. This lets the model learn nonlinear patterns and interactions.

### Evaluation metrics
- **MAE:** average absolute difference between actual and predicted prices; easy to interpret in rupees.
- **RMSE:** square root of mean squared error; penalizes larger errors more strongly.
- **R²:** proportion of test-set target variation explained relative to a mean baseline; values closer to 1 indicate better fit.
- **MAPE:** mean absolute percentage error; useful for interpreting typical relative error, though percentage metrics can be unstable for targets near zero.

### Hypothesis test
H₀: mean Petrol price equals mean Diesel price. H₁: the means differ. Welch's t-test is applied at a 5% significance level. The result is associative and does not show that fuel type alone causes any difference.

## 9. Results and discussion
The supplied notebook was executed with the included synthetic dataset and the fixed random seed. These are example results from that run; small changes can occur across software versions.

### Held-out test-set comparison

| Model | MAE | RMSE | R² | MAPE |
|---|---:|---:|---:|---:|
| Random Forest | ₹132,508 | ₹300,967 | 0.883 | 23.87% |
| Linear Regression | ₹232,635 | ₹436,042 | 0.754 | 79.33% |

Random Forest performed better on all four reported metrics for this generated dataset and was selected by the lowest test-set RMSE. The 3-fold cross-validation MAE for the selected model was approximately **₹142,609 ± ₹21,071**. The sample car in the notebook (Hyundai sedan, age 5 years, 55,000 km) received an estimated price of around **₹622,860** in this run.

The Welch two-sample test reported mean price of about ₹572,925 for Petrol records and ₹690,680 for Diesel records, with p ≈ 0.0253. At the 5% significance level, the notebook rejects the equal-means null hypothesis for this sample. Because the data is synthetic, this result only demonstrates the testing method and does not establish a real-market difference.

The Random Forest's highest feature importances in this run included car age, premium-brand indicators, vehicle category and kilometres driven. Feature importance represents the model's predictive usage, not causation.

## 10. Conclusion
The project demonstrates an end-to-end regression workflow: data loading, cleaning, EDA, basic statistical testing, model development, model comparison and prediction. Random Forest was the better model on the supplied educational dataset. Because the data is synthetic, the metrics, feature relationships and estimated prices are demonstrations only and must not be generalized to real used-car listings.

## 11. Limitations and future scope
- Replace the synthetic data with a documented, licensed real-world dataset for meaningful market conclusions.
- Add condition, service history, accident history, exact model/variant, insurance and listing date.
- Tune model parameters and compare additional algorithms, with careful cross-validation.
- A future version could include a Streamlit-based user interface and model monitoring.

## 12. Syllabus alignment
| Lab syllabus area | Project evidence |
|---|---|
| Python / Data Science tools | Notebook, Pandas, NumPy and Python workflow |
| Data acquisition & cleaning | CSV input, duplicate and missing-value audit, range validation |
| Visualization and EDA | Distribution charts, brand/fuel plots, correlation matrix |
| Statistical / algorithmic modeling | Welch t-test, Linear Regression, Random Forest Regression |
| Model evaluation | MAE, RMSE, R², MAPE and cross-validation |
| Mini-project report | Aim, theory, algorithm, data description, mathematical background, results and limitations |

## 13. References
1. PCCoE, *Data Science Laboratory (BIT23VS01) syllabus*, supplied for this mini-project.
2. Pandas documentation: https://pandas.pydata.org/docs/
3. Scikit-learn documentation: https://scikit-learn.org/stable/
4. Matplotlib documentation: https://matplotlib.org/stable/
5. Seaborn documentation: https://seaborn.pydata.org/
