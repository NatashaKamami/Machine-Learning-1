# ANALYSIS OF BANK MARKETING CAMPAIGN SUCCESS
## Problem Statement: Predicting the likelihood that a customer will subscribe to a term deposit. 
A **term deposit**, also known as a fixed deposit, is a type of financial product offered by banks or financial institutions where an individual deposits a certain amount of money for a fixed period at a predetermined interest rate.

## Data Overview:
The Data used is from: https://archive.ics.uci.edu/dataset/222/bank+marketing.  
It contains information about customers, and the target variable is whether or not the customer subscribed to a term deposit.  
The data includes the following columns:
- **Age**: The age of the customer.
- **Job**: The customer's job.
- **Marital**: Marital status of the customer.
- **Education**: Customer's level of education.
- **Default**: Whether the customer has credit default.
- **Housing**: Whether the customer has a housing loan.
- **Loan**: Whether the customer has a personal loan.
- **Contact**: Communication type used to contact the customer.
- **Day of Week**: Last contact day of the week.
- **Month**: The last contact month of the year.
- **Duration**: Last contact duration in seconds.
- **Campaign**: Number of contacts performed during this campaign for a customer.
- **Pdays**: Number of days that passed by after the customer was last contacted from a previous campaign.
- **Previous**: Number of contacts performed before this campaign for a customer.
- **Poutcome**: Outcome of the previous marketing campaign.
- **Employment Variation Rate**: Quarterly indicator that measures the percentage change in employment compared to the previous period.
- **Consumer Price Index (CPI)**: Measures the average change in the prices paid by consumers for goods and services. It's a key indicator of inflation.
- **Consumer Confidence Index**: Measures consumer optimism about the economic situation. Higher values indicate greater confidence in economic conditions.
- **3-Month Euribor Rate**: The 3-month Euro Interbank Offered Rate, which is the average interest rate at which European banks lend to each other.
- **Number of Employees**: Measures the total number of people employed in the economy.
- **Deposit**: (The target variable) where: 1 indicates the customer subscribed to the term deposit and 0 indicates they did not.

