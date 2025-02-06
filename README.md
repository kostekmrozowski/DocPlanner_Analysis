# DocPlanner_Analysis - Pricing analysis and Pricing Policy optimization for Jameda

**Jameda Pricing Strategy & Churn Risk Analysis**

## **Objectives**

- **Price Policy Suggestion**: Develop a data-driven pricing strategy based on customer engagement and churn risk.
- **Assign Next Price for Customers**: Recommend an optimized price for each customer, balancing revenue potential and churn risk.
- **Estimate Final Monthly Revenue**: Forecast expected monthly revenue by accounting for customer retention and potential churn
  
# **Short Overview**

# **Full Overview**


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

#### **Churn Risk & Pricing:**

- **Churn Risk Score**: Calculated as:  
    (2 × Standardized Price-Usage Fit) - (0.5 × Standardized Engagement Score)
- **Churn Risk Quartiles**: Customers segmented into four risk categories: Low, Medium, High, Critical.
- **Normalized Engagement**: Normalized version of Engagement Score using the min-max method.
- **Optimized Price**: Suggested price based on Price Usage Fit and churn risk tolerance.
- **New Churn Risk Score**: Updated churn risk score considering the engagement score and optimized price.

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

**Aggressive vs Moderate -> Table of Comparison**

| **Approach / KPIs** | **Segments with a Price Increase** | **Risk Threshold Level** | **Total Optimized Revenue:** | **Total Revenue Increase in %:** | **Break-Even Churn Count** | **Break-Even Churn Rate** |
| --- | --- | --- | --- | --- | --- | --- |
| **Aggressive Growth Approach** | Low and Moderate Risk | 14.4075 | €62,471.00 | 23.41% | 108 customers<br><br>(Medium & Low Risk Segment) | 43.20%<br><br>(Medium & Low Risk Segment) |
| --- | --- | --- | --- | --- | --- | --- |
| **Moderate Growth Approach** | Low Risk | 5.5311 | €54,145.40 | 6.96% | 30 customers<br><br>(Low Risk<br><br>Segment) | 24.00%<br><br>(Low Risk): |
| --- | --- | --- | --- | --- | --- | --- |


**Assumptions:**

- Revenue Recognition: Revenue as in international standard, will be recognized with installment payments (break down into monthly payments)
- Price Difference Validity: In approximately 30 cases, the difference between the actual price and the price specified in the price name will be considered valid and not a data mistake
- 1€ Payment Plans: Customers on 1€ payment plans won’t be treated as special cases (in case such plans were supposed to support social causes like certain medical specializations.)

**Limitations:**

- Insufficient historical data prevents from assessing historical churn rates.
- The absence of data on fluctuations in average bookings prevents reasonable evaluation of client engagement patterns.
- Consequently, calculating key metrics like CLV, NRR, or price elasticity won’t be possible, nor performing regression analyses on the potential impact of price changes on churn rates.



**Contact**

For questions or contributions, please contact the Jameda data analytics team.


