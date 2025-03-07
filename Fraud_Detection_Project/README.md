# Credit Card Fraud Detection

## Project Overview
This project focuses on detecting fraudulent transactions in a credit card dataset using machine learning techniques. The dataset is highly imbalanced, meaning fraudulent transactions are rare compared to legitimate ones. To address this issue, the project applies Synthetic Minority Over-sampling Technique (SMOTE) to balance the dataset and improve model performance.

## Objective
The goal of this project is to build a classification model that can accurately distinguish between fraudulent and non-fraudulent transactions. The models are evaluated using various performance metrics to ensure their reliability and effectiveness.

## Methodology

### 1. Exploratory Data Analysis (EDA)
Exploratory data analysis was conducted to get an overview of the data, its distribution, key trends and patterns as well as its linear separability.

### 2. Feature Scaling
The **Amount** column was scaled using `RobustScaler()` sice it had outliers, while the **Time** column is normalized using `MinMaxScaler()` since it is not normally distributed.

### 3. Handling Class Imbalance with SMOTE
The data is split into 80% training data and 20% testing data. The target variable was highly imbalanced, with very few fraudulent transactions. SMOTE (Synthetic Minority Over-sampling Technique) was applied on the training dataset in order to generate synthetic samples of the minority class, while keeping the testing set imbalanced so as to maintain the authenticity of the original dataset.

### 4. Model Training and Evaluation
A Random Forest Classifier was trained on the balanced dataset and the model made predictions on the test set. Performance metrics such as accuracy, precision, recall and f1-Score** were calculated in order to assess the performance of the model. Lastly a precision-recall curve was plotted to visualize precision and recall trade-offs.

### 5. Hyperparameter Tuning using Randomized Search
The Random Forest model was optimized using `RandomizedSearchCV()`. The best hyperparameters were identified, and the model is retrained with these parameters. The optimized model is then evaluated again using variousperformance metrics.

### 6. Model Performance Analysis
A classification report and confusion matrix are generated to analyze the model's predictions. A heatmap of the Confusion Matrix was also plotted for better visualization of the model's predictions.

## Conclusion
This project detects fraudulent transactions using machine learning. The combination of SMOTE for balancing the dataset, feature scaling, Random Forest classification, and hyperparameter tuning results in an effective fraud detection model. Future improvements could involve testing additional models, or using deep learning approaches.
