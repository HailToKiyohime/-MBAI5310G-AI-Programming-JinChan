# Assignment 5: Clustering and Customer Segmentation

## Project Description

This project uses unsupervised learning to discover customer patterns in a SaaS free trial dataset for CloudDesk.

The goal is to group trial accounts into meaningful customer segments based on product usage, engagement, pricing interest, support activity, trial completion, product fit, and estimated annual value.

The project uses K-means clustering to help the business understand which trial accounts may deserve more sales attention, onboarding support, or lower-touch marketing campaigns.

## Business Problem

CloudDesk is a SaaS business that receives many free trial sign-ups. The sales and customer success teams cannot give every trial account the same level of attention.

The main business problem is deciding how to prioritize trial accounts before they convert to paid customers. Customer segmentation is useful because it helps CloudDesk group similar trial users and choose better marketing or sales actions for each group.

This analysis can help improve decisions such as:

* Which trial accounts should receive direct sales outreach
* Which accounts may need onboarding support
* Which accounts should receive product education or webinar invitations
* Which accounts may be best handled through lower-cost email nurturing
* Which accounts have the strongest potential value for the business

## Dataset

The dataset used in this project is:

`clouddesk_saas_trial_conversion_dataset.csv`

The original dataset contains 262 rows and 21 columns. After removing duplicate rows, the cleaned dataset contains 260 rows.

The dataset includes SaaS trial account information such as:

* Trial ID
* Trial start date
* Industry
* Region
* Lead source
* Plan type
* Company size
* Trial length
* Login count during the first 14 days
* Number of features used
* Team invites
* Pricing pages viewed
* Email clicks
* Webinar attendance
* Support tickets
* Discount offered percent
* Competitor mention status
* Trial completion percent
* Product fit score
* Estimated annual value
* Converted to paid status

The column `Converted_To_Paid` was kept only as a reference for business interpretation. It was excluded from the K-means training features because this assignment uses unsupervised learning.

## Features Used for Clustering

The K-means model used the following numerical features:

* Trial_Length_Days
* Login_Count_14_Days
* Features_Used
* Team_Invites
* Pricing_Pages_Viewed
* Email_Clicks
* Webinar_Attended
* Support_Tickets
* Discount_Offered_Percent
* Competitor_Mentioned
* Trial_Completion_Percent
* Product_Fit_Score
* Estimated_Annual_Value

Categorical columns such as `Industry`, `Region`, `Lead_Source`, `Plan_Type`, and `Company_Size` were inspected, then excluded from the final K-means model because the notebook selected numerical features for clustering.

## Data Preparation

The notebook completed the following preparation steps:

1. Loaded the dataset
2. Checked dataset shape, column names, data types, missing values, and duplicate rows
3. Removed duplicate rows
4. Selected useful numerical features for clustering
5. Converted `Estimated_Annual_Value` from currency text into a numeric value
6. Converted selected numerical columns into numeric format
7. Filled missing numerical values using the median
8. Scaled the selected features using `StandardScaler`
9. Confirmed that the scaled features were ready for K-means clustering

Scaling was important because K-means clustering is distance-based. Without scaling, larger-value columns such as `Estimated_Annual_Value` could dominate the clustering result.

## Clustering Method

### K-means Clustering

K-means clustering was used to group SaaS trial accounts into customer segments.

The notebook used the Elbow Method to compare different values of K from 1 to 10. The final model used:

```python
KMeans(n_clusters=3, random_state=42, n_init=10)
```

K = 3 was selected because the inertia decreased strongly for the first few cluster values and became more gradual after about 3 clusters. This made 3 clusters a practical choice for business interpretation.

## Elbow Method Results

| Number of Clusters | Inertia |
|---:|---:|
| 1 | 3380.00 |
| 2 | 2864.49 |
| 3 | 2677.33 |
| 4 | 2525.82 |
| 5 | 2403.45 |
| 6 | 2290.69 |
| 7 | 2219.54 |
| 8 | 2138.75 |
| 9 | 2058.24 |
| 10 | 2016.03 |

## Cluster Results

The final K-means model created 3 customer segments.

| Segment Name | Cluster | Number of Trial Accounts | Conversion Rate for Reference | Avg. Login Count | Avg. Features Used | Avg. Pricing Pages Viewed | Avg. Trial Completion | Avg. Product Fit Score | Avg. Estimated Annual Value |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| High-Value Engaged Trial Accounts | 0 | 96 | 0.62 | 14.47 | 6.34 | 36.08 | 86.94 | 6.07 | $7,366.58 |
| Low-Engagement Trial Accounts | 1 | 101 | 0.10 | 6.02 | 3.04 | 18.82 | 55.07 | 5.52 | $2,997.35 |
| Medium-Engagement Trial Accounts | 2 | 63 | 0.60 | 11.54 | 4.87 | 29.49 | 77.78 | 6.74 | $4,872.43 |

## Segment Interpretation

### High-Value Engaged Trial Accounts

This segment has the highest login activity, the most features used, the most pricing page views, strong trial completion, and the highest estimated annual value.

This is likely the most valuable segment for CloudDesk because these accounts show strong product engagement and high revenue potential. These users should receive direct sales outreach, personalized demos, and fast customer success follow-up.

