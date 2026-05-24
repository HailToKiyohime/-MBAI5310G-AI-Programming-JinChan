# Machine Learning Pipeline Assignment

## Project Description

This project builds an end-to-end machine learning pipeline to predict whether a customer will purchase a product.

## Dataset

The dataset used in this project is `marketing_customer_purchase.csv`.

It contains customer information such as age, gender, city, income, website visits, time on site, previous purchases, membership level, email opened, discount used, social media clicks, cart abandoned status, and purchase status.

## Target Variable

The target variable is:

`Purchased`

The model predicts whether a customer purchased the product.

## Features Used

The features used include:

- Age
- Gender
- City
- Income
- Website_Visits
- Time_on_Site_Minutes
- Previous_Purchases
- Membership_Level
- Email_Opened
- Discount_Used
- Social_Media_Clicks
- Cart_Abandoned

## Steps Completed

1. Loaded and inspected the dataset
2. Checked missing values and duplicate rows
3. Cleaned the data
4. Defined features X and target y
5. Split the data into training and testing sets
6. Applied preprocessing using SimpleImputer, StandardScaler, and OneHotEncoder
7. Trained a Logistic Regression baseline model
8. Generated predictions
9. Evaluated the model result

## Model Used

Logistic Regression was used as the baseline classification model.

## Main Result

The baseline model completed the full machine learning workflow and generated predictions on the test data.

## How to Run

Open the notebook in Jupyter Notebook or Google Colab.

Install the required packages:

```bash
pip install -r requirements.txt