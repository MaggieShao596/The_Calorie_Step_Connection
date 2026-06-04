## The Calorie-Step Connection: Can We Predict Recipe Calories?

**By Jacey Chow, Maggie Shao**

## Introduction

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