### Medium-Engagement Trial Accounts

This segment has medium engagement, strong trial completion, and the highest average product fit score. Its estimated annual value is lower than the high-value segment, while its reference conversion rate is still strong.

This segment may respond well to onboarding support, product education, webinars, case studies, and targeted follow-up messages.

### Low-Engagement Trial Accounts

This segment has the lowest login activity, fewer features used, fewer pricing page views, lower trial completion, the lowest product fit score, and the lowest reference conversion rate.

This group may need lower-cost marketing attention such as automated email nurturing, tutorial content, product reminders, and simple onboarding messages. The business should avoid spending too many high-cost sales resources on this segment unless there is additional context showing strong opportunity.

## Main Business Insights

The clustering analysis found clear differences in SaaS trial behavior.

High engagement, more feature usage, more pricing page views, and higher trial completion are connected with stronger business value. The High-Value Engaged Trial Accounts segment is the strongest opportunity because it combines active usage with the highest estimated annual value.

The Medium-Engagement segment is also important because it has the highest average product fit score and a strong reference conversion rate. These customers may need the right education or onboarding support to move closer to paid conversion.

The Low-Engagement segment is the least ready for direct sales attention. These accounts may still be useful for long-term nurturing, but they should receive lower-cost campaigns unless other business signals suggest higher potential.

## Visualizations Created

The notebook creates the following visualizations:

* Elbow Method plot for choosing the number of clusters
* Scatter plot comparing login count and trial completion percent
* Bar chart comparing average engagement metrics by segment
* Box plot comparing estimated annual value by segment
* PCA scatter plot showing clusters in two dimensions

## Visualization Interpretation

The Elbow Method plot shows that inertia decreases as the number of clusters increases. The decrease becomes more gradual around K = 3, which supports the choice of 3 customer segments.

The scatter plot using login count and trial completion percent shows that more active trial accounts tend to have higher completion levels. This supports the idea that product engagement is a useful signal for segmentation.

The bar chart comparing segment averages shows that the High-Value Engaged segment has stronger engagement across important usage metrics. This helps explain why the segment should receive priority sales and customer success attention.

The box plot of estimated annual value shows that the High-Value Engaged segment has the strongest revenue potential. This supports using estimated value as part of account prioritization.

The PCA visualization gives a simplified two-dimensional view of the clusters. It helps show how the K-means model separated customers based on the combined scaled features.

## Business Recommendation

CloudDesk should use the three customer segments to guide sales and marketing decisions.

For High-Value Engaged Trial Accounts, CloudDesk should prioritize direct sales outreach, personalized demos, onboarding support, and fast follow-up because this segment has the highest engagement and revenue potential.

For Medium-Engagement Trial Accounts, CloudDesk should focus on product education, webinars, onboarding reminders, case studies, and targeted emails because this group shows good product fit and may convert with stronger support.

For Low-Engagement Trial Accounts, CloudDesk should use lower-cost marketing campaigns such as automated email reminders, beginner tutorials, self-service onboarding, and product value messages. Human review should still be used before reducing attention to any specific account.

This segmentation can help the business allocate time, sales resources, and customer success support more efficiently.

## Limitation and Responsible AI Reflection

One limitation is that the dataset may not include all real sales factors. For example, it may miss budget timing, decision-maker involvement, company urgency, buying committee size, competitor contracts, or relationship quality.

K-means does not always create perfect customer segments because real customers can overlap across groups. K-means also depends on the selected features, scaling method, and chosen number of clusters.

One possible unfair decision is that low-engagement accounts could receive less support even when they have a valid reason for low activity. Some customers may need more training, have internal delays, or still represent a good future opportunity.

Human judgment should still be used because business teams can consider customer context, account history, fairness, campaign cost, and relationship quality before making final decisions based on clustering results.

## How to Run

Open the notebook in Jupyter Notebook or Google Colab.

Install the required Python packages:

```bash
pip install pandas scikit-learn matplotlib
```

Run the notebook cells from top to bottom.

Make sure the dataset file is in the same folder as the notebook. The dataset file should be named:

```text
clouddesk_saas_trial_conversion_dataset.csv
```

## Files in This Project

```text
assignment-5-clustering-customer-segmentation/
│
├── Assigment 5_ Clustering and_Customer_Segmentation.ipynb
├── clouddesk_saas_trial_conversion_dataset.csv
├── README.md
└── requirements.txt
```

## Final Conclusion

This project completed an unsupervised learning workflow using K-means clustering for CloudDesk SaaS trial customer segmentation.

The final model created 3 customer segments: High-Value Engaged Trial Accounts, Medium-Engagement Trial Accounts, and Low-Engagement Trial Accounts.

The High-Value Engaged segment is the most valuable because it has the highest usage activity and highest estimated annual value. The Medium-Engagement segment also shows good business potential because it has the strongest product fit score and a high reference conversion rate. The Low-Engagement segment may benefit from lower-cost nurturing and onboarding content.

Overall, this analysis helps CloudDesk make better marketing, sales, and customer success decisions by matching each trial account segment with a more appropriate business strategy.
