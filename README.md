# DocPlanner_Analysis - Pricing analysis and Pricing Policy optimization for Jameda

Jameda Pricing Strategy & Churn Risk Analysis
Overview
Jameda is a SaaS platform that facilitates patient bookings at clinics while enabling clinical administration to manage timesheets, schedule visits, and allow doctors to communicate with patients and issue prescriptions. This project focuses on analyzing customer engagement, churn risk, and pricing optimization to maximize monthly recurring revenue (MRR).
Objectives
•	Price Policy Suggestion: Develop a data-driven pricing strategy based on customer engagement and churn risk.
•	Assign Next Price for Customers: Recommend an optimized price for each customer, balancing revenue potential and churn risk.
•	Estimate Final Monthly Revenue: Forecast expected monthly revenue by accounting for customer retention and engagement levels.
Data Description
The dataset consists of customer subscription information, engagement metrics, and pricing details.
Original Columns
Customer Data:
•	Customer ID: Unique identifier for the customer.
•	Cohort: The customer’s joining cohort.
•	Price: The amount the customer is paying (monthly, annually, or over 15 months depending on the invoicing period).
•	Price Name: Name of the pricing plan.
•	Commercial Type: Type of subscription plan (Platinum, Gold, Gold Pro).
•	Invoicing Period Length: Length of the invoicing period (in months).
•	Next Invoice At: Date of the next invoice.
Engagement Metrics:
•	Avg 3M Admin Bookings: Monthly average of patient visits scheduled by administration over the last three months.
•	Avg 3M User Bookings: Monthly average of visits scheduled through the marketplace over the last three months.
Location & Specialization:
•	City: City where the customer operates.
•	City ID: Unique identifier for the city.
•	Specialization Name: Name of the medical specialization.
•	Specialization ID: Unique identifier for the specialization.
Engineered Columns
Revenue & Engagement Metrics:
•	Recognized MRR: Price divided by the invoicing period to determine the monthly recognized revenue.
•	Normalized Admin Bookings: Normalized version of Avg 3M Admin Bookings using the min-max method.
•	Normalized User Bookings: Normalized version of Avg 3M User Bookings using the min-max method.
•	Normalized Revenue: Normalized version of recognized MRR using the min-max method.
•	Engagement Score: Engagement metric calculated as:
(1 × Standardized Admin Bookings + 1.25 × Standardized User Bookings)
•	Price Usage Fit: Measures how engaged a customer is relative to the price they are paying.
Churn Risk & Pricing:
•	Churn Risk Score: Calculated as:
(2 × Standardized Price-Usage Fit) - (0.5 × Standardized Engagement Score)
•	Churn Risk Quartiles: Customers segmented into four risk categories: Low, Medium, High, Critical.
•	Normalized Engagement: Normalized version of Engagement Score using the min-max method.
•	Optimized Price: Suggested price based on Price Usage Fit and churn risk tolerance.
•	New Churn Risk Score: Updated churn risk score considering the engagement score and optimized price.
Methodology
1. Data Preprocessing
•	Standardized engagement metrics using min-max normalization.
•	Computed monthly-recognized revenue.
•	Derived Price Usage Fit to assess how well a customer’s price aligns with their usage.
2. Churn Risk Analysis
•	Segmented customers into four quartiles based on churn risk scores.
•	Considered the impact of engagement levels on potential churn.
3. Price Optimization Strategy
•	Suggested optimized prices based on balancing revenue growth and churn minimization.
•	Adjusted pricing within acceptable churn risk thresholds.
4. Revenue Forecasting
•	Estimated future monthly revenue based on updated pricing and expected retention rates.
Assumptions
(To be defined based on project scope and constraints.)
Limitations
(To be defined based on data constraints and business factors.)
Future Enhancements
•	Implement machine learning models for dynamic pricing adjustments.
•	Develop real-time churn risk prediction dashboards.
•	Refine engagement score metrics with additional user activity features.
Contact
For questions or contributions, please contact the Jameda data analytics team.



