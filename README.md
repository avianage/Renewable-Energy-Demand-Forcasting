# Energy Load Forecasting and Modeling

This repository contains a comprehensive project for forecasting energy load using machine learning and time series analysis techniques. The project demonstrates a complete workflow—from data preprocessing and feature engineering to model training, evaluation, and visualization using Random Forest, XGBoost, and ARIMA.

## Table of Contents

- [Overview](#overview)
- [Data Preparation and Feature Engineering](#data-preparation-and-feature-engineering)
- [Modeling](#modeling)
  - [Random Forest](#random-forest)
  - [XGBoost](#xgboost)
  - [ARIMA](#arima)
- [Model Evaluation and Visualization](#model-evaluation-and-visualization)
- [Dependencies](#dependencies)
- [Usage](#usage)

## Overview

This project forecasts energy load based on historical energy data. The process includes:
- Loading the dataset and performing exploratory data analysis.
- Extracting time-based features (e.g., day, month, hour, day of week, and season).
- Handling missing values and creating lag features to capture temporal dependencies.
- Training multiple models:
  - **Random Forest Regressor**
  - **XGBoost Regressor**
  - **ARIMA** for time series forecasting
- Evaluating the models using metrics like RMSE, MAE, MAPE, and R2 Score.
- Visualizing predictions and error distributions.

## Data Preparation and Feature Engineering

- **Loading Data:**  
  The dataset is read from a CSV file (`datasets/energy_dataset.csv`) using pandas.

- **Time Feature Extraction:**  
  - The `time` column is converted to a datetime format with UTC.
  - Additional features are derived: `day`, `month`, `hour`, and `day_of_week`.
  - A custom function assigns a season based on the month.

- **Handling Missing Values:**  
  - For columns with less than 5% missing data, missing values are imputed using the column mean.
  - Columns that are entirely missing are dropped.

- **Lag Features:**  
  - Lag features (up to 7 lags) for the target variable (`total load actual`) are created.
  - The dataset is resampled into daily and weekly aggregates, with corresponding lag features generated.
  - Additional time-based features (hour, day, month) are reintroduced after setting the datetime index.

- **Feature Selection:**  
  A set of predictors is defined that includes renewable generation data, day-ahead forecasts, price, time features, and the lagged load values. The target variable is `total load actual`.

## Modeling

### Random Forest

- A **Random Forest Regressor** is used to model the energy load.
- The data is split into training and testing sets.
- The model is trained on the training data, and predictions are generated for the test set.
- Predictions are visualized alongside actual values.

### XGBoost

- An **XGBoost Regressor** with the objective set to `reg:squarederror` is used.
- The model is similarly trained and its predictions are compared to the actual values using visualizations.

### ARIMA

- An **ARIMA** model is applied to the target variable with order (5, 1, 0).
- The model is trained on the training set and used to forecast the test set.
- A rolling window cross-validation is implemented to compute error metrics (RMSE, MAE, MAPE) for ARIMA forecasts.
- Visualizations display the forecast for one of the cross-validation windows.

## Model Evaluation and Visualization

- **Cross Validation:**  
  - Cross-validation (with cv=3) is performed for both Random Forest and XGBoost.
  - Metrics computed include RMSE, MAE, and MAPE.
  
- **Metric Calculation:**  
  - A helper function calculates evaluation metrics (RMSE, MAE, MAPE, and R2 Score) for each model.
  
- **Visualizations:**  
  - Histograms display the distribution of actual versus predicted values for each model.
  - Time series plots compare the actual energy load with predictions from Random Forest, XGBoost, and ARIMA over the test period.

## Dependencies

- **Python Libraries:**
  - `pandas`
  - `numpy`
  - `scikit-learn`
  - `xgboost`
  - `statsmodels`
  - `matplotlib`
  - `seaborn`

Make sure to install these libraries using pip if they are not already installed.

## Usage

1. **Clone the Repository:**  
   Clone this repository to your local machine.

2. **Install Dependencies:**  
   Install the required packages:
   ```bash
   pip install pandas numpy scikit-learn xgboost statsmodels matplotlib seaborn