## Exploratory Data Analysis
1. **Description of summary statistics for our numeric columns**: Provides an overview of the data by highlighting its range, spread, and potential outliers.  
![image](https://github.com/user-attachments/assets/3076acbf-e6aa-4c7b-b1e8-22166e5cae22)


2. **Distribution plots for the numeric columns**: Visualize how values are distributed across numeric columns revealing skewness and the presence of outliers.
![image](https://github.com/user-attachments/assets/0a25b7ac-99a4-454b-b330-244dba3b62a9)
![image](https://github.com/user-attachments/assets/fb4a97fb-95bc-4617-88ca-c52531973153)


3. **Pairplot for selected numeric columns depending on deposit**: Explores relationships between some numeric columns by identifying potential outliers, patterns and correlations, and also investigates whether the classes of the target variable are linearly separable.
![image](https://github.com/user-attachments/assets/eea5357d-3ec9-4bc6-8bb7-eef9d639cd64)
![image](https://github.com/user-attachments/assets/658b26c2-4a91-4614-97c8-cd548671301d)
![image](https://github.com/user-attachments/assets/61f22918-8050-4e38-b55c-78ff2bb82022)


4.**Correlation Matrix**: Explores relationships that may exist between the numeric columns.
![image](https://github.com/user-attachments/assets/f25f746e-df79-48dc-b0d7-17665914f235)


5.  **Countplot of the deposit column**: Visualizes the class imbalance in the target variable.
![image](https://github.com/user-attachments/assets/85335882-5ed3-42ae-bbc1-4ae21251ec8e)


## Data PreProcessing
1. **Encoding**: Label encoding was used for the deposit column which had binary variables i.e yes and no, while one-hot encoding was used for all the other categorical columns that had multiple categories since label encoding in such columns may introduce an unintended ordinal relationship.
2.  **Feature Scaling**: Standard Scaling was used in the age column since data was normally distributed, MinMax Scaling was used in the employment variation rate, consumer price index, consumer confidence index, 3-Month Euribor Rate, Number of employees columns since data was not normally distributed while robust scaling was used in all the other numeric columns(duration, campaign, previous, pdays) since data in these columns had extreme outliers and was also not normally distributed.
3.  **Splitting the data into training, validation and training sets**: 60% for training, 20% for validation and 20% for testing.
![image](https://github.com/user-attachments/assets/8a05d90d-634b-4b2c-867b-f3afdbad3a06)

4.  **Handling Imbalanced Data**: Sythetic Minority Oversamping Technique(SMOTE) was used to generate sythetic samples for the minority class in the training data so that the data can be balanced.  
![image](https://github.com/user-attachments/assets/2ee3c340-462d-457c-bfe6-dc970f2a61d9)

 
## Selecting and Training the model
### Baseline Models
To determine the best-performing classification models and evaluate their performance before hyperparameter tuning, the F1 score was chosen as the evaluation metric. Given that the dataset is imbalanced, and identifying customers who subscribe to the term deposit is more critical than identifying those who don't (i.e one class is more important), the F1 score is particularly useful since it balances precision and recall, ensuring the model performs well in minimizing both false positives and false negatives. 

- **1. Logistic Regression**

![image](https://github.com/user-attachments/assets/45d8f81d-4c4e-4a04-abe4-0fccab9dd0b5)

- **2. Support Vector Machine - Linear Kernel**

![image](https://github.com/user-attachments/assets/0a49cd0b-3b97-4b86-a72b-c24ffbc83d50)

- **3. Support Vector Machine - RBF Kernel**

![image](https://github.com/user-attachments/assets/78687b8c-3760-46ab-829d-bca9ac2f2261)

- **4. Decision Tree Classifier**
  
![image](https://github.com/user-attachments/assets/d87861ef-19e8-416b-a7a6-c7aceb2721d0)

- **5. Random Forest Classifier**

![image](https://github.com/user-attachments/assets/2b76efda-c00e-404f-9101-23a3ddf0fbe6)


Random Forest stands out as the best performing model. 

### Hyper parameter tuning the best model
Hyper parameter tuning was done using Randomized Search CV

![image](https://github.com/user-attachments/assets/3d5714f1-b498-482a-a41e-e3385bc9582f)


The F1 score of the tuned Random Forest model is a lot higher than that of the baseline model, indicating that hyperparameter tuning has improved its performance. This makes the tuned Random Forest model an optimal choice for our analysis. Using these optimized parameters, we will now evaluate the model on the test set to see if it performs equally well on unseen data.

### Final evaluation on the test set
![image](https://github.com/user-attachments/assets/b64746b4-8859-4bd5-87a8-f4fcf956e85f)


The F1 score from the evaluation on the test set is a bit lower than that from the validation set. The f1 score is above average hence showing that the model performs well on new, unseen data.

### Evaluating the tuned model using the precision-recall curve
![image](https://github.com/user-attachments/assets/90cbc4a3-6ddc-4692-85ec-b689401ae375)


The above curve provides a better understanding of how well the model is at detecting the minority class(positive class). An AUC-PR of 0.60 means that the model achieves a moderate trade-off between precision and recall for the positive class suggesting that the model has a moderate ability to correctly identify the minority class without overwhelming false positives. For an imbalanced dataset like this, the PR AUC of a random classifier equals the prevalence of the positive class and in this case the minority class represents 11% of the dataset, a PR AUC of 0.11 would be the baseline for random guessing therefore a PR AUC of 0.60 is well above the baseline, indicating the model is successfully learning patterns in the data.


## Error Analysis
### Confusion Matrix
![image](https://github.com/user-attachments/assets/11decdf9-f316-4912-9d0c-207c82f20e97)


The confusion matrix evaluates the performance of the classification model by visualizing how well the model's predictions match the actual values. It helps identify where the model is making mistakes by showing the false positives and false negatives.

### Error rate by class
![image](https://github.com/user-attachments/assets/dbbaa04e-e879-46a9-be61-c8998c362cae)



The visualization shows how often the model makes errors when classifying each class, which helps us understand whether the model is more prone to misclassifying one class over the other.
Error rate of 0.063312 means around 6.3% of class 0 samples were misclassified.
Error rate of 0.352432 means around 35.2% of class 1 samples were misclassified.
This highlights that our model is more likely to misclassify class 1 samples i.e classifying false negatives. 
The model performs better on Class 0 (non-subscribers) but struggles with Class 1 (subscribers). Which highlights the imbalance in the dataset, where the majority class dominates, making it harder for the model to correctly identify the minority class resulting in higher false negatives. 
For a bank marketing campaign, this means potential revenue is lost due to missed opportunities with actual subscribers that were misclassified.

### Validation Curve

![image](https://github.com/user-attachments/assets/5ea452d9-4f18-48f0-8ca0-24069edac6d9)

The validation curve shows how the model's performance changes as the number of trees (n_estimators) increases.
The training F1-score starts very high (0.998) and quickly reaches 1 as the number of trees increases, meaning the model fits the training data almost perfectly. However, this could signal overfitting, where the model is memorizing the training data.
The validation F1-score starts at around 0.943 and plateaus at 0.948, showing that the model generalizes reasonably well but has a gap compared to the training score. The plateau indicates that increasing the number of trees beyond 120 does not significantly improve the model's performance.
