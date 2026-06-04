## 🍳 Can We Predict Recipe Calories?

**By Jacey Chow, Maggie Shao**

## Overview

This data science project, conducted at UC San Diego, focuses on **predicting the calories of a recipe using recipe-level characteristics** from the Food.com dataset. In particular, the project studies whether higher-calorie recipes tend to require more preparation steps.

## Introduction

Food is an important part of everyday life, and cooking is both a practical activity and a creative outlet for many people. Recipes vary widely in the time, effort, ingredients, and nutritional content they require, and understanding these differences can help both home cooks and recipe platforms better serve their users.

The dataset we use contains over 83,000 recipes with information such as the number of preparation steps, number of ingredients, nutritional values, and user ratings. Our central question is: **Do higher-calorie recipes tend to require more preparation steps?** We are interested in understanding whether calorie-dense recipes are also more complex to prepare, and ultimately whether we can predict a recipe's calorie content based on its observable characteristics.

Answering this question can help:
- Users better understand the relationship between recipe complexity and nutritional content
- Recipe platforms surface recipes that match users' time and health preferences
- Researchers and developers build better recipe recommendation systems

### Datasets Discription
This project uses two datasets from [Food.com](https://www.food.com/):
- `RAW_recipes`: contains recipe-level information (83,782 rows)
- `interactions`: contains user ratings and reviews (731,927 rows)

These datasets were originally collected for recommender system research in the paper Generating Personalized Recipes from Historical User Preferences by Majumder et al

The most relevant columns for our analysis are:

| Column | Description |
|--------|-------------|
| `calories` | Total calories of the recipe |
| `n_steps` | Number of preparation steps |
| `n_ingredients` | Number of ingredients |
| `avg_rating` | Average user rating |
| `minutes` | Time required to prepare the recipe |


The main question we explore is:

**Do recipes with different calorie levels have different average numbers of steps?**

We also examine missingness patterns in the dataset and test whether missing values in columns such as `avg_rating` and `description` depend on other recipe features.

## Data Cleaning and Exploratory Data Analysis

## Assessment of Missingness

## Hypothesis Testing

## Framing a Prediction Problem

Our goal is to predict the calories of recipes. The model we are using is a regression model.

The response variable is calories. We chose calories because we are curious if we are able to accurately predict each recipe's calories based on the information in the dataset.

The metrics we will be using to evaluate the model are R² and RMSE. We chose R² because this tells us how much of the variation in the response variable our model can explain. We chose RMSE because this tells us how far off the predictions are from the actual values, on average. We chose RMSE over MAE because RMSE penalizes large errors more heavily, which is important when large calorie mispredictions are particularly undesirable.

At the time of prediction, we would know features such as the number of ingredients, number of steps, and cooking time, since these are properties of the recipe itself before it is consumed. We would not know the calories, as that is exactly what we are trying to predict.

## Baseline Model

## Final Model

## Fairness Analysis
