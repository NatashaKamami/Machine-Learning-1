# Credit Risk Analysis

## Project Overview
This project aims to analyze credit risk to assess potential risks associated with loan applicants and categorize customers based on their likelihood of loan default. The model is trained on a dataset containing customer information and loan details. Various machine learning models are used to predict creditworthiness, and customers are assigned credit scores based on their predicted probability of default.

## Methodology
### 1. Data Cleaning
- **Renaming Columns** - Columns were renamed for easy readability and understanding of the data.
- **Handling Missing Values** - Missing values were filled them with appropriate values (e.g., mean, median, or mode) amd columns with missing values amounting to 60% of the data were dropped. Furthermore, records that had missing values in more than one column where the columns semmed correlated were also dropped since the missingness of these values was not completely random.
- **Dropping Unnecessary Columns** - Some columns that were irrelevant for analysis were removed from the dataset.


### 2. Exploratory Data Analysis (EDA)
Basic exploratory data analysis was conducted to get an overview of the data,visualize key trends and distributions in the data, as well as identify relationships between the features in the dataset.

### 3. Data Preprocessing
**Encoding Categorical Variables:** - Categorical columns were encoded using a label encoding to convert them into numerical form.

### 4. Handling Class Imbalance
There existed an imbalance in the distribution of the classes in the target variable (`y`). SMOTE (Synthetic Minority Over-sampling Technique) was applied on the dataset in order to balance the classes.

### 5. Model Training and Evaluation
A number of classification models were trained and the models were evaluated using the f1 score. The models implemented included:

1. **Logistic Regression:** - Standard logistic regression was applied, as well as L1-regularized logistic regression (Lasso) and L2-regularized logistic regression (Ridge).

2. **Decision Tree Classifier:** - A Decision Tree model was trained.

3. **Random Forest Classifier:** - A Random Forest model was also trained and evaluated.

### 6. Hyperparameter Tuning
Random Forest was the best performing model from the models that were trained and hyperparameter tuning was done on it to improve the model's performance.
A `RandomizedSearchCV` was used to optimize the hyperparameters of the Random Forest classifier and find the best parameters. However, tuning the model did not help improve the model since the model was already performing well.

### 7. Generating Credit Scores and Categorizing Customers
The random forest model was used to predict loan default probabilities, which were scaled to a range of 0-800 to represent credit scores. After credit score calculation, customers were then classified into five categories based on their credit score:
     - **Bad Customer** (≤ 200)
     - **2nd Worst** (201 - 350)
     - **Not So Bad** (351 - 500)
     - **Ideal Guys** (501 - 700)
     - **Big Loans** (> 700)
   
## Conclusion
The project successfully predicts credit risk and categorizes customers using machine learning techniques.




