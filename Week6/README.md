# Assignment 6: Model Evaluation, Explainability, and Fairness Reflection

## Project Description

This project uses a supervised machine learning classification model to predict employee attrition.

The goal is to evaluate whether a Decision Tree model can help an HR team identify employees who may be at risk of leaving the company. The notebook does not only report accuracy. It also checks prediction errors, overfitting, feature importance, SHAP, LIME, and fairness across different employee groups.

The project focuses on whether the model is accurate, explainable, and fair enough for business decision-making.

## Business Problem

A company may want to understand which employees are more likely to leave. If HR can identify at-risk employees earlier, the company may be able to provide support, improve work conditions, or plan retention actions.

This analysis can help support business decisions such as:

* Which employees may need retention support
* Which work-related factors are useful signals for attrition risk
* Whether the model makes more mistakes for certain employee groups
* Whether the model is reliable enough for HR decision-making
* Whether the model should be used only as a prototype or improved before real use

## Dataset

The dataset used in this project is:

`employee_attrition_dataset.csv`

The dataset contains 340 records and 19 columns. Each row represents one employee record.

The dataset includes employee information such as:

* Employee ID
* Age
* Age group
* Gender
* Department
* Job level
* Employment type
* Region
* Monthly salary
* Years at company
* Years in current role
* Overtime hours
* Training hours last year
* Performance rating
* Job satisfaction
* Work-life balance
* Promotion in the last 2 years
* Commute distance
* Attrition status

The dataset has no missing values and no duplicate records.

## Target Variable

The target variable is:

`attrition`

The target classes are:

| Class | Meaning | Number of Records |
|---:|---|---:|
| 0 | No attrition | 72 |
| 1 | Attrition | 268 |

The target variable is imbalanced because most records belong to class 1. This means accuracy alone is not enough to judge the model. Precision, recall, F1-score, and the confusion matrix are also important.

## Features Used for the Model

The model used work-related employee information as input features.

The input features included:

* Age
* Department
* Job level
* Employment type
* Monthly salary
* Years at company
* Years in current role
* Overtime hours
* Training hours last year
* Performance rating
* Job satisfaction
* Work-life balance
* Promotion in the last 2 years
* Commute distance

The column `employee_id` was removed because it is only an identifier.

The columns `gender`, `age_group`, and `region` were removed from the model input and kept only for fairness reflection. This helps check whether model performance differs across groups without directly using those group columns for prediction.

## Data Preparation

The notebook completed the following preparation steps:

1. Loaded the dataset
2. Checked dataset shape, column names, data types, missing values, and duplicate rows
3. Checked the target variable distribution
4. Defined the target variable and input features
5. Removed the identifier column from model input
6. Kept group-related columns only for fairness reflection
7. Filled numerical missing values using the median
8. Filled categorical missing values using the most frequent value
9. Converted categorical columns into numerical columns using `pd.get_dummies()`
10. Split the data into training and testing sets using stratified splitting

Preprocessing was necessary because machine learning models need clean numerical input. Text or category labels such as department and job level must be converted into numerical columns before model training.

## Train and Test Split

The dataset was split into training and testing data.

| Dataset Part | Number of Records |
|---|---:|
| Training set | 272 |
| Testing set | 68 |

The training data was used to teach the model. The testing data was used to check how well the model performs on records it has not seen before.

Stratified splitting was used so the attrition and non-attrition distribution stayed similar in both sets.

## Classification Method

### Decision Tree Classifier

The notebook used a Decision Tree classification model:

```python
DecisionTreeClassifier(max_depth=4, random_state=42)
```

A Decision Tree was selected because it is simple and easier to explain than many complex models. The maximum depth was set to 4 to reduce overfitting and keep the model understandable.

## Main Evaluation Results

| Metric | Score |
|---|---:|
| Accuracy | 0.7794 |
| Precision | 0.8095 |
| Recall | 0.9444 |
| F1-score | 0.8718 |

The testing accuracy is about 0.78, which means the model correctly predicted about 78% of the test records.

