# Assignment 4: Decision Tree Model and Business Interpretation

## Project Description

This project builds a Decision Tree classification model to predict whether a customer will convert after a marketing campaign.

The assignment focuses on both machine learning performance and business interpretation. The model is trained on customer, campaign, engagement, and purchase information. The goal is to help the business understand which customers are more likely to convert and how marketing decisions can be improved using data.

## Business Problem

The business is running marketing campaigns across different channels such as email, social media, SMS, search ads, and display ads. The business wants to improve campaign performance by identifying customers who are more likely to convert.

The main problem is deciding which customers should receive more marketing attention, promotions, or follow-up actions. Machine learning can support this decision by predicting whether a customer is likely to convert based on customer profile, campaign behavior, purchase history, and engagement data.

This prediction is useful because it can help the business:

* Focus marketing resources on customers with higher conversion potential
* Reduce wasted campaign spending
* Improve customer targeting
* Understand which customer behaviors are most related to conversion
* Make more data-driven campaign decisions

## Dataset

The dataset used in this project is:

`marketing_campaign_decision_tree_dataset.csv`

The original dataset contains 605 rows and 21 columns. After removing duplicate rows, the cleaned dataset contains 600 rows.

The dataset includes customer and marketing campaign information such as:

* Age
* Annual income
* Customer segment
* Region
* Campaign channel
* Campaign type
* Ad exposure count
* Email opened status
* Ad clicked status
* Website visits in the last 30 days
* Previous purchases
* Average order value
* Discount offered percentage
* Days since last purchase
* Loyalty score
* Customer satisfaction
* Social media engagement score
* Prior campaign response
* Conversion status

## Target Variable

The target variable is:

`Converted`

The model predicts whether a customer converted after the marketing campaign.

The target values are:

* `No`
* `Yes`

## Input Features

The input features used in the model are:

* Age
* Annual_Income
* Customer_Segment
* Region
* Campaign_Channel
* Campaign_Type
* Ad_Exposure_Count
* Email_Opened
* Ad_Clicked
* Website_Visits_Last_30_Days
* Previous_Purchases
* Average_Order_Value
* Discount_Offered_Percent
* Days_Since_Last_Purchase
* Loyalty_Score
* Customer_Satisfaction
* Social_Media_Engagement_Score
* Prior_Campaign_Response

The columns `Customer_ID`, `Campaign_Date`, and `Converted` were not used as input features. `Converted` was used as the target variable.

## Machine Learning Steps Completed

1. Loaded and inspected the dataset
2. Checked dataset shape, column names, data types, missing values, and duplicate rows
3. Removed duplicate rows
4. Converted currency columns from text format into numeric format
5. Defined the target variable as `Converted`
6. Separated input features and target variable
7. Dropped non-predictive identifier and date columns
8. Identified numerical and categorical features
9. Split the data into training and testing sets
10. Built preprocessing pipelines for numerical and categorical variables
11. Handled missing values using median imputation for numerical columns
12. Handled missing values using most frequent value imputation for categorical columns
13. Applied one-hot encoding to categorical variables
14. Trained a Decision Tree classification model
15. Calculated training accuracy and testing accuracy
16. Evaluated the model using confusion matrix, accuracy, precision, recall, and F1-score
17. Checked whether the model showed signs of overfitting
18. Calculated and visualized feature importance values
19. Interpreted the model results from a business perspective

## Model Used

### Decision Tree Classifier

A Decision Tree Classifier was used for this project. Decision Trees are useful for business interpretation because they create rule-based splits that can help explain which features are important in prediction.

The model was trained using a pipeline that included preprocessing and the Decision Tree model.

Main model settings:

