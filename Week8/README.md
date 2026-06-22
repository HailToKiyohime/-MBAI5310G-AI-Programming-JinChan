# Assignment 8: NLP and Text Classification

## Project Description

This project uses Natural Language Processing to classify food delivery customer comments into feedback topics.

The goal is to build a simple text classification pipeline that can clean raw customer comments, convert the text into numerical features, train a machine learning model, and predict the correct feedback topic.

The project uses TF-IDF and Logistic Regression to help a food delivery business organize customer feedback more quickly.

## Business Problem

Food delivery companies receive many customer comments from app reviews, social media, surveys, and customer support channels.

Reading and sorting every comment by hand takes a lot of time. The main business problem is how to quickly understand what each customer comment is about.

This text classification model can help the company sort comments into topics such as:

* Delivery
* Pricing
* Packaging
* Food quality
* App experience
* Customer service

This is useful because the company can send the right comments to the right team faster. For example, delivery problems can go to the delivery operations team, while app problems can go to the app or technical support team.

## Dataset

The dataset used in this project is:

`food_delivery_feedback_topic_dataset.csv`

The original Excel dataset is also included:

`NLP_Dataset_3_Food_Delivery_Feedback_Topic.xlsx`

The dataset contains 120 rows and 9 columns. Each row represents one customer feedback comment about a food delivery service.

The dataset includes the following columns:

* CommentID
* CommentDate
* Platform
* City
* MealType
* CustomerSegment
* CustomerComment
* FeedbackTopic
* EngagementScore

## Important Columns

### CustomerComment

`CustomerComment` is the main text column. It contains the customer feedback text used as the model input.

### FeedbackTopic

`FeedbackTopic` is the target variable. It is the topic label that the model tries to predict.

The feedback topics are:

* App_Experience
* Customer_Service
* Delivery
* Food_Quality
* Packaging
* Pricing

### Business Context Columns

`Platform`, `City`, `MealType`, and `CustomerSegment` provide extra business context. These columns help explain where the comment came from and what type of customer or meal it relates to.

### EngagementScore

`EngagementScore` is a numeric business signal that shows how much attention or interaction the comment received.

## Target Variable Distribution

The target variable is balanced. Each feedback topic has 20 records.

| Feedback Topic | Number of Records |
|---|---:|
| App_Experience | 20 |
| Customer_Service | 20 |
| Delivery | 20 |
| Food_Quality | 20 |
| Packaging | 20 |
| Pricing | 20 |

This is helpful because the model gets an equal chance to learn each topic.

## Text Preprocessing

The notebook completed the following text preprocessing steps:

1. Converted text to lowercase
2. Removed punctuation
3. Tokenized the text into words
4. Removed stopwords
5. Applied stemming using PorterStemmer
6. Created a cleaned text column called `CleanedComment`

Preprocessing is important because raw customer comments can be messy. They may include capital letters, punctuation, common words, and different word forms.

Cleaning the text helps the model focus on useful topic-related words.

## Exploratory Text Analysis

The notebook analyzed word frequency in the cleaned customer comments.

The most common words included topic-related words such as:

* freshbit
* app
* price
* order
* fee
* delivery
* driver
* food
* support
* service

These frequent words show that customers are mainly talking about delivery speed, food quality, customer support, pricing, and app experience.

## POS Tagging and Named Entity Recognition

The notebook selected three example customer comments and applied:

* POS tagging
* Named Entity Recognition

POS tagging helps identify word roles such as nouns, verbs, and adjectives.

For example:

* Nouns can show key topics, such as delivery, price, app, support, food, or packaging
* Verbs can show actions, such as arrived, replied, refunded, or solved
* Adjectives can show opinions, such as fast, slow, cold, expensive, or clean

Named Entity Recognition helps detect names, locations, brands, dates, and other important details.

This can help a business understand what customers are discussing and which service areas need attention.

## Feature Extraction

The notebook used TF-IDF for feature extraction.

TF-IDF converts cleaned text into numerical features. Each feature represents a word, and each value shows how important that word is in a comment.

This step is necessary because machine learning models cannot directly understand raw text. The text must be converted into numbers before model training.

## Classification Method

### Logistic Regression

The notebook used Logistic Regression as the classification model.

The model was trained using TF-IDF features from the cleaned customer comments.

The notebook used an 80 percent training set and a 20 percent testing set:

| Dataset Split | Number of Records |
|---|---:|
| Training set | 96 |
| Testing set | 24 |

