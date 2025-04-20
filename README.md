# Customer Segmentation Optimization & Delivery Standerdization for Swire Coca-Cola
## Project Overview
Swire Coca-Cola’s distribution team found that an outdated 400-gallon/year rule for customer segmentation was leading to inefficiencies in its delivery model. Lower-volume customers were being serviced with costly in-house Red Truck deliveries instead of third-party White Truck service, causing significant waste. This static threshold failed to adapt to actual customer behavior, resulting in:
Missed revenue opportunities: An estimated $52–$74 million in annual revenue was being forfeited due to suboptimal customer classification​

Operational inefficiencies: Many low-volume customers remained in high-cost delivery groups (Red Trucks), inflating logistics costs​

Customer misclassification: The rigid rule overlooked some potentially high-volume customers who were not properly identified under the old system​
## Objectives
This project aimed to reassess and redefine the customer segmentation strategy using data-driven methods. Key objectives included:
Customer Re-Segmentation: Identify true high-potential customers that warrant costlier direct delivery, versus those suitable for outsourced delivery​

Threshold Optimization: Determine optimal annual volume cut-off thresholds (gallons or cases) to replace the static 400-gallon rule​.

Revenue Retention: Capture more revenue by correctly classifying and servicing high-potential customers (preventing churn or missed sales)​.

Cost Minimization: Reduce delivery and logistics costs by moving low-volume accounts to more cost-effective delivery methods​.
##  Business Problem
Swire Coca-Cola’s Western U.S. operations are experiencing elevated logistical costs stemming from the blanket assignment of in-house Red Truck delivery services to customers, regardless of their order volume or profitability. This one-size-fits-all approach fails to distinguish between low- and high-potential customers, leading to inefficient use of resources and unnecessary delivery expenses. The business challenge is to develop a predictive framework that accurately identifies which customers should be whitelisted for cost-effective White Truck (third-party) service, enabling the company to reduce logistics costs while preserving revenue from high-value accounts.
## Solution Summary
To address these goals, we developed a multi-faceted solution combining supervised machine learning and unsupervised clustering:
Machine Learning Models: Trained classification models (XGBoost, Logistic Regression, and Random Forest) to predict whether a customer’s volume would qualify for cost-effective delivery or require dedicated service​.

XGBoost proved most effective for the overall customer base, while Logistic Regression worked well for a specific subset of customers.
Optimal Volume Thresholds: The supervised models revealed better volume cut-offs. For the general customer population, an annual threshold of approximately 615 gallons (or equivalent cases) was identified as optimal. For the LMP fountain-only segment (customers exclusively buying fountain syrup), a lower threshold around 350 gallons/year was more appropriate.​

These thresholds significantly differ from the old 400-gallon rule, indicating a need for more nuanced segmentation.
Unsupervised Clustering: We performed customer segmentation using clustering techniques to group similar customers together. By analyzing patterns like monthly order trends (Average Growth Index) and product mix, we derived distinct customer profiles and uncovered behavioral segments​

This helped validate the new thresholds and provided deeper insight into customer behavior beyond a single volume metric.
Projected Financial Impact: Implementing the new segmentation scheme is expected to yield substantial benefits. We estimate around $7.6 million in annual cost savings by offloading unprofitable low-volume deliveries​

Additionally, by correctly retaining high-potential customers in the direct delivery program, the company can preserve roughly $170.6 million in revenue (at ~20% profit margin) that might otherwise be lost​
## Technical Approach
Data Wrangling: We collected two years of customer order data and performed extensive cleaning and feature engineering:
Treated and filled missing values to ensure complete data for all active customers​

Converted categorical fields (e.g. ORDER_TYPE, PRIMARY_GROUP_NUMBER) into a series of boolean flags for each category​, making the data more suitable for modeling.
Created aggregated features per customer, such as total gallons and cases ordered in Year 1 and Year 2, as well as calculated metrics like Average Growth Index (AGI) to quantify monthly growth/decline trends​

Labeled customers based on their service type (Red Truck vs. White Truck) and prior-year volume, to use as the target variable for supervised learning.
## Model Training & Evaluation: We applied multiple algorithms to classify customers into high-volume (retain on Red Truck) vs low-volume (move to White Truck) segments:
Trained an XGBoost classifier on the full customer dataset (combining gallons and cases) – this model had the best performance in identifying high-value customers​

It suggested ~615 gallons/year as the break-even threshold for cost-effective service.
Built a Logistic Regression model for the LMP fountain-only customer subset (who only purchase syrup in gallons) – this simpler model was more interpretable and indicated ~350 gallons/year as a suitable cutoff​

Evaluated models primarily by classification accuracy and business criteria. The XGBoost model achieved about 43% accuracy in classifying customers at the 615-gallon threshold, and the logistic model about 46% accuracy at the 350-gallon mark​
While accuracy was modest (due to imbalanced classes and a conservative threshold definition), these models were sufficient to guide a policy change.
Used a Random Forest model as a supplementary check to identify any misclassified cases and key feature indicators. This helped reveal that roughly 60% of non-LMP customers exhibit usage patterns similar to LMP customers​, suggesting many accounts could be treated as high-potential despite not being in the LMP program.
