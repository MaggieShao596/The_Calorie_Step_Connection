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

## Datasets Discription
This project uses two datasets from [Food.com](https://www.food.com/):
- `RAW_recipes`: contains recipe-level information 
- `interactions`: contains user ratings and reviews 

These datasets were originally collected for recommender system research in the paper Generating Personalized Recipes from Historical User Preferences by Majumder et al

### 📘 RAW_recipes

This dataset contains **83,782 rows**, where each row corresponds to a unique recipe.

| Column | Description |
|--------|-------------|
| `name` | Recipe name |
| `id` | Recipe ID |
| `minutes` | Minutes required to prepare the recipe |
| `contributor_id` | User ID of the recipe contributor |
| `submitted` | Date the recipe was submitted |
| `tags` | Food.com tags describing the recipe |
| `nutrition` | Nutrition info: [calories, fat, sugar, sodium, protein, saturated fat, carbohydrates] |
| `n_steps` | Number of preparation steps |
| `steps` | Recipe instructions |
| `description` | Recipe description |
| `ingredients` | List of ingredients |
| `n_ingredients` | Number of ingredients |

### 📗 interactions

This dataset contains **731,927 rows**, where each row represents a user interaction with a recipe.

| Column | Description |
|--------|-------------|
| `user_id` | User ID |
| `recipe_id` | Recipe ID |
| `date` | Date of interaction |
| `rating` | User rating |
| `review` | User review text |

### missing values
| Column | Missing Count |
|--------|--------------|
| `name` | 1 |
| `id` | 0 |
| `minutes` | 0 |
| `contributor_id` | 0 |
| `submitted` | 0 |
| `tags` | 0 |
| `nutrition` | 0 |
| `n_steps` | 0 |
| `steps` | 0 |
| `description` | 70 |
| `ingredients` | 0 |
| `n_ingredients` | 0 |
| `avg_rating` | 2609 |

### Cleaned Dataset Preview

| name | minutes | n_steps | n_ingredients | calories | total fat(PDV) | sugar(PDV) | sodium(PDV) | protein(PDV) | saturated fat(PDV) | carbohydrates(PDV) | avg_rating |
|------|---------|---------|---------------|----------|----------------|------------|-------------|--------------|-------------------|-------------------|------------|
| 1 brownies in the world best ever | 40 | 10 | 9 | 138.4 | 10.0 | 50.0 | 3.0 | 3.0 | 19.0 | 6.0 | 4.0 |
| 1 in canada chocolate chip cookies | 45 | 12 | 11 | 595.1 | 46.0 | 211.0 | 22.0 | 13.0 | 51.0 | 26.0 | 5.0 |
| 412 broccoli casserole | 40 | 6 | 9 | 194.8 | 20.0 | 6.0 | 32.0 | 22.0 | 36.0 | 3.0 | 5.0 |
| millionaire pound cake | 120 | 7 | 7 | 878.3 | 63.0 | 326.0 | 13.0 | 20.0 | 123.0 | 39.0 | 5.0 |
| 2000 meatloaf | 90 | 17 | 13 | 267.0 | 30.0 | 12.0 | 12.0 | 29.0 | 48.0 | 2.0 | 5.0 |

### Univariate Analysis

We first examined the distribution of calories across all recipes (after removing outliers above 4,000 calories).

<iframe
  src="assets/calories_hist.html"
  width="800"
  height="500"
  frameborder="0"
></iframe>

The distribution is right-skewed, with most recipes falling between 0 and 800 calories.

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