```python
DecisionTreeClassifier(
    random_state=42,
    max_depth=3,
    min_samples_leaf=5
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

Precision measures how many customers predicted as converted actually converted.

Recall measures how many actual converted customers the model successfully identified.

F1-score balances precision and recall into one score.

## Model Results

| Metric | Score |
|---|---:|
| Training Accuracy | 0.6917 |
| Testing Accuracy | 0.6167 |
| Accuracy | 0.6167 |
| Precision | 0.6111 |
| Recall | 0.5690 |
| F1-score | 0.5893 |

## Confusion Matrix

| Actual / Predicted | Predicted No | Predicted Yes |
|---|---:|---:|
| Actual No | 41 | 21 |
| Actual Yes | 25 | 33 |

## Overfitting Interpretation

The training accuracy was 0.6917 and the testing accuracy was 0.6167. The difference between them was 0.0750.

This difference is not very large, so the model does not show strong signs of overfitting. The model performs better on the training data than the testing data, which is expected, but the gap is still reasonable.

## Business Interpretation

The Decision Tree model had moderate predictive performance. The testing accuracy was 0.6167, meaning the model correctly predicted about 61.67% of the test cases.

The F1-score was selected as the most important metric for this business problem because both types of prediction errors matter. The business wants to identify customers who are likely to convert, while also avoiding too many incorrect positive predictions.

In this business context:

* A false positive means the model predicted that a customer would convert, but the customer did not convert. This could lead to wasted marketing budget or unnecessary follow-up.
* A false negative means the model predicted that a customer would not convert, but the customer actually converted. This could cause the business to miss a valuable customer opportunity.

## Most Important Features

The most important features in the Decision Tree model were:

| Feature | Importance |
|---|---:|
| Loyalty_Score | 0.4931 |
| Social_Media_Engagement_Score | 0.1486 |
| Ad_Clicked_No | 0.1228 |
| Days_Since_Last_Purchase | 0.0880 |
| Annual_Income | 0.0803 |
| Customer_Satisfaction | 0.0671 |

The most important feature was `Loyalty_Score`, which means customer loyalty had the strongest influence on the model's conversion predictions.

These features can help the business make better decisions by showing which customer behaviors and characteristics are most related to conversion. For example, customers with stronger loyalty scores or higher engagement may be better targets for campaign follow-up, personalized offers, or retention-focused marketing.

## Key Business Insights

The main business insight is that customer loyalty and engagement are important signals for predicting campaign conversion. The business can use these signals to improve targeting and prioritize customers who are more likely to respond positively.

The model also shows that recent purchase behavior, income, and customer satisfaction may support campaign decision-making. These features can help the business design better customer segments and more relevant marketing strategies.

## Limitation

One limitation of this model is that it was trained on a small dataset of 600 cleaned rows. Because of this, the model may not fully capture all customer behavior patterns. The dataset may also contain bias if it does not represent the full customer population.

Human judgment should still be used when making business decisions. The model can support decision-making, but business teams should also consider campaign goals, customer relationships, market conditions, and ethical use of customer data.

## Charts and Outputs

The notebook generates the following outputs:

* Confusion matrix table
* Confusion matrix chart saved as `confusion_matrix.png`
* Feature importance table
* Feature importance chart saved as `feature_importance.png`
* Decision tree visualization saved as `decision_tree_visualization.png`
* Final model summary table

## How to Run

Open the notebook in Jupyter Notebook or Google Colab.

Install the required Python packages:

```bash
pip install pandas scikit-learn matplotlib
```

Run the notebook cells from top to bottom.

Make sure the dataset file is in the same folder as the notebook. If the uploaded file has a suffix such as `(3)`, rename it to:

```text
marketing_campaign_decision_tree_dataset.csv
```

## Files in This Project

```text
assignment-4-decision-tree-business-interpretation/
│
├── Assignment 4_Decision_Trees_P1.ipynb
├── marketing_campaign_decision_tree_dataset.csv
├── README.md
├── confusion_matrix.png
├── feature_importance.png
└── decision_tree_visualization.png
```

## Final Conclusion

This project completed a Decision Tree classification workflow for predicting customer conversion after a marketing campaign. The model achieved a testing accuracy of 0.6167 and an F1-score of 0.5893.

The model does not show strong signs of overfitting because the difference between training accuracy and testing accuracy is 0.0750. The most important feature was `Loyalty_Score`, followed by `Social_Media_Engagement_Score`, `Ad_Clicked_No`, `Days_Since_Last_Purchase`, `Annual_Income`, and `Customer_Satisfaction`.

From a business perspective, the model can help the company identify customers who may be more likely to convert and support better marketing targeting decisions.
