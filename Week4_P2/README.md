# Assignment 4 Part 2: Decision Tree Model and Business Interpretation

## Project Description

This project builds a Decision Tree classification model to predict whether a FreshBasket customer is likely to churn.

The assignment focuses on both machine learning results and business interpretation. The model uses customer profile, subscription, ordering, delivery, service, discount, app engagement, and satisfaction information to help the business identify customers who may need retention support.

## Business Problem

FreshBasket is a grocery delivery or subscription-based food service business. The business wants to reduce customer churn by identifying customers who may stop using the service.

The main problem is deciding which customers should receive retention actions such as service follow-up, improved offers, loyalty support, or customer experience improvements.

Machine learning can help FreshBasket predict whether a customer is likely to churn based on past customer behavior and account information. This prediction is useful because it can help the business:

* Identify at-risk customers earlier
* Focus retention efforts on customers who need attention
* Reduce customer loss
* Improve customer satisfaction
* Make better decisions about discounts, service support, and customer engagement

## Dataset

The dataset used in this project is:

`freshbasket\_customer\_churn\_dataset.csv`

The original dataset contains 425 rows and 16 columns. After removing duplicate rows, the cleaned dataset contains 420 rows.

The dataset includes customer churn information such as:

* Customer age group
* Region
* Subscription type
* Payment method
* Delivery window
* Membership length
* Monthly spend
* Average order value
* Orders in the last 3 months
* Delivery issues in the last 3 months
* Customer service tickets
* Discount usage
* App engagement score
* Satisfaction score
* Churn status

The original dataset contained 5 duplicate rows. Missing values were handled inside the preprocessing pipeline.

## Target Variable

The target variable is:

`Churned`

The model predicts whether a customer churned.

The target values are:

* `No`
* `Yes`

In this business context, `Yes` means the customer churned.

## Input Features

The input features used in the model are:

* Age\_Group
* Region
* Subscription\_Type
* Payment\_Method
* Delivery\_Window
* Membership\_Length\_Months
* Monthly\_Spend
* Average\_Order\_Value
* Orders\_Last\_3\_Months
* Delivery\_Issues\_Last\_3\_Months
* Customer\_Service\_Tickets
* Discount\_Used
* App\_Engagement\_Score
* Satisfaction\_Score

The columns `Customer\_ID` and `Churned` were not used as input features. `Customer\_ID` was removed because it is an identifier, and `Churned` was used as the target variable.

## Machine Learning Steps Completed

The notebook completed the following workflow:

1. Loaded and inspected the dataset
2. Checked dataset shape, column names, data types, missing values, and duplicate rows
3. Removed duplicate rows
4. Defined the target variable as `Churned`
5. Separated input features and target variable
6. Removed the non-predictive `Customer\_ID` column
7. Identified numerical and categorical features
8. Split the dataset into training and testing sets
9. Built preprocessing pipelines for numerical and categorical variables
10. Handled missing values using median imputation for numerical columns
11. Handled missing values using most frequent value imputation for categorical columns
12. Applied one-hot encoding to categorical variables
13. Trained a Decision Tree classification model
14. Calculated training accuracy and testing accuracy
15. Evaluated the model using confusion matrix, accuracy, precision, recall, and F1-score
16. Checked whether the model showed signs of overfitting
17. Calculated and visualized feature importance values
18. Interpreted the model results from a business perspective

## Model Used

### Decision Tree Classifier

A Decision Tree Classifier was used for this project. Decision Trees are useful for business interpretation because they create rule-based splits that help explain which customer features are most related to churn.

The model was trained using a pipeline that included preprocessing and the Decision Tree model.

Main model settings:

```python
DecisionTreeClassifier(
    random\_state=42,
    max\_depth=4,
    min\_samples\_leaf=15,
    class\_weight="balanced"
)
```

## Evaluation Metrics

The model was evaluated using the following metrics:

* Confusion matrix
* Accuracy
* Precision
* Recall
* F1-score
* Training accuracy
* Testing accuracy

Accuracy measures the total percentage of correct predictions.

Precision measures how many customers predicted as churned actually churned.

Recall measures how many actual churned customers the model successfully identified.

F1-score balances precision and recall into one score.

For this business problem, recall and F1-score are especially important because the business wants to identify customers who may churn while still keeping the overall prediction quality balanced.

## Model Results

|Metric|Score|
|-|-:|
|Training Accuracy|0.6607|
|Testing Accuracy|0.7024|
|Accuracy|0.7024|
|Precision|0.4750|
|Recall|0.8261|
|F1-score|0.6032|

