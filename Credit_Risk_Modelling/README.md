# Credit Risk Analysis

## Project Overview
This project aims to analyze credit risk to assess potential risks associated with loan applicants and categorize customers based on their likelihood of loan default. The model is trained on a dataset containing customer information and loan details. Various machine learning models are used to predict creditworthiness, and customers are assigned credit scores based on their predicted probability of default.

## Methodology
### 1. Data Cleaning
- **Handling Missing Values** - Missing values in each column were filled them with appropriate values (e.g., mean, median, or mode).
- **Dropping Unnecessary Columns** - Some columns that were irrelevant for analysis were removed from the dataset.
- **Data Type Conversions** - Columns with wrong data types were converted into appropriate data types (e.g., categorical to numerical) to ensure consistency in analysis.
- **Renaming Columns** - Columns were renamed for easy readability and understanding of the data.

### 2. Exploratory Data Analysis (EDA)
Basic exploratory data analysis was conducted to get an overview of the data,visualize key trends and distributions in the data, as well as identify relationships between the features in the dataset.

### 3. Data Preprocessing
**Encoding Categorical Variables:** - Categorical columns were encoded using a label encoding to convert them into numerical form.

### 4. Handling Class Imbalance
There existed an imbalance in the distribution of the classes in the target variable (`y`). SMOTE (Synthetic Minority Over-sampling Technique) was applied in order to balance the classes.

### 5. Model Training and Evaluation
A number of classification models were trained and the model were evaluated

2. **Logistic Regression:**
   - Standard logistic regression is applied, achieving an accuracy of **81.6%**.
   - L1-regularized logistic regression (Lasso) and L2-regularized logistic regression (Ridge) are also tested.

3. **Decision Tree Classifier:**
   - A Decision Tree model is trained and cross-validated.
   - The mean accuracy score is **96.1%**.

4. **Random Forest Classifier:**
   - A Random Forest model is trained and evaluated using cross-validation.
   - The mean accuracy is **98.1%**, and additional metrics (precision, recall, F1-score) are reported.

### 6. Generating Credit Scores and Categorizing Customers
1. **Credit Score Calculation:**
   - A Random Forest model is trained and used to predict loan default probabilities.
   - These probabilities are scaled to a range of **0-800** to represent credit scores.

2. **Customer Categorization:**
   - Customers are classified into five categories based on credit score:
     - **Bad Customer** (≤ 200)
     - **2nd Worst** (201 - 350)
     - **Not So Bad** (351 - 500)
     - **Ideal Guys** (501 - 700)
     - **Big Loans** (> 700)
   
## Hyperparameter Tuning
1. **Randomized Search for Best Parameters:**
   - A `RandomizedSearchCV` is used to optimize the hyperparameters of the Random Forest classifier.
   - The best parameters found are:
     - `max_depth`: 25
     - `min_samples_leaf`: 2
     - `min_samples_split`: 4
     - `n_estimators`: 72
   - The best accuracy achieved through tuning is **97.5%**.

## Conclusion
- The project successfully predicts credit risk and categorizes customers using machine learning techniques.
- Random Forest performed best, achieving high accuracy and reliable classification.
- Future improvements could include feature engineering and testing additional models.



## Conclusion
This project provides a structured approach to cleaning and preparing credit risk data for analysis. By handling missing values and unnecessary columns efficiently, it sets the stage for further predictive modeling and decision-making processes.


