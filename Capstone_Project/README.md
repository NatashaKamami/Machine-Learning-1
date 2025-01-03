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
- **Balance**: The customer’s average yearly account balance.
- **Housing**: Whether the customer has a housing loan.
- **Loan**: Whether the customer has a personal loan.
- **Contact**: Communication type used to contact the customer.
- **Day**: The last contact day of the month.
- **Month**: The last contact month of the year.
- **Duration**: Last contact duration in seconds.
- **Campaign**: Number of contacts performed during this campaign for a customer.
- **Pdays**: Number of days that passed by after the customer was last contacted from a previous campaign.
- **Previous**: Number of contacts performed before this campaign for a customer.
- **Poutcome**: Outcome of the previous marketing campaign.
- **Deposit**: (The target variable) where: 1 indicates the customer subscribed to the term deposit and 0 indicates they did not.

## Exploratory Data Analysis
1. **Description of summary statistics for our numeric columns**: Provides an overview of the data by highlighting its range, spread, and potential outliers.  
  ![image](https://github.com/user-attachments/assets/aec54db6-d427-442c-b328-0a5fa759e2a9)

2. **Distribution plots for the numeric columns**: Visualize how values are distributed across numeric columns revealing skewness and the presence of outliers.
   ![image](https://github.com/user-attachments/assets/2a73c9bf-9ccf-4d5d-bb11-39156580095c)
   ![image](https://github.com/user-attachments/assets/9e9d8f47-87d6-4816-b648-7a5aaf55f1c9)
   ![image](https://github.com/user-attachments/assets/d6ccc81d-ec64-4ba3-85b4-f8105d1cd27e)

3. **Pairplot for the numeric columns depending on deposit**: Explores relationships between numeric columns by identifying potential outliers, patterns and correlations, and also investigates whether the classes of the target variable are linearly separable.
   ![image](https://github.com/user-attachments/assets/d12de381-eb62-421c-bc66-baad0c87f135)
   ![image](https://github.com/user-attachments/assets/79626a18-4f3a-4678-9724-261bce478156)
   ![image](https://github.com/user-attachments/assets/3073e91d-3aa2-456a-af0b-b28beb3c7f3c)

4. **Countplot of the deposit column**: Visualizes the class imbalance in the target variable.
   ![image](https://github.com/user-attachments/assets/bbfd8bc3-985d-436a-89c4-65e1d899cddc)

## Data PreProcessing
1. **Encoding**: Label encoding was used for columns with binary variables i.e yes and no, while one-hot encoding was used for columns with multiple categories since label encoding in such columns may introduce an unintended ordinal relationship.
2.  **Feature Scaling**: Standard Scaling was used in the age column since data was normally distributed, MinMax Scaling was used in the day column since data was not normally distributed while robust scaling was used in all the other numeric columns(balance, duration, campaign, previous, pdays) since data in these columns had outliers and was also not normally distributed.
3.  **Handling Imbalanced Data**: Sythetic Minority Oversamping Technique(SMOTE) was used to generate sythetic samples for the minority class so that the data can be balanced.
   
![image](https://github.com/user-attachments/assets/0754c24e-4bc8-4705-bab0-d83e9a2c9be5)
 
## Selecting and Training the model
- **Splitting the data into training, validation and training sets**: 60% for training, 20% for validation and 20% for testing.
  ![image](https://github.com/user-attachments/assets/46e577db-52ff-498d-95b8-4400f42e5f40)

### Baseline Models
To see which classification model works best and also see the performance of the models before hyperparameter tuning is done.
- **1. Logistic Regression**

![image](https://github.com/user-attachments/assets/622a90c2-b318-404e-a873-12947af84cf7)
- **2. Support Vector Machine - Linear Kernel**

![image](https://github.com/user-attachments/assets/6b92f6e3-9550-47b0-88e5-d9385013c246)
- **3. Support Vector Machine - RBF Kernel**

![image](https://github.com/user-attachments/assets/550f5965-e3f1-48de-844a-3843c3affa38)
- **4. Decision Tree Classifier**

![image](https://github.com/user-attachments/assets/bd8cc240-8d49-414c-a66a-6015d67c4545)

- **5. Random Forest Classifier**

![image](https://github.com/user-attachments/assets/e8fc6619-16ff-48a9-9e8a-68a5ca9bc0bc)
- **6. XG Boost Classifier**

![image](https://github.com/user-attachments/assets/565daa11-4ae6-4883-87f6-2be1fb3befad)

Since the dataset was imbalanced, and one class is more important than the other (i.e, identifying customers who subscribe to the term deposit is more important than identifying those who don't), F1 score is the evaluation metric that was used to evaluate model performance. Random Forest stands out as the best performing model due to its ability to handle complex relationships, feature interactions, and outliers, while being robust to overfitting. Logistic Regression and SVM with a linear kernel perform poorly in comparison since they assume linear separability, which limits their performance on complex datasets. Although SVM with an RBF kernel can handle non-linearity, it is computationally expensive and sensitive to hyperparameters like C hence why it did not perform as well. Decision Trees on the other hand are prone to overfitting especially with imbalanced data. And while XGBoost is powerful, it requires extensive tuning to surpass Random Forest. 

### Hyper parameter tuning the best model
Hyper parameter tuning was done using Randomized Search CV

![image](https://github.com/user-attachments/assets/5178ea9a-3930-46d5-887b-bc8a0554fa59)


The F1 score of the tuned Random Forest model is higher than that of the baseline model, indicating that hyperparameter tuning has improved its performance. This makes the tuned Random Forest model an optimal choice for our analysis. Using these optimized parameters, we will now evaluate the model on the test set to see if it performs equally well on unseen data.

### Final evaluation on the test set
![image](https://github.com/user-attachments/assets/2205fcaf-1fb9-40ff-9415-ffe598ab983b)


The F1 score from the evaluation on the test set shows that the model performs just as well on new, unseen data as it did on the training data.

### Evaluating the tuned model using the precision-recall curve
![image](https://github.com/user-attachments/assets/b031c92d-90ab-48b1-9c89-9a256e206bdb)


The above curve provides a better understanding of how well the model is at detecting the minority class(positive class). An AUC-PR of 0.99 means that the model achieves near-perfect precision and recall for the positive class suggesting that the model is correctly identifying most of the positive instances (high recall) while also minimizing false positives (high precision).


## Error Analysis
### Confusion Matrix
![image](https://github.com/user-attachments/assets/36c513d6-a517-48e0-af41-d6778c5ee71b)


The confusion matrix evaluates the performance of the classification model by visualizing how well the model's predictions match the actual values. It helps identify where the model is making mistakes by showing the false positives and false negatives.

### Error rate by class
![image](https://github.com/user-attachments/assets/47757234-f08f-4b75-8c17-2f8914c867af)


The visualization shows how often the model makes errors when classifying each class, which helps us understand whether the model is more prone to misclassifying one class over the other.
Error rate of 0.083375 means around 8.3% of class 0 samples were misclassified.
Error rate of 0.042598 means around 4.2% of class 1 samples were misclassified.
This highlights that our model is more likely to misclassify class 0 samples i.e classifying false negatives.