## Confusion Matrix

|Actual / Predicted|Predicted No|Predicted Yes|
|-|-:|-:|
|Actual No|40|21|
|Actual Yes|4|19|

## Overfitting Interpretation

The training accuracy was 0.6607 and the testing accuracy was 0.7024.

The testing accuracy was slightly higher than the training accuracy, so the model does not show strong signs of overfitting. Overfitting would usually be a concern when training accuracy is much higher than testing accuracy. In this project, the model appears to generalize reasonably well to the testing data.

## Business Interpretation

The Decision Tree model had moderate predictive performance. The testing accuracy was 0.7024, meaning the model correctly predicted about 70.24% of the test cases.

The recall score was 0.8261, which means the model successfully found most of the customers who actually churned. This is useful for FreshBasket because missing churned customers could lead to lost revenue and weaker customer retention.

The precision score was 0.4750, which means some customers predicted as churned did not actually churn. This suggests the model may produce extra retention alerts, but that may still be acceptable if the business values catching more at-risk customers.

In this business context:

* A false positive means the model predicted that a customer would churn, but the customer did not churn. This could lead to unnecessary retention offers, discounts, or follow-up messages.
* A false negative means the model predicted that a customer would not churn, but the customer actually churned. This could cause FreshBasket to miss a customer who needed retention support.

## Most Important Features

The most important features in the Decision Tree model were:

|Feature|Importance|
|-|-:|
|Satisfaction\_Score|0.4880|
|App\_Engagement\_Score|0.2634|
|Orders\_Last\_3\_Months|0.1846|
|Age\_Group\_35-44|0.0432|
|Discount\_Used\_No|0.0208|

The most important feature was `Satisfaction\_Score`, which means customer satisfaction had the strongest influence on the model's churn predictions.

The next most important features were `App\_Engagement\_Score` and `Orders\_Last\_3\_Months`. This suggests that customer satisfaction, app activity, and recent ordering behavior are important signals for predicting churn.

## Key Business Insights

The main business insight is that customer experience and engagement are strong signals for churn risk. Customers with lower satisfaction, weaker app engagement, or reduced ordering activity may need more attention from the business.

FreshBasket can use these insights to improve retention decisions. For example, the business could prioritize customers with low satisfaction scores for support follow-up, offer personalized retention incentives to customers with declining order activity, or improve app engagement for customers who are becoming less active.

## Limitation

One limitation of this model is that the dataset is relatively small, with 420 cleaned rows. A larger dataset could help the model learn more reliable churn patterns.

Another limitation is that `Monthly\_Spend` and `Average\_Order\_Value` are stored as currency text values in the dataset. In a future version, these columns could be converted into numeric values before modeling so the Decision Tree can interpret spending amounts more directly.

The model should support business decisions, but human judgment should still be used. Business teams should consider customer relationships, service issues, campaign costs, fairness, and customer experience before taking action based only on model predictions.

## Charts and Outputs

The notebook generates the following outputs:

* Confusion matrix table
* Confusion matrix chart saved as `confusion\_matrix.png`
* Feature importance table
* Feature importance chart saved as `feature\_importance.png`
* Decision tree visualization saved as `decision\_tree\_visualization.png`
* Final model summary table

## How to Run

Open the notebook in Jupyter Notebook or Google Colab.

Install the required Python packages:

```bash
pip install pandas scikit-learn matplotlib
```

Run the notebook cells from top to bottom.

Make sure the dataset file is in the same folder as the notebook. If the uploaded file has a suffix such as `(1)`, rename it to:

```text
freshbasket\_customer\_churn\_dataset.csv
```

## Files in This Project

```text
assignment-4-decision-tree-business-interpretation-p2/
│
├── Assignment 4\_Decision\_Trees\_P2.ipynb
├── freshbasket\_customer\_churn\_dataset.csv
└── README.md
```

## Final Conclusion

This project completed a Decision Tree classification workflow for predicting FreshBasket customer churn. The model achieved a testing accuracy of 0.7024 and an F1-score of 0.6032.

The model does not show strong signs of overfitting because the training accuracy was 0.6607 and the testing accuracy was 0.7024. The most important feature was `Satisfaction\_Score`, followed by `App\_Engagement\_Score`, `Orders\_Last\_3\_Months`, `Age\_Group\_35-44`, and `Discount\_Used\_No`.

From a business perspective, the model can help FreshBasket identify customers who may be at risk of churn and support better retention decisions. The model is most useful as a decision-support tool when combined with business judgment and customer service knowledge.

