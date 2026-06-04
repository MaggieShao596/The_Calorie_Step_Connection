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

Given the datasets, our project investigates whether recipes with different calorie levels tend to have different levels of recipe complexity. More specifically, we focus on whether calorie groups are associated with differences in the average number of preparation steps. To support this analysis, we constructed a clean, recipe-level dataset by combining information from both the recipes and interactions datasets.

## Data Cleaning and Exploratory Data Analysis
First, we processed the interactions dataset to create a new variable called `avg_rating`, which represents the average user rating for each recipe. Ratings of 0 were treated as missing values because they do not represent valid user ratings. We then grouped the interactions data by `recipe_id`, calculated the mean rating using only non-missing ratings, and merged this recipe-level rating information into the recipes dataset using the recipe identifiers.

Next, we cleaned and engineered several features from the recipes dataset. The original `nutrition` column stored multiple nutrition values together as a list-like string, so we converted it into a usable list format and separated it into individual numeric columns. These columns include `calories`, `total fat(PDV)`, `sugar(PDV)`, `sodium(PDV)`, `protein(PDV)`, `saturated fat(PDV)`, and `carbohydrates(PDV)`. This step allowed us to analyze calories directly and compare recipes based on nutritional content.

We also used existing recipe characteristics such as `n_steps`, `n_ingredients`, and `minutes` to describe recipe complexity. The variable `n_steps` is especially important because our main research question asks whether recipes with different calorie levels require different numbers of preparation steps. In addition, we converted the `tags` column into a usable list format and created `n_tags`, which counts the number of tags associated with each recipe.

To make calorie comparisons clearer, we created a categorical variable called `calorie_group`. Recipes were divided into four groups based on calorie quartiles: `Low`, `Medium`, `High`, and `Very High`. This allowed us to compare average number of steps, average ratings, and other recipe features across different calorie levels.

### summary table of calorie groups

| calorie_group | count | mean_steps | median_steps | mean_calories |
|---------------|-------|------------|--------------|---------------|
| Low | 20946 | 8.17 | 7.0 | 101.14 |
| Medium | 20952 | 9.57 | 8.0 | 236.53 |
| High | 20940 | 10.62 | 9.0 | 392.56 |
| Very High | 20944 | 12.06 | 11.0 | 989.57 |

The most relevant variables for our analysis are `calories`, `calorie_group`, `n_steps`, `n_ingredients`, `minutes`, `avg_rating`, and the separated nutrition variables. These variables allow us to examine whether calorie level is connected to recipe complexity and whether higher-calorie recipes tend to involve more preparation steps.

### Cleaned Dataset Preview

| name | minutes | n_steps | n_ingredients | calories | total fat(PDV) | sugar(PDV) | sodium(PDV) | protein(PDV) | saturated fat(PDV) | carbohydrates(PDV) | avg_rating |
|------|---------|---------|---------------|----------|----------------|------------|-------------|--------------|-------------------|-------------------|------------|
| 1 brownies in the world best ever | 40 | 10 | 9 | 138.4 | 10.0 | 50.0 | 3.0 | 3.0 | 19.0 | 6.0 | 4.0 |
| 1 in canada chocolate chip cookies | 45 | 12 | 11 | 595.1 | 46.0 | 211.0 | 22.0 | 13.0 | 51.0 | 26.0 | 5.0 |
| 412 broccoli casserole | 40 | 6 | 9 | 194.8 | 20.0 | 6.0 | 32.0 | 22.0 | 36.0 | 3.0 | 5.0 |
| millionaire pound cake | 120 | 7 | 7 | 878.3 | 63.0 | 326.0 | 13.0 | 20.0 | 123.0 | 39.0 | 5.0 |
| 2000 meatloaf | 90 | 17 | 13 | 267.0 | 30.0 | 12.0 | 12.0 | 29.0 | 48.0 | 2.0 | 5.0 |


By structuring the data in this way, we created a clean recipe-level dataset that supports exploratory analysis, missingness assessment, and hypothesis testing. Our research question helps us understand how calorie content, preparation effort, and recipe characteristics are related. This can help users choose recipes more effectively, help recipe creators understand how nutritional content connects to preparation complexity, and provide insight into how food platforms may organize or recommend recipes.

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

We first examined the distribution of calories across all recipes.

<iframe
  src="assets/calories_hist_adjusted.html"
  width="800"
  height="500"
  frameborder="0"
></iframe>

Data is extremely right-skewed because there are some recipes with very large carlorie values aka outliers, such as 10,000 to 40,000 calories  

To fix this we remove unrealistic outliers that limited the calories from 0 to 4000.
<iframe
  src="assets/calories_hist.html"
  width="800"
  height="500"
  frameborder="0"
></iframe>

The distribution is right-skewed, with most recipes falling between 0 and 800 calories.

Also, We explored the relationship between calorie group and numbers of preperation steps.