Recall is the most important metric for this business problem because HR wants to identify most employees who may leave. A low recall would mean many at-risk employees are missed.

## Confusion Matrix Results

| Actual Class | Predicted No Attrition | Predicted Attrition |
|---|---:|---:|
| Actual No Attrition | 2 | 12 |
| Actual Attrition | 3 | 51 |

The confusion matrix values are:

| Error Type | Count | Meaning |
|---|---:|---|
| True Negative | 2 | The model predicted no attrition, and the employee did not leave |
| False Positive | 12 | The model predicted attrition, but the employee did not leave |
| False Negative | 3 | The model predicted no attrition, but the employee was an attrition case |
| True Positive | 51 | The model predicted attrition, and the employee was an attrition case |

## Error Analysis

The most common wrong prediction type is false positive.

A false positive means the model predicts that an employee may leave, but the employee actually stays. In business terms, this may cause unnecessary retention action, extra manager attention, or extra spending.

False negatives are less common in this result, but they are more serious. A false negative means the company may miss an employee who actually leaves. This could reduce the usefulness of the model for retention planning.

## Cross-Validation Results

The notebook used 5-fold cross-validation to test model stability.

| Fold | Accuracy |
|---:|---:|
| 1 | 0.8676 |
| 2 | 0.6765 |
| 3 | 0.8088 |
| 4 | 0.7647 |
| 5 | 0.8382 |

| Cross-Validation Measure | Value |
|---|---:|
| Mean accuracy | 0.7912 |
| Standard deviation | 0.0667 |

The model performance is fairly stable, but there is still some variation across folds. This may be related to the small dataset size.

## Overfitting and Underfitting Analysis

The selected model has higher training accuracy than testing accuracy.

| Measure | Score |
|---|---:|
| Training accuracy | 0.8824 |
| Testing accuracy | 0.7794 |

This shows a moderate overfitting pattern. The model performs better on the training data than on new test data.

The depth comparison also showed that deeper trees can reach very high training accuracy without improving testing accuracy. For example, a tree depth of 10 reached 1.0000 training accuracy but only 0.7353 testing accuracy.

This means deeper trees may memorize the training data instead of generalizing well to new employees.

## Feature Importance Results

The most important features in the Decision Tree model were:

| Feature | Importance |
|---|---:|
| job_satisfaction | 0.3396 |
| age | 0.2262 |
| overtime_hours | 0.2186 |
| work_life_balance | 0.1020 |
| monthly_salary | 0.0403 |
| commute_distance_km | 0.0401 |
| department_HR | 0.0333 |

From a business perspective, this suggests that employee experience, workload, and job conditions are useful signals for attrition prediction.

Feature importance does not prove cause and effect. For example, overtime hours may help the model make predictions, but this does not prove that overtime directly causes employees to leave.

## SHAP and LIME Explanation

The notebook used SHAP and LIME to explain the model.

SHAP was used to explain how each feature pushes predictions toward attrition or away from attrition. It provides both global explanation and individual prediction explanation.

LIME was used to explain one individual prediction by showing which feature conditions supported the predicted class and which feature conditions worked against it.

These methods help make the model more understandable for business users because they explain why the model made a prediction.

## Fairness and Bias Reflection

The fairness analysis compared model behavior across group-related columns:

* Gender
* Age group
* Region

For each group, the notebook reported:

* Number of records
* Actual positive rate
* Predicted positive rate
* Accuracy by group

### Fairness Summary by Gender

| Gender | Number of Records | Actual Positive Rate | Predicted Positive Rate | Accuracy by Group |
|---|---:|---:|---:|---:|
| Female | 31 | 0.8710 | 0.9677 | 0.8387 |
| Male | 37 | 0.7297 | 0.8919 | 0.7297 |

### Fairness Summary by Age Group

| Age Group | Number of Records | Actual Positive Rate | Predicted Positive Rate | Accuracy by Group |
|---|---:|---:|---:|---:|
| 18-25 | 4 | 1.0000 | 1.0000 | 1.0000 |
| 26-35 | 22 | 0.7727 | 0.9091 | 0.7727 |
| 36-50 | 23 | 0.6522 | 0.8696 | 0.6087 |
| 51+ | 19 | 0.9474 | 1.0000 | 0.9474 |

