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

Evaluated models primarily by classification accuracy and business criteria. The XGBoost model achieved about 43% accuracy in classifying customers at the 615-gallon threshold, and the logistic model about 46% accuracy at the 350-gallon mark​.
While accuracy was modest (due to imbalanced classes and a conservative threshold definition), these models were sufficient to guide a policy change.
Used a Random Forest model as a supplementary check to identify any misclassified cases and key feature indicators. This helped reveal that roughly 60% of non-LMP customers exhibit usage patterns similar to LMP customers​, suggesting many accounts could be treated as high-potential despite not being in the LMP program.
Customer Clustering & Profiling: Beyond predictive modeling, we employed clustering to further analyze customer behaviors:
Performed monthly order clustering using features like monthly volume, growth rates (AGI), product mix, and delivery type. This unsupervised analysis grouped customers into profile clusters (e.g. steady growers, declining volume, seasonal buyers)​

Each cluster was profiled to understand common characteristics such as order frequency and package preferences, supporting more targeted strategies.
Conducted geographic analysis, creating state-level density maps to visualize where customer growth or decline was concentrated​.

This highlighted regional patterns – for example, certain states had higher concentrations of declining small accounts, indicating where a different service approach might be needed.
These profiles and cluster insights gave context to the ML model results, ensuring that our recommendations made sense for distinct groups of customers and were not solely driven by aggregate volume metrics.
## Key Insights
The analysis yielded several important insights about Swire’s customer base and delivery practices:
Medium-Volume Customer Patterns: A significant number of customers fall into a "medium" volume range of roughly 150–250 gallons per year, with a median around 201 gallons​

These accounts were historically treated as high-cost deliveries despite relatively low volumes, indicating a large opportunity to migrate them to a cheaper service without much revenue loss.
Declining Order Trends: There was a noticeable year-over-year drop in average order volume, especially within the first seven months of the second year​

This trend suggests that many customers reduced their purchase volume over time (possibly due to over-servicing or competition), underlining the need for proactive re-segmentation and engagement of at-risk accounts.
Hidden High-Potential Customers: Through model analysis, we discovered that many non-LMP customers share traits with LMP customers. In fact, roughly 60% of non-LMP accounts exhibit “LMP-like” purchasing behavior (e.g. high growth rates or consistent ordering patterns)​

These customers were not flagged under the old system but represent untapped potential — they could be groomed or upsold to become major accounts if given appropriate attention.
## Business Recommendations
Based on the findings, the project proposes several changes to Swire Coca-Cola’s delivery segmentation policy and customer management:
Dynamic Volume Thresholds: Replace the one-size-fits-all 400-gallon rule with a dynamic threshold model. Start by implementing the new cutoffs — ~615 gallons/year for most customers and 350 gallons/year for fountain-only customers — as criteria for Red Truck service​

These thresholds should be periodically re-evaluated and adjusted as customer behavior shifts, rather than kept static.
"Brown Truck" Program: Introduce a third-party delivery option (informally termed the Brown Truck Program) for low-volume customers who no longer qualify for Red Truck service​
Leveraging carriers like FedEx/UPS or postal services can service these accounts more cost-effectively. This offboarding strategy is expected to save on operating costs by avoiding the need for costly in-house deliveries to unprofitable routes​.

while still maintaining reasonable delivery times and customer service levels.
Automated Whitelist Management: Implement an automated whitelisting system that continuously monitors customer volumes and flags threshold crossings. Much like how e-commerce fulfillment programs (e.g., Amazon FBA/FBM or Walmart WFS) manage inventory and sellers, Swire can automatically onboard or offboard customers to the appropriate delivery program based on real-time data​
This ensures high-potential customers are quickly identified and retained on premium service, and low-volume customers are promptly moved to third-party delivery when their volumes drop.
## My Contribution
I played an equal and active role in this project alongside my team partner. I took the lead on exploratory data analysis (EDA), spending significant time analyzing the original dataset to uncover meaningful trends and guide our modeling approach. I built the initial versions of decision tree and regression models, which served as the foundation for model selection and tuning. Beyond technical work, I helped manage the overall project workflow—ensuring we stayed on track with deadlines, maintained high-quality standards, and collaborated effectively as a team.
## Challenges Encountered
Our team faced several challenges throughout the project:

Data Quality and Completeness: The dataset contained missing values and inconsistencies, which required careful cleaning and imputation to prepare it for analysis.

High-Dimensional Feature Space: Working with a large number of variables posed challenges in terms of feature selection, increasing the risk of overfitting and requiring thoughtful dimensionality reduction strategies.

Time Management: Exploring multiple modeling techniques while meeting tight deadlines demanded efficient coordination, clear task delegation, and continuous prioritization of key deliverables
## Key Learnings
This project provided valuable hands-on experience in applying data science techniques to solve real-world business problems. Key takeaways include:

End-to-End Data Workflow: I gained a deeper understanding of the entire analytics pipeline—from data cleaning and exploratory analysis to model building and interpretation.

Model Selection and Evaluation: I learned how to compare multiple machine learning models based on both performance metrics and business context, and how to balance complexity with interpretability.

Collaboration and Project Management: Working in a team setting strengthened my communication and coordination skills, especially under time constraints.

Business-Driven Decision Making: I learned how to align technical outputs with strategic business goals, such as optimizing delivery logistics and improving customer segmentation.
