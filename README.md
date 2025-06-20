# Predicting Inventory Demand

## Team members
[Elliot Blackstone](https://github.com/ElliotBlackstone)\
[Amirhossein Tavakoli](https://github.com/amirhosseintavakoli)

# Introduction
We travel back in time to participate in the Kaggle competition [Grupo Bimbo Inventory Demand](https://www.kaggle.com/competitions/grupo-bimbo-inventory-demand/data), which ended in August 2016.  [Grupo Bimbo](https://www.grupobimbo.com/) is a large Mexican company that sells baked goods all over the world.  The objective of this competition is to predict the demand of various baked goods purchased by various clients on a week to week basis.


# Dataset
The training dataset is provided by Grupo Bimbo and has roughly 75 million entries.  The target variable is adjusted demand and 10 predictor variables are provided with the dataset.  Noteworthy variables are client ID, product ID, and week number (3 through 9).  The goal is to predict the adjusted demand for nearly 7 million client/product combinations in weeks 10 and 11.  An important caveat about this dataset is that many client/product combinations do not appear in every week (e.g. client X buys product Y in weeks 3, 4, and 8).  New clients and new products can appear in weeks 10 and 11 so models must be able to handle the appearance of new data.


# Preprocessing
We have two preprocessing steps.  First, we create an ID for each client/product combination in the training and test data.  This useful as the ID can be used to easily determine if a client/product combination is in the training set and/or test set.  Our second step is to compute the aggregate statistics of each client and each product.


# Model Selection and Results
Models are scored against the true data (not available to public, you must submit to Kaggle to get a score) by root mean squared log error.  After making some simple baseline models using aggregate statistics, our best model is a gridsearch cross validated XGBoost model trained with the previous 3 weeks of adjusted demand, client ID, client mean/median/min/max, product ID, and product mean/median.  The score from Kaggle on this model was 0.491.  LightGBM is another gradient boosting method that is more efficient than XGBoost.  Computing power was an issue for the project, so using the same predictors to train a LightGBM model, our score improved to 0.477.  For reference, the best score on the Kaggle leaderboard is 0.442.


# Files

## CSV files:
Due to the size of the dataset, it can't be uploaded to Github.  See the [Kaggle competition](https://www.kaggle.com/competitions/grupo-bimbo-inventory-demand/data) to download the datasets.

## Notebooks:
[2_town_state.ipynb](https://github.com/ElliotBlackstone/EWinter25_Product_Inventory/blob/main/2_town_state.ipynb) produces location based heat maps of client sales\
[simple_models.ipynb](https://github.com/ElliotBlackstone/EWinter25_Product_Inventory/blob/main/simple_models.ipynb) contains 4 different simple models that are based off of aggregate statistics\
[xgboost_final_EB.ipynb](https://github.com/ElliotBlackstone/EWinter25_Product_Inventory/blob/main/xgboost_final_EB.ipynb) is a well explained notebook of one of our top models\
[xgboost_final_minmaxgrid_EB.ipynb](https://github.com/ElliotBlackstone/EWinter25_Product_Inventory/blob/main/xgboost_final_minmaxgrid_EB.ipynb) is a slight improvement of the model in the previous file, which produced our top score with XGBoost\
[lgb-prediction.ipynb](https://github.com/ElliotBlackstone/EWinter25_Product_Inventory/blob/main/lgb-prediction.ipynb) uses the same predictors as our best XGBoost model but scores better

## Folder:
The folder 'etc' contained many files with poor notation that were used to build our understanding of the dataset and various models.