### Fairness Summary by Region

| Region | Number of Records | Actual Positive Rate | Predicted Positive Rate | Accuracy by Group |
|---|---:|---:|---:|---:|
| East | 23 | 0.9130 | 0.9565 | 0.9565 |
| North | 21 | 0.7143 | 0.9048 | 0.6190 |
| South | 13 | 0.7692 | 0.8462 | 0.7692 |
| West | 11 | 0.7273 | 1.0000 | 0.7273 |

The results show that the model does not perform exactly the same across all groups. Some groups have higher predicted attrition rates or different accuracy scores.

Even though `gender`, `age_group`, and `region` were removed from the model input, other features may still act as indirect proxy variables. Because this is an employee-related model, fairness should be reviewed carefully before real business use.

## Visualizations Created

The notebook creates the following visualizations:

* Target variable distribution bar chart
* Confusion matrix visualization
* Error type count visualization
* Cross-validation accuracy visualization
* Training and testing accuracy by tree depth
* Feature importance bar chart
* SHAP summary plot
* LIME explanation visualization or table
* Fairness comparison charts by gender, age group, and region

## Main Business Insights

The model can help HR identify employees who may be at risk of leaving.

The model has high recall, which means it catches most actual attrition cases. This is useful for retention planning because the company wants to miss as few at-risk employees as possible.

The main trade-off is that the model also creates false positives. This means HR may spend extra time or resources on employees who may not actually leave.

The most important features suggest that job satisfaction, age, overtime hours, work-life balance, salary, commute distance, and department may be useful signals for attrition risk.

The fairness analysis shows that the model should not be used automatically for employee decisions. Human review and stronger fairness testing are needed.

## Business Recommendation

This model should be treated as an early prototype.

It is useful for learning and initial HR analysis, but it is not ready for real business deployment. Before using this model in real employee decisions, the company should:

* Collect more employee data
* Test more classification models
* Compare results using recall, precision, F1-score, and confusion matrices
* Review false positives and false negatives with HR experts
* Check fairness across more employee groups
* Review possible proxy variables
* Use human judgment before making retention decisions

## Limitation and Responsible AI Reflection

One limitation is that the dataset is small and imbalanced. Most records belong to the attrition class. This can affect how the model learns and how reliable the results are.

Another limitation is that employee attrition is complex. Real attrition decisions may depend on factors not included in the dataset, such as manager relationships, personal situations, career goals, workplace culture, or external job opportunities.

Because the model is related to employee decisions, it should be used carefully. The model should support human decision-making, not replace HR judgment.

## How to Run

Open the notebook in Jupyter Notebook or Google Colab.

Install the required Python packages:

```bash
pip install pandas numpy scikit-learn matplotlib shap lime
```

Run the notebook cells from top to bottom.

Make sure the dataset file is in the same folder as the notebook. The dataset file should be named:

```text
employee_attrition_dataset.csv
```

If SHAP or LIME is missing in Jupyter, install the packages inside a notebook cell:

```python
import sys
!{sys.executable} -m pip install shap lime
```

Then restart the kernel and run all cells again.

## Files in This Project

```text
assignment6_submission/
│
├── Assignment6_Model_Evaluation_Explainability_Fairness.ipynb
├── employee_attrition_dataset.csv
├── README.md
└── requirements.txt
```

## Final Conclusion

This project completed a supervised classification workflow for employee attrition prediction.

The Decision Tree model achieved about 0.78 testing accuracy and 0.94 recall. This means the model is good at finding most attrition cases, which is useful for retention planning.

However, the model also shows moderate overfitting, false positive errors, and fairness differences across groups. Because of this, the model is only suitable as an early prototype.

Overall, the model can help demonstrate how classification, evaluation, explainability, and fairness reflection work together, but it needs more data, better validation, and HR expert review before real business use.
