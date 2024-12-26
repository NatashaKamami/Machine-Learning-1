# ANALYSIS OF BANK MARKETING CAMPAIGN SUCCESS
## Problem Statement: Predicting the likelihood that a customer will subscribe to a term deposit. 

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
- **Day**: The last contact day of the week.
- **Month**: The last contact month of the year.
- **Duration**: Last contact duration in seconds.
- **Campaign**: Number of contacts performed during this campaign for a customer.
- **Pdays**: Number of days that passed by after the customer was last contacted from a previous campaign.
- **Previous**: Number of contacts performed before this campaign for a customer.
- **Poutcome**: Outcome of the previous marketing campaign.
- **Deposit**: (The target variable) where: 1 indicates the customer subscribed to the term deposit and 0 indicates they did not.

## Exploratory Data Analysis
1. **Description of summary statistics for our numeric columns**: Helps us get an overview of our data and helps in identifying outliers in our data.
  ![image](https://github.com/user-attachments/assets/aec54db6-d427-442c-b328-0a5fa759e2a9)

2. **Distribution plots for the numeric columns**: Displays distribution of values in the numeric columns and can show presence of outliers.
   ![image](https://github.com/user-attachments/assets/2a73c9bf-9ccf-4d5d-bb11-39156580095c)
   ![image](https://github.com/user-attachments/assets/9e9d8f47-87d6-4816-b648-7a5aaf55f1c9)
   ![image](https://github.com/user-attachments/assets/d6ccc81d-ec64-4ba3-85b4-f8105d1cd27e)

3. **Pairplot for the numeric columns depending on deposit**: Investigates whether or not our data is linearly separable into the 2 different classes.
   ![image](https://github.com/user-attachments/assets/d12de381-eb62-421c-bc66-baad0c87f135)
   ![image](https://github.com/user-attachments/assets/79626a18-4f3a-4678-9724-261bce478156)
   ![image](https://github.com/user-attachments/assets/3073e91d-3aa2-456a-af0b-b28beb3c7f3c)

4. **Countplot of the deposit column**: Visualizes the class imbalance in the target variable.
   ![image](https://github.com/user-attachments/assets/bbfd8bc3-985d-436a-89c4-65e1d899cddc)

## Data PreProcessing
1. **Encoding**: Label encoding was used for columns with binary variables i.e yes and no, while one-hot encoding was used for columns with multiple categories since label encoding in such columns may introduce an unintended ordinal relationship.
2.  **Feature Scaling**: Standard Scaling was used in the age column since data was normally distributed, MinMax Scaling was used in the day column since data was not normally distributed while robust scaling was used in all the other numeric columns(balance, duration, campaign, previous, pdays) since data in these columns had outliers and was also not normally distributed.
3.  **Handling Imbalanced Data**: Sythetic Minority Oversamping Technique(SMOTE) was used to generate sythetic samples for the minority class so that the data can be balanced.
   
   ![image](https://github.com/user-attachments/assets/061213c8-d124-41db-a943-d70d866acdd9)

## Selecting and Training the model
- **Splitting the data into training, validation and training sets**: 60% for training, 20% for validation and 20% for testing.
  ![image](https://github.com/user-attachments/assets/46e577db-52ff-498d-95b8-4400f42e5f40)

### Baseline Models
To see which classification model works best and also see the performance of the models before hyperparameter tuning is done.
- **1. Logistic Regression**

![image](https://github.com/user-attachments/assets/1278ba7a-6c32-4f25-826a-ef7adc7184a4)
- **2. Support Vector Machine - Linear Kernel**

![image](https://github.com/user-attachments/assets/023af4b7-cb25-49ff-a6c4-d9ac9b9b38d3)
- **3. Support Vector Machine - RBF Kernel**

![image](https://github.com/user-attachments/assets/9a477cb6-5c99-4cd1-aa4d-79f4d9781e86)
- **4. Decision Tree Classifier**

![image](https://github.com/user-attachments/assets/f112ff37-8dfd-4088-bb41-7024038c0e02)
- **5. Random Forest Classifier**

![image](https://github.com/user-attachments/assets/cd34b2fa-3c97-4f47-a8c0-85c536584da8)
- **6. XG Boost Classifier**

![image](https://github.com/user-attachments/assets/f5cfbe9c-1bac-40e7-908f-83113129ea0b)

From the performance metrics in each of the models, we can see that the random forest classifier performs the best and is the best model to tune in order to enhance its performance.

### Hyper parameter tuning the best model
Hyper parameter tuning was done using Randomized Search CV
![image](https://github.com/user-attachments/assets/6516a8b9-0327-44ae-b4e2-35d1f4a1d9b9)

On comparing our F1 score of the baseline random forest moddl and the tuned model, the F1 is higher in the tuned model hence hyperparameter tuning has enhanced our model performance and withe the same parameters we will make predictions on our test set to see if our model performs just as well on the unseen data.

### Final evaluation on the test set
![image](https://github.com/user-attachments/assets/919f1344-5a6b-4daf-b6fa-e5bcc32270a6)

Judging from the performance metrics from evaluation on the test set, we can see that the model works just as fine on new data as it did on the training data.

### Evaluating the tuned model using the precision-recall curve
![image](https://github.com/user-attachments/assets/b031c92d-90ab-48b1-9c89-9a256e206bdb)

The Area under the above curve provides a better understanding of how well the model is detecting the minority class.
An AUC-PR of 0.99 means that the model achieves near-perfect precision and recall for the positive clasd suggesting that the model is correctly identifying most of the positive instances (high recall) while also minimizing false positives (high precision).

