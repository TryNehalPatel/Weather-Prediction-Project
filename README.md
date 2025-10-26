# Weather Prediction Project

## Project Overview

This project aims to build and evaluate binary classification models to predict whether or not it will rain tomorrow based on historical weather data. The process involves loading the data, performing extensive data preprocessing (handling missing values, encoding categorical features, handling temporal features), splitting the data for training, validation, and testing, training multiple machine learning models, and evaluating their performance using various metrics and visualizations.

## Dataset

The dataset used in this project is the **Weather Dataset** from Kaggle, available at [https://www.kaggle.com/datasets/jsphyg/weather-dataset-rattle-package](https://www.kaggle.com/datasets/jsphyg/weather-dataset-rattle-package). It contains daily weather observations from various locations across Australia. The target variable is `RainTomorrow`, which indicates whether it rained on the following day.

## Steps Performed

1.  **Data Loading**: The dataset was downloaded from Kaggle using the `opendatasets` library and loaded into a pandas DataFrame.
2.  **Initial Data Exploration**: Performed an initial overview of the data, including checking data types, non-null counts, descriptive statistics, and the percentage of missing values for each column.
3.  **Handling Missing Values**:
    *   Rows with missing values in the target variable (`RainTomorrow`) and `RainToday` were removed.
    *   Columns with a high percentage of missing values (`Evaporation`, `Cloud9am`) were dropped after examining their relationship with the target.
    *   Missing values in the remaining numerical columns were imputed with the median.
    *   Missing values in the remaining categorical columns were imputed with the mode.
4.  **Handling Temporal Features**:
    *   The `Date` column was converted to datetime objects.
    *   `Year` and `Month` were extracted from the `Date` column.
    *   A `TimeIndex` feature was created from the `Year` column (Year - Baseline Year). We commented this section out later as it didn't increase accuray.
    *   Cyclical features (`Month_sin`, `Month_cos`) were created from the `Month` column.
    *   The original `Date`, and `Month` columns were dropped. `Year` column was needed to divide the data for training\val\test sets which is discussed later. 
5.  **Encoding Categorical Features**: Categorical features (`Location`, `WindGustDir`, `WindDir9am`, `WindDir3pm`, `RainToday`) were One-Hot Encoded.
6.  **Data Scaling**: Numerical features were scaled using `StandardScaler`.
7.  **Data Splitting**: The data was split into training, validation, and test sets based on the `Year` column to maintain temporal order (Train: 2007-2014, Val: 2015-2016, Test: 2017).
8.  **Model Evaluation**: Multiple binary classification models (Logistic Regression, Decision Tree, Random Forest) were evaluated on the training and validation sets using a custom evaluation function.
9.  **Model Analysis**: The performance of the models was analyzed using:
    *   Feature Importance (for Random Forest)
    *   Confusion Matrix (for Random Forest)
    *   Classification Report (for Random Forest)
    *   ROC Curves and AUC scores (for all models), visualized interactively using Plotly.

## Key Findings

*   The Random Forest model achieved the highest performance among the evaluated models based on the ROC AUC score (approximately 0.8681), indicating good discriminatory power.
*   Feature importance analysis showed that `Humidity3pm`, `Sunshine`, `Pressure3pm`, and `Humidity9am` were among the most important features for the Random Forest model.
*   The confusion matrix and classification report provided detailed insights into the Random Forest model's performance on predicting both rainy and non-rainy days.

## Next Steps (Potential)

*   Hyperparameter tune the best-performing model (Random Forest).
*   Evaluate the final selected model on the unseen test set (2017 data).
*   Explore other advanced classification models.
*   Implement a scikit-learn pipeline for streamlined preprocessing and modeling.
*   Save or deploy the trained model.

