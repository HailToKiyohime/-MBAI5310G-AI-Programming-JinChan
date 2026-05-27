Machine Learning Pipeline Assignment
Project Description
This project builds a basic machine learning pipeline for a marketing campaign response prediction task. The goal is to use customer and campaign related information to predict whether a customer responded to a marketing campaign.
Dataset
The dataset used in this project is `marketing_campaign_response_dataset.csv`.
The dataset contains customer information and marketing campaign activity, including demographics, customer segment, website visits, email activity, ad clicks, previous purchases, discount offer status, campaign channel, customer satisfaction, last month spending, and campaign response.
After duplicate rows were removed, the cleaned dataset contained 300 records.
Business Problem
Marketing teams need to understand which customers are more likely to respond to a campaign. A prediction model can help support campaign planning by identifying customers with a higher chance of responding.
Target Variable
The target variable is `Responded`.
This variable shows whether a customer responded to the marketing campaign. The values were converted into numeric labels for model training:
`Yes = 1`
`No = 0`
Features Used
The model used the following features as input variables:
`Age`, `Gender`, `City`, `Income`, `Customer_Segment`, `Website_Visits`, `Email_Opened`, `Ad_Clicks`, `Previous_Purchases`, `Discount_Offered`, `Campaign_Channel`, `Customer_Satisfaction`, and `Last_Month_Spending`.
The `Customer_ID` column was excluded because it is only an identifier and does not provide useful predictive information.
Machine Learning Workflow
The notebook completed the main steps of a basic machine learning pipeline. The dataset was loaded and inspected, duplicate rows were removed, missing values were handled, features and target variable were defined, and the data was split into training and testing sets.
Numerical features were processed with median imputation and standard scaling. Categorical features were processed with most frequent value imputation and one hot encoding. A Logistic Regression model was then trained as the baseline classification model.
Model Used
Logistic Regression was used as the baseline model.
This model was selected because it is simple, interpretable, and suitable for a binary classification problem such as predicting whether a customer responded to a campaign.
Main Result
The model achieved an accuracy of approximately `78.33%` on the test set.
The confusion matrix was:
```text
[[22  8]
 [ 5 25]]
```
This means the model correctly predicted 22 customers who did not respond and 25 customers who responded. It also made 13 incorrect predictions on the test set.
Limitation
One limitation is that this is only a simple baseline model. The result could be improved by testing additional models, tuning model parameters, or adding more useful customer behavior data.
How to Run
Open the notebook in Jupyter Notebook or Google Colab.
Install the required packages:
```bash
pip install pandas scikit-learn notebook
```
Run the notebook cells from top to bottom.
Make sure the dataset file path points to:
```text
../data/marketing_campaign_response_dataset.csv
```
Files
`assignment2_ml_pipeline_campaign_response.ipynb` contains the full machine learning pipeline.
`marketing_campaign_response_dataset.csv` contains the dataset used for the project.