# Assignment 3: Classification Models and Evaluation Metrics

## Project Description

This project builds a machine learning classification pipeline to predict whether a customer will respond to a marketing campaign.

The project trains and compares two classification models:

* Logistic Regression
* Support Vector Machine (SVM)

The models are evaluated using confusion matrix, accuracy, precision, recall, and F1-score.

## Dataset

The dataset used in this project is `marketing\_campaign\_response\_dataset.csv`.

It contains customer and marketing campaign information, including age, income, website visits, ad clicks, previous purchases, customer satisfaction, last month spending, gender, city, customer segment, email opened, discount offered, campaign channel, and campaign response status.

The dataset originally contains 305 rows and 15 columns. After removing duplicate rows, the cleaned dataset contains 300 rows.

## Target Variable

The target variable is:

`Responded`

The model predicts whether a customer responded to the marketing campaign.

The target values are converted into numeric labels:

* `No` = 0
* `Yes` = 1

## Features Used

The features used in this project are:

* Age
* Income
* Website\_Visits
* Ad\_Clicks
* Previous\_Purchases
* Customer\_Satisfaction
* Last\_Month\_Spending
* Gender
* City
* Customer\_Segment
* Email\_Opened
* Discount\_Offered
* Campaign\_Channel

## Machine Learning Steps Completed

1. Loaded and inspected the dataset
2. Checked dataset shape, column names, data types, missing values, and duplicate rows
3. Removed duplicate rows
4. Handled missing values in numerical and categorical columns
5. Defined feature columns as `X`
6. Defined the target column as `y`
7. Converted the target variable from text labels into numeric labels
8. Split the dataset into training and testing sets
9. Applied preprocessing with `StandardScaler` and `OneHotEncoder`
10. Trained a Logistic Regression model
11. Trained an SVM model
12. Generated predictions for both models
13. Calculated confusion matrix, accuracy, precision, recall, and F1-score
14. Compared both models using a model comparison table and bar chart
15. Interpreted the final model results in a business context

## Models Used

### Logistic Regression

Logistic Regression was used as the first classification model. It is a simple and interpretable baseline model for binary classification problems.

### Support Vector Machine

Support Vector Machine was used as the second classification model. It was trained as a comparison model to evaluate whether it performed better than Logistic Regression.

## Evaluation Metrics

The models were evaluated using the following metrics:

* Confusion matrix
* Accuracy
* Precision
* Recall
* F1-score

Accuracy measures the total percentage of correct predictions.

Precision measures how many predicted responses were actually correct.

Recall measures how many actual response cases the model successfully found.

F1-score combines precision and recall into one balanced score.

## Model Results

|Model|Accuracy|Precision|Recall|F1-score|
|-|-:|-:|-:|-:|
|Logistic Regression|0.766667|0.750000|0.800000|0.774194|
|SVM|0.733333|0.769231|0.666667|0.714286|

## Confusion Matrices

### Logistic Regression

```text
\[\[22  8]
 \[ 6 24]]
```

### SVM

```text
\[\[24  6]
 \[10 20]]
```

## Main Result

Logistic Regression performed better overall because it had a higher accuracy, recall, and F1-score than SVM.

Although SVM had slightly higher precision, Logistic Regression had a better balance between precision and recall. Based on the F1-score, Logistic Regression was selected as the better model for this dataset.

## How to Run

Open the notebook in Jupyter Notebook or Google Colab.

Install the required Python packages:

```bash
pip install pandas scikit-learn matplotlib
```

Run the notebook cells from top to bottom.

Make sure the dataset file is in the same folder as the notebook, or update the dataset file path in the notebook.

## Files in This Project

```text
assignment-3-classification-models/
│
├── Assigment3\_ Classification Models and Evaluation Metrics.ipynb
├── marketing\_campaign\_response\_dataset.csv
└── README.md
```

## Final Conclusion

This project completed the required classification workflow for Assignment 3. Logistic Regression and SVM were trained, evaluated, and compared. Based on the F1-score, Logistic Regression was selected as the better model for predicting customer marketing campaign response.