The training data teaches the model patterns between customer comments and feedback topics. The testing data checks whether the model can classify new comments that it has not seen before.

## Model Evaluation

The model was evaluated using:

* Accuracy
* Confusion matrix
* Classification report

## Main Evaluation Results

The model achieved an accuracy of 1.00 on the testing data.

This means the model classified all 24 test comments correctly in this assignment dataset.

| Metric | Result |
|---|---:|
| Accuracy | 1.00 |
| Test records | 24 |

The classification report also showed precision, recall, and F1-score of 1.00 for each feedback topic.

| Feedback Topic | Precision | Recall | F1-score | Support |
|---|---:|---:|---:|---:|
| App_Experience | 1.00 | 1.00 | 1.00 | 4 |
| Customer_Service | 1.00 | 1.00 | 1.00 | 4 |
| Delivery | 1.00 | 1.00 | 1.00 | 4 |
| Food_Quality | 1.00 | 1.00 | 1.00 | 4 |
| Packaging | 1.00 | 1.00 | 1.00 | 4 |
| Pricing | 1.00 | 1.00 | 1.00 | 4 |

## Confusion Matrix Interpretation

The confusion matrix showed that the model correctly classified the test comments into the right feedback topics.

In a business setting, a wrong prediction could send a customer comment to the wrong team. For example, a delivery issue could be incorrectly sent to the customer service team. This could slow down the response.

In this assignment result, the model did not make mistakes on the testing set.

## Main Business Insights

The text analysis shows that common words are strongly connected to business issues.

For example:

* Pricing comments often include words such as price and fee
* App experience comments often include words such as app
* Customer service comments often include words such as support and service
* Delivery comments often include words such as delivery, order, and driver
* Food quality comments often include words related to meal condition
* Packaging comments often include words related to spills, containers, or damaged packaging

This means customer comments can provide useful signals about which part of the business needs attention.

## Visualizations Created

The notebook creates the following visualizations:

* Target variable distribution bar chart
* Most common words bar chart
* Confusion matrix visualization

## Visualization Interpretation

The target distribution chart shows that each feedback topic has the same number of records. This means the dataset is balanced.

The most common words chart shows the main themes in the customer comments. Words related to delivery, app experience, pricing, customer service, food quality, and packaging appear frequently.

The confusion matrix visualization shows how well the model classified each feedback topic in the testing set.

## Business Interpretation

This model predicts the feedback topic of food delivery customer comments.

The model uses the `CustomerComment` column as the input text and predicts the `FeedbackTopic` column.

The model can help a food delivery company organize customer feedback faster. It can also help send comments to the correct business team.

This can reduce manual review time and help the company respond to customer issues more quickly.

## Limitation

One limitation is that the dataset is small. It only has 120 records.

Another limitation is that some comments have repeated sentence patterns. Because of this, the model may perform very well on this assignment dataset, but it may not perform as well on real customer comments.

Real customer comments may be longer, messier, more emotional, or harder to classify.

Before using this model in a real company, the business should test it on more real-world customer feedback and review wrong predictions carefully.

## How to Run

Open the notebook in Jupyter Notebook or Google Colab.

Install the required Python packages:

```bash
pip install pandas numpy scikit-learn matplotlib nltk spacy openpyxl
```

If spaCy is used for Named Entity Recognition, install the English model:

```bash
python -m spacy download en_core_web_sm
```

Run the notebook cells from top to bottom.

Make sure the dataset file is in the same folder as the notebook. The dataset file should be named:

```text
food_delivery_feedback_topic_dataset.csv
```

## Files in This Project

```text
assignment8_food_delivery_nlp/
│
├── Assignment8_NLP_Text_Classification.ipynb
├── food_delivery_feedback_topic_dataset.csv
├── README.md
└── requirements.txt
```

## Final Conclusion

This project completed a basic Natural Language Processing and text classification workflow.

The notebook loaded a food delivery feedback dataset, cleaned the customer comments, analyzed frequent words, applied POS tagging and Named Entity Recognition, converted text into TF-IDF features, trained a Logistic Regression model, and evaluated the model using accuracy, confusion matrix, and classification report.

The model performed strongly on the testing data and correctly classified the test comments in this assignment dataset.

Overall, this analysis shows that NLP can help a food delivery company organize customer feedback by topic and route comments to the correct team faster. However, the model should be tested with more real customer comments before being used in a real business setting.