<iframe
  src="assets/calorie_group_box.html"
  width="800"
  height="500"
  frameborder="0"
></iframe>

The box plot shows that recipes in the Very High calorie group tend to have more preparation steps compared to the Low calorie group. This suggests that higher-calorie recipes are generally more complex to prepare.

## Data Cleaning and Exploratory Data Analysis

## Assessment of Missingness

Looking at the cleaned dataset, there are three columns with missing values:

- `avg_rating`: 2,609 missing (~3.11%)
- `description`: 70 missing (~0.084%)
- `name`: 1 missing

We conducted a missingness assessment on two columns: `avg_rating` and `description`. 
We did not conduct a missingness assessment for `name` because only 1 value is missing out of 83,782 recipes, which represents less than 0.01% of the dataset. This single missing value has a negligible effect on our analysis and would not meaningfully impact any of our results or conclusions. 
For each column, we tested whether its missingness depends on other observed variables using permutation tests.

### NMAR Analysis

We believe `avg_rating` is likely **Not Missing at Random (NMAR)**. Whether a recipe has a rating may depend on the rating value itself, for example, users may be less likely to rate recipes they dislike, meaning the missingness is related to the unseen rating value itself. To determine whether this missingness could instead be MAR, we would need additional data such as the number of recipe views, whether users saved the recipe, or how long the recipe has been posted. If missing ratings are mainly explained by low interaction counts or newer recipes, then the missingness may depend on observed variables rather than the missing value itself.

A plausible NMAR column in this dataset is also `description`. Because `description` is written by the recipe contributor, whether it is missing may depend on unobserved factors such as how much effort the contributor wants to put into the recipe, how confident they feel about it, or whether they believe additional explanation is necessary. These factors are not fully captured in the dataset. Additional data that could help explain this missingness (and potentially make it MAR) would include contributor-level information such as experience level, engagement history, or whether Food.com prompted users to include a description during submission.

### Missingness Dependency Tests

#### `avg_rating` Missingness depends on `calorie_group`

- **Null Hypothesis:** The missingness of `avg_rating` is independent of `calorie_group`.
- **Alternative Hypothesis:** The missingness of `avg_rating` depends on `calorie_group`.
- **Test Statistic:** Variance of the mean missingness rate across the four calorie groups.
- **Result:** p-value < 0.05. We reject the null hypothesis.

The plot below shows the distribution of calorie groups when `avg_rating` is missing (True) versus not missing (False). The Very High calorie group has a noticeably higher proportion of missing ratings compared to other groups, suggesting that the missingness of `avg_rating` is related to calorie level.

<iframe
  src="assets/missingness_avg_rating_Calories.html"
  width="800"
  height="500"
  frameborder="0"
></iframe>

The plot below shows the empirical distribution of the test statistic under the null hypothesis from 1,000 permutations. The red line indicates the observed statistic, which falls far to the right of the null distribution. The p-value from our permutation test is **0.0**, confirming that the result is statistically significant.

<iframe
  src="assets/missingness_calorie_perm.html"
  width="800"
  height="500"
  frameborder="0"
></iframe>

#### `avg_rating` Missingness is independent of `sodium (PDV)`

- **Null Hypothesis:** The missingness of `avg_rating` is independent of `sodium (PDV)`.
- **Alternative Hypothesis:** The missingness of `avg_rating` depends on `sodium (PDV)`.
- **Test Statistic:** Absolute difference in mean sodium between missing and non-missing groups.
- **Result:** p-value > 0.05. We fail to reject the null hypothesis.

<iframe
  src="assets/missingness_sodium.html"
  width="800"
  height="500"
  frameborder="0"
></iframe

The plot below shows the empirical distribution of the test statistic under the null hypothesis. The red line indicates the observed statistic, which falls well within the null distribution. With a p-value of 0.892, there is no statistically significant relationship between sodium content and the missingness of `avg_rating`.

<iframe
  src="assets/missingness_sodium_perm.html"
  width="800"
  height="500"
  frameborder="0"
></iframe>

## Hypothesis Testing

## Framing a Prediction Problem

Our goal is to predict the calories of recipes. The model we are using is a regression model.

The response variable is calories. We chose calories because we are curious if we are able to accurately predict each recipe's calories based on the information in the dataset.

The metrics we will be using to evaluate the model are R² and RMSE. We chose R² because this tells us how much of the variation in the response variable our model can explain. We chose RMSE because this tells us how far off the predictions are from the actual values, on average. We chose RMSE over MAE because RMSE penalizes large errors more heavily, which is important when large calorie mispredictions are particularly undesirable.

At the time of prediction, we would know features such as the number of ingredients, number of steps, and cooking time, since these are properties of the recipe itself before it is consumed. We would not know the calories, as that is exactly what we are trying to predict.

## Baseline Model

## Final Model

## Fairness Analysis
