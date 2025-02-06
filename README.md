# Pricing Analysis and Pricing Policy optimization by Konstanty Mrozowski

### **Table of Contents**

1. **Documents Description**
2. **Objectives**
3. **Data Description**
4. **Pricing Policy Optimization Logic**
5. **Aggressive vs Moderate Strategy**
    - **Table of Comparison**
6. **Overview of the Results**
7. **Assumptions**
8. **Limitations**
9. **Formulas and Definitions**
10. **Requirements List**

## **Documents Descriptions**
- **Chosen_aggressive_approach - Konstanty Mrozowski.ipynb** – The selected aggressive pricing model, with a step-by-step explanation of the approach and rationale.
- **Moderate_approach - Konstanty Mrozowski.ipynb** – The moderate pricing model, which was tested but found to be less effective compared to the aggressive approach.
- **Analysis_Results_Konstanty-Mrozowski.csv** – A CSV file containing key elements of the analysis, including computed prices
- **Full_Table_Konstanty-Mrozowski.csv** – A CSV file with all original and computed columns used in the analysis.

## **Objectives**

- **Price Policy Suggestion**: Develop a data-driven pricing strategy based on customer engagement and churn risk.
- **Assign Next Price for Customers**: Recommend an optimized price for each customer, balancing revenue potential and churn risk.
- **Estimate Final Monthly Revenue**: Forecast expected monthly revenue by accounting for customer retention and potential churn
  

## **Data Description**

The dataset consists of customer subscription information, engagement metrics, and pricing details.

### **Original Columns**

#### **Customer Data:**

- **Customer ID**: Unique identifier for the customer.
- **Cohort**: The customer’s joining cohort.
- **Price**: The amount the customer is paying (monthly, annually, or over 15 months depending on the invoicing period).
- **Price Name**: Name of the pricing plan.
- **Commercial Type**: Type of subscription plan (Platinum, Gold, Gold Pro).
- **Invoicing Period Length**: Length of the invoicing period (in months).
- **Next Invoice At**: Date of the next invoice.

#### **Engagement Metrics:**

- **Avg 3M Admin Bookings**: Monthly average of patient visits scheduled by administration over the last three months.
- **Avg 3M User Bookings**: Monthly average of visits scheduled through the marketplace over the last three months.

#### **Location & Specialization:**

- **City**: City where the customer operates.
- **City ID**: Unique identifier for the city.
- **Specialization Name**: Name of the medical specialization.
- **Specialization ID**: Unique identifier for the specialization.

### **Engineered Columns**

#### **Revenue & Engagement Metrics:**

- **Recognized MRR**: Price divided by the invoicing period to determine the monthly recognized revenue.
- **Normalized Admin Bookings**: Normalized version of Avg 3M Admin Bookings using the min-max method.
- **Normalized User Bookings**: Normalized version of Avg 3M User Bookings using the min-max method.
- **Normalized Revenue**: Normalized version of recognized MRR using the min-max method.
- **Engagement Score**: Engagement metric calculated as:  
    (1 × Standardized Admin Bookings + 1.25 × Standardized User Bookings)
- **Price Usage Fit**: Measures how engaged a customer is relative to the price they are paying.
- **Normalized Engagement**: Normalized version of Engagement Score using the min-max method.
- **Optimized Price**: Suggested price based on Price Usage Fit and churn risk tolerance.
- **price_change_%** – The percentage change between the current price and the optimized price, indicating the price adjustment impact.

#### **Churn Risk & Pricing:**

- **Churn Risk Score**: Calculated as:  
    (2 × Standardized Price-Usage Fit) - (0.5 × Standardized Engagement Score)
- **Churn Risk Quartiles**: Customers segmented into four risk categories: Low, Medium, High, Critical.
- **New Churn Risk Score**: Updated churn risk score considering the engagement score and optimized price.
- **New_churn_risk_segments** – The updated churn risk categorization (Low, Medium, High, Critical) after price adjustments.

## **Pricing Policy Optimization Logic**

1. **Standardization & Scoring**:  
    Min-Max normalization was applied to improve model accuracy. The Customer Engagement Score (CES), Pricing Usage Fit Score, and Churn Risk Score were defined.
2. **Segmenting Customers**:  
    Customers were divided into quartiles based on the Churn Risk Score and categorized as Low, Medium, High, or Critical risk.
