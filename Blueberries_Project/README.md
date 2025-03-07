# Blueberries Yield Prediction Project

## Project Overview
Using machine learning techniques, the model estimates yield values by analyzing past data and applying regression techniques. This project aims to predict agricultural yield based on various factors. These factors include:
- Pollinator Factors: The dataset includes information on different pollinators such as honeybees, bumblebees, andrena, and osmia.
- Temperature Ranges: Maximum, minimum, and average upper and lower temperature ranges are included.
- Rainfall Patterns: The number of raining days and the average amount of rainfall.
- Fruit and Seed Data: Features like fruit set, fruit mass, and seed counts.
- Clone Size: Represents the size of the plant clone.
  
## Methodology

### 1. Data Preprocessing
- The dataset is analyzed for missing values and the data types of each colimn are checked.
- Features and target variables are identified.
- The training dataset is split into training and validation sets.

### 2. Exploratory Data Analysis (EDA)
A correlation heatmap is plotted to understand feature relationships and this also influenced feature selection. Features with high correlation were left out of the model and only one of the features with a strong relationship was included in the model.

### 3. Model Training 
The following regression models were implemented and the performance of each model was evaluated using Mean Absolute Error (MAE):

- **Linear Regression** - Fits a simple linear regression model to the data.

- **Polynomial Regression** -  Incorporates polynomial features into linear regression.

- **Lasso Regression** - Implements Lasso regression (L1 regularization) to reduce overfitting.

- **Ridge Regression** - Implements Ridge regression  (L2 regularization) to prevent overfitting.

- **Elastic Net Regression** - Combines both L1 and L2 regularization techniques to determine the optimal balance between the two.

### 4. Model Selection and Prediction
- The best-performing model is selected based on the lowest MAE.
- Predictions are made on the test dataset using this best performing model.

### 5. Output and Submission
The final predictions are saved into a CSV file (`submission.csv`) which contains the predicted yield values for the test dataset.

## Conclusion
This project applies multiple regression techniques to predict yield based on environmental and pollination factors. The best-performing model is then chosen based on MAE, and predictions are made on the test set.


