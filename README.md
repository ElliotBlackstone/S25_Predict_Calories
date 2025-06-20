# Predicting Calorie Expenditure

## Team members
[Elliot Blackstone](https://github.com/ElliotBlackstone)

# Introduction
The objective of this project is to predict calorie expenditure during a workout.  This project is an extension of my participation in the Kaggle competition ["Predict Calorie Expenditure"](https://www.kaggle.com/competitions/playground-series-s5e5/overview), which ended on May 31, 2025.


# Dataset
The training data set contains 750,000 rows with features id, Sex, Age, Weight, Body Temperature, Heart Rate, Duration, and Calories (the target) and the testing set contains 250,000 rows (with features only).  It is worth mentioning that the [dataset](https://www.kaggle.com/competitions/playground-series-s5e5/data) was generated from a deep learning model trained on the [Calories Burnt Prediction](https://www.kaggle.com/datasets/ruchikakumbhar/calories-burnt-prediction) dataset. Feature distributions are close to, but not exactly the same, as the original.



# Preprocessing and Feature Engineering
The id column is not necessary and can be deleted.  Age is of integer type and the others are of type float.  We notice in the test set that Height, Weight, Duration, and Heart_Rate only take integer values.  In the training set, Weight, Duration, and Calories only take integer values.  We then notice in the training set that all but one of 750,000 entries in both Height and Heart_Rate takes a non-integer value.  Rounding these two entries to the nearest integer, changing these columns from float to int, and deleting the id column reduces the file size of the training and testing dataset by 33%.

For feature engineering, I added body mass index, Body Temp squared, and interaction terms between all numerical features.


# Model Selection and Results
Models are scored against the true data (not available to public, you must submit to Kaggle to get a score) by root mean squared log error.  After making some simple baseline models using aggregate statistics, our best model is a gridsearch cross validated XGBoost model trained with the previous 3 weeks of adjusted demand, client ID, client mean/median/min/max, product ID, and product mean/median.  The score from Kaggle on this model was 0.491.  LightGBM is another gradient boosting method that is more efficient than XGBoost.  Computing power was an issue for the project, so using the same predictors to train a LightGBM model, our score improved to 0.477.  For reference, the best score on the Kaggle leaderboard is 0.442.


# Files

## CSV files:
See the [Kaggle competition](https://www.kaggle.com/competitions/grupo-bimbo-inventory-demand/data) to download the datasets.

## Notebooks:
[2_town_state.ipynb](https://github.com/ElliotBlackstone/EWinter25_Product_Inventory/blob/main/2_town_state.ipynb) produces location based heat maps of client sales\
[simple_models.ipynb](https://github.com/ElliotBlackstone/EWinter25_Product_Inventory/blob/main/simple_models.ipynb) contains 4 different simple models that are based off of aggregate statistics\
[xgboost_final_EB.ipynb](https://github.com/ElliotBlackstone/EWinter25_Product_Inventory/blob/main/xgboost_final_EB.ipynb) is a well explained notebook of one of our top models\
[xgboost_final_minmaxgrid_EB.ipynb](https://github.com/ElliotBlackstone/EWinter25_Product_Inventory/blob/main/xgboost_final_minmaxgrid_EB.ipynb) is a slight improvement of the model in the previous file, which produced our top score with XGBoost\
[lgb-prediction.ipynb](https://github.com/ElliotBlackstone/EWinter25_Product_Inventory/blob/main/lgb-prediction.ipynb) uses the same predictors as our best XGBoost model but scores better

## Folder:
The folder 'etc' contained many files with poor notation that were used to build our understanding of the dataset and various models.
