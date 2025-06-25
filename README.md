# Predicting Calorie Expenditure

# Introduction
The objective of this project is to predict calorie expenditure during a workout.  This project is an extension of my participation in the Kaggle competition "[Predict Calorie Expenditure](https://www.kaggle.com/competitions/playground-series-s5e5/overview)", which ended on May 31, 2025.


# Dataset
The training data set contains 750,000 rows with features id, Sex, Age, Weight, Body Temperature, Heart Rate, Duration, and Calories (the target) and the testing set contains 250,000 rows (with features only).  It is worth mentioning that the [dataset](https://www.kaggle.com/competitions/playground-series-s5e5/data) was generated from a deep learning model trained on the [Calories Burnt Prediction](https://www.kaggle.com/datasets/ruchikakumbhar/calories-burnt-prediction) dataset. Feature distributions are close to, but not exactly the same, as the original.



# Preprocessing and Feature Engineering
The id column is not necessary and can be deleted.  Age is of integer type and the others are of type float.  We notice in the test set that Height, Weight, Duration, and Heart_Rate only take integer values.  In the training set, Weight, Duration, and Calories only take integer values.  We then notice in the training set that all but one of 750,000 entries in both Height and Heart_Rate takes a non-integer value.  Rounding these two entries to the nearest integer, changing these columns from float to int, and deleting the id column reduces the file size of the training and testing dataset by 33%.

For feature engineering, I added body mass index, Body Temp squared, and interaction terms between all numerical features.


# Model Selection and Results
Models are scored against the true data (not available to public, you must submit to Kaggle to get a score) by root mean squared log error (RMSLE).  Optuna was used for optimal feature selection in linear regression and GAM and for hyperparameter selection in XGBoost, LightGBM, and CatBoost models.

| Model | Feature Engineering | Feature Selection | RMSLE | LB (out of 4318) |
|----------|:--------:|:---------:|:---------:|:---------:|
| Linear Regression | No | No | 0.45056 | 4103 |
| Linear Regression | No | Yes | 0.34825 | 4083 |
| Linear Regression | Yes | Yes | 0.08976 | 3812 |
| GAM | No | No | 0.08945 | 3811 |
| GAM | No | No | 0.06949 | 3605 |
| XGBoost | Yes | No | 0.05922 | 1324 |
| LightGBM | Yes | No | 0.05921 | 1314 |
| CatBoost | Yes | No | 0.05906 | 1090 |
| Ensemble* | N/A | N/A | 0.05879 | 678 |
| AutoGluon | No | No | 0.05846 | 4 |

*: The ensemble model was comprised of the XGBoost, LightGBM, and CatBoost models.

The AutoGluon model is a stacked ensemble of CatBoost, XGBoost, LightGBM, RandomForest, ExtraTrees, and NN models.  It is the simplest top performing model on the Kaggle leaderboard.

# Files

## CSV files:
See the [Kaggle competition](https://www.kaggle.com/competitions/playground-series-s5e5/data) to download the datasets.

## Notebooks:
[calorie_compress.ipynb](https://github.com/ElliotBlackstone/S25_Predict_Calories/blob/main/calorie_compress.ipynb) reduce dataset file size by 33%\
[calorie_EDA.ipynb](https://github.com/ElliotBlackstone/S25_Predict_Calories/blob/main/calorie_EDA.ipynb) exploratory data analysis\
[calorie_LinReg.ipynb](https://github.com/ElliotBlackstone/S25_Predict_Calories/blob/main/calorie_LinReg.ipynb) linear regression models with Optuna for feature selection\
[calorie_gam.ipynb](https://github.com/ElliotBlackstone/S25_Predict_Calories/blob/main/calorie_gam.ipynb) GAMs with Optuna for feature selection\
[calorie_autogluon.ipynb](https://github.com/ElliotBlackstone/S25_Predict_Calories/blob/main/calorie_autogluon.ipynb) top performing AutoGluon model with SHAP for explainability\
[calorie_catboost.ipynb](https://github.com/ElliotBlackstone/S25_Predict_Calories/blob/main/calorie_catboost.ipynb) CatBoost model with SHAP for explainability\
[calorie_xgboost.ipynb](https://github.com/ElliotBlackstone/S25_Predict_Calories/blob/main/calorie_xgboost.ipynb) XGBoost model with SHAP for explainability\
[calorie_lightGBM.ipynb](https://github.com/ElliotBlackstone/S25_Predict_Calories/blob/main/calorie_lightGBM.ipynb) LightGBM model with SHAP for explainability\
[calorie_ensemble.ipynb](https://github.com/ElliotBlackstone/S25_Predict_Calories/blob/main/calorie_ensemble.ipynb) Ensemble model of XGBoost, LightGBM, CatBoost

## Folders:
[catboost_info](https://github.com/ElliotBlackstone/S25_Predict_Calories/tree/main/catboost_info) contains files automatically generated while training CatBoost models\
[Optuna databases]() contains databases from Optuna studies
