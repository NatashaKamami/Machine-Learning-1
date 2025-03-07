# Chip Data Analysis and Classification

## Project Overview
This project focuses on analyzing semiconductor chip data, including CPUs and GPUs, to understand trends in transistor counts, performance, and market insights. It also includes a machine learning model to classify chip types based on key characteristics.

## Methodology
### 1. Data Cleaning & Handling Missing Values
- Dropped the following columns, 'FP16 GFLOPS', 'FP32 GFLOPS', 'FP64 GFLOPS' due to excessive missing data.
- Dropped records where both 'Die Size (mm^2)' and 'Transistors (million)' were missing, where both 'TDP (W)' and 'Freq (GHz)' were missing and where 'Release Date' or 'Process Size (nm)' were missing because missingness in these rows was not completely random hence imputing them would mess with the integrity of the data.
- Filled the remaining missing values with either median or mode depending on the data type.

### 2. Exploratory Data Analysis (EDA)
1. **Moore's Law Analysis**: Visualizing transistor count over time.
2. **Dennard Scaling**: Analyzing power consumption relative to die size.
3. **Frequency Trends**: Comparing CPU and GPU frequency evolution.
4. **GPU Performance Trends**: Measuring improvement in GPU performance over time.
5. **Technology Adoption**: High-end GPUs use the latest semiconductor technology first.
6. **Process Size Distribution**: Comparing chip manufacturers' process sizes.
7. **Market Share Analysis**: Identifying the top foundries in chip manufacturing.
8. **Feature Correlations**: Heatmap visualization of feature relationships.

### 3. Feature Engineering & Encoding
- **One-Hot Encoding**: Applied to categorical features.
- **Label Encoding**: Used for ordinal features like 'Release Date'.
- **Feature Scaling**: Min-Max scaling applied to all the numerical features.

### 4. Machine Learning Models
The data was split into 80% training data and 20% testing data. A number of classification models were trained including: Logistic Regression and Random Forest Classifier. 
Both models were evaluated using accuracy score and the ROC-AUC score, and a classification report for each model was also given for model comparison.
Lastly, an ROC curve was plotted to to assess the models' ability to correctly classify semiconductor chips and to also visually compare their performance.

## Key Insights
- Moore's Law and Dennard Scaling remain relevant in chip evolution.
- GPUs are catching up with CPUs in frequency improvements.
- GPU performance improvement is driven by smaller transistors, larger die sizes, and higher clock speeds.
- Leading manufacturers like Intel, AMD, and Nvidia use the latest semiconductor technology.
- TSMC leads in chip production worldwide.

## Conclusion
This project provides insights into the evolution of semiconductor chips and uses a predictive model for chip classification. It combines data analysis, visualization, and machine learning techniques to explore trends in the chip industry.


