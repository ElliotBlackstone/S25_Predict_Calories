# Predicting Calorie Expenditure

# Introduction
The objective of this project is to predict calorie expenditure during a workout.  This project is an extension of my participation in the Kaggle competition "[Predict Calorie Expenditure](https://www.kaggle.com/competitions/playground-series-s5e5/overview)", which ended on May 31, 2025.


# Dataset
The training data set contains 750,000 rows with features id, Sex, Age, Weight, Body Temperature, Heart Rate, Duration, and Calories (the target) and the testing set contains 250,000 rows (with features only).  It is worth mentioning that the [dataset](https://www.kaggle.com/competitions/playground-series-s5e5/data) was generated from a deep learning model trained on the [Calories Burnt Prediction](https://www.kaggle.com/datasets/ruchikakumbhar/calories-burnt-prediction) dataset. Feature distributions are close to, but not exactly the same, as the original.



# Preprocessing and Feature Engineering
Our preprocessing is comprised of the following steps:
-	Log transform Calories
-	One-hot encoding for gender and recast as categorical type
-	Delete id column
-	Change height, weight, duration, heart rate from float to int

Notably, in the last step, only 1 value of heart rate and height was non-integer, so these were rounded to the nearest integer.  These preprocessing steps reduced file size by roughly 10.5%.

For feature engineering, I added body mass index, Body Temp squared, and interaction terms between all numerical features.


# Model Selection and Results
Models are scored against the true data (not available to public, you must submit to Kaggle to get a score) by root mean squared log error (RMSLE).  Optuna was used for hyperparameter selection in XGBoost, LightGBM, and CatBoost models.

| Model | Feature Engineering | RMSLE | LB (out of 4318) |
|----------|:--------:|:---------:|:---------:|
| Linear Regression | No | 0.17926 | 4025 |
| Linear Regression | Yes | 0.09431 | 3826 |
| GAM | No | 0.08945 | 3811 |
| GAM | Yes | 0.06949 | 3605 |
| XGBoost | Yes | 0.05922 | 1324 |
| LightGBM | Yes | 0.05921 | 1314 |
| CatBoost | Yes | 0.05903 | 1050 |
| Ensemble* | N/A | 0.05879 | 678 |
| AutoGluon | No | 0.05846 | 4 |

*: The ensemble model was comprised of the XGBoost, LightGBM, and CatBoost models.

The AutoGluon model is a stacked ensemble of CatBoost, XGBoost, LightGBM, RandomForest, ExtraTrees, and NN models.  It is the simplest top performing model on the Kaggle leaderboard.

# Files

## Package requirements:
[requirements.txt](https://github.com/ElliotBlackstone/S25_Predict_Calories/blob/main/requirements.txt)

## CSV files:
See the [Kaggle competition](https://www.kaggle.com/competitions/playground-series-s5e5/data) to download the datasets.

## Notebooks:
[calorie_preprocess.ipynb](https://github.com/ElliotBlackstone/S25_Predict_Calories/blob/main/calorie_preprocess.ipynb) preprocessing and reduce dataset file size by 10.5%\
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
[Optuna_databases](https://github.com/ElliotBlackstone/S25_Predict_Calories/tree/main/Optuna_databases) contains databases from Optuna studies

## Erdős Files:
[Exec_Summary_calorie.pdf](https://github.com/ElliotBlackstone/S25_Predict_Calories/blob/main/Exec_Summary_calorie.pdf) Executive summary\
[PredCalExp_slides.pdf](https://github.com/ElliotBlackstone/S25_Predict_Calories/blob/main/PredCalExp_slides.pdf) Powerpoint slides