3. **Setting a Pricing Threshold**:  
    The highest churn risk score within the Low (Moderate Approach) or Medium (Aggressive Approach) category was identified to ensure that price increases do not shift customers into a higher-risk group.
4. **Applying Price Increases**:  
    Price adjustments were implemented only for customers in the Low (Moderate) or Low and Medium (Aggressive) risk segments, with a maximum price capped at $195 (Platinum Package without discounts).
5. **Revenue Impact Analysis**:  
    Total revenue was calculated before and after price changes, and the potential number of customers who could churn before revenue losses offset gains was determined.
6. **Final Adjustments**:  
    The optimized pricing model was refined to ensure a net revenue increase while maintaining a sustainable churn rate.

### **Aggressive vs Moderate Strategy -> Table of Comparison**

| **Approach / KPIs** | **Segments with a Price Increase** | **Risk Threshold Level** | **Total Optimized Revenue:** | **Total Revenue Increase in %:** | **Break-Even Churn Count** | **Break-Even Churn Rate** |
| --- | --- | --- | --- | --- | --- | --- |
| **Aggressive Growth Approach** | Low and Moderate Risk | 14.4075 | €61,775.60 | 22.04% | 97 customers | 38.80% |
| --- | --- | --- | --- | --- | --- | --- |
| **Moderate Growth Approach** | Low Risk | 5.5311 | €53,798.01 | 6.28% | 27 customers | 21.60% |
| --- | --- | --- | --- | --- | --- | --- |


## **Overview and Results**

The **Aggressive Approach** proved to be significantly more valuable as it maximized revenue while maintaining a sustainable churn rate. This strategy led to a **22.04%** revenue increase (**€11,155.38 extra revenue**, bringing total revenue to **€61,775.60**), compared to the previous pricing model. In contrast, the **Moderate Approach** resulted in a **6.28%** increase (**€3,177.80 extra revenue**, bringing total revenue to **€53,798.01**).

Additionally, the **Aggressive Approach**  had a higher break-even churn capacity (**97 customers, 38.80% churn in Medium & Low-risk groups**) compared to the **Moderate Approach (27 customers, 21.60% churn in the Low-risk group**). This indicates that a more aggressive pricing adjustment was feasible without significantly increasing overall churn.

## **Assumptions:**

- Revenue Recognition: Revenue as in international standard, will be recognized with installment payments (break down into monthly payments)
- Price Difference Validity: In approximately 30 cases, the difference between the actual price and the price specified in the price name will be considered valid and not a data mistake
- 1€ Payment Plans: Customers on 1€ payment plans won’t be treated as special cases (in case such plans were supposed to support social causes like certain medical specializations.)

## **Limitations:**

- Insufficient historical data prevents from assessing historical churn rates.
- The absence of data on fluctuations in average bookings prevents reasonable evaluation of client engagement patterns.
- Consequently, calculating key metrics like CLV, NRR, or price elasticity won’t be possible, nor performing regression analyses on the potential impact of price changes on churn rates.

## **Formulas and Definitions:**

- **Engagement Score** = (1 × Standardized Admin Bookings) + (1.25 × Standardized User Bookings)  
    _Calculates how actively a customer uses the platform by combining admin bookings (by clinic staff) and user bookings (directly by patients), with extra weight on user bookings as they can drive revenue growth._
- **Price-Usage Fit Score** = Standardized Monthly Revenue / (Standardized Engagement Score + 0.01)  
    _Evaluates whether a customer is getting fair value for what they pay; a higher score indicates they are paying a lot relative to their usage (potential dissatisfaction), while a lower score suggests good value, with the 0.01 factor preventing division by zero._
- **Churn Risk Score** = (2 × Price-Usage Fit Score) − (0.5 × Engagement Score)  
    _Estimates the likelihood of a customer leaving by weighing price dissatisfaction (doubled effect) against engagement (negative effect, reducing risk for active users)._
- **Break-Even Churn Count:** _Number of customers that can churn before revenue returns to the original level._
- **Break-Even Churn Rate:** _Percentage of adjusted customers that can leave before revenue gains are nullified._

## **Requirements**
Used Libraries:
**pandas**: 2.2.3
**numpy**: 1.25.0
**matplotlib**: 3.8.0
**seaborn**: 0.13.2
