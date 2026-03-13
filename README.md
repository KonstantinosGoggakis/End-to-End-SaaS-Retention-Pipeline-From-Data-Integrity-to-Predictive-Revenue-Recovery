SaaS Churn Analysis & Prediction
Project Overview

This project analyzes customer churn behavior in a SaaS environment and builds a predictive model to identify customers at risk of leaving. The goal is to transform raw behavioral, billing, and satisfaction data into actionable business insights that help reduce churn and protect revenue.

Dataset Overview

This dataset is particularly valuable because it captures multiple dimensions of customer behavior:

Engagement Depth

session_time

features_used

weekly_active_days

Engagement Trend

usage_growth_rate (very powerful indicator)

Contract Structure

Monthly vs Yearly subscriptions

Revenue & Billing Friction

payment_failures

price_increases

Customer Experience & Satisfaction

support_tickets

csat_score

nps_score

Data Cleaning & Feature Engineering

Several preprocessing steps were applied before analysis:

Data Cleaning

Fixed float formatting issues (comma → dot).

Handled missing values (e.g., replaced with No Complaint where appropriate).

Feature Engineering

Created new business metrics:

Ticket Intensity

Billing Risk

Frustration Index
(Support Tickets × Resolution Time)

Logical Data Corrections

Detected and investigated inconsistencies between variables.

Logical Consistency Checks

Two key consistency tests were performed.

Revenue Consistency
total_revenue vs monthly_fee

Result:

Revenue consistency errors: 0
Usage Consistency
weekly_active_days > 0 vs monthly_logins = 0

Result:

Usage consistency errors: 263
Why Does This Happen? (Business Context)

These inconsistencies can occur due to real system behavior.

Session Persistence

A user may have logged in previously, but their session cookie remains active, allowing continued activity without new login events.

Tracking Bug

Different tools may track different metrics:

Auth systems (e.g., Auth0) → track logins

Product analytics tools (e.g., Mixpanel) → track activity

If the login tracker fails, usage may still be recorded.

Correlation Analysis: Churn Drivers

Churn Drivers (Positive Correlation)

payment_failures (0.11)
The strongest churn driver. Confirms the hypothesis that billing friction pushes customers out.

last_login_days_ago (0.04)
The longer a user stays inactive, the higher the churn probability.

Loyalty Drivers (Negative Correlation)

csat_score (-0.16)
The strongest protective factor against churn. Higher satisfaction directly reduces churn.

tenure_months (-0.12)
Older customers tend to be more loyal.

monthly_logins (-0.08)
Higher engagement leads to stronger retention.

CSAT vs Payment Failures vs Churn

Business Insight

A surprising pattern emerged:

Some highly satisfied customers (CSAT 4–5) still churn due to billing issues.

Interpretation

This means churn is not always caused by dissatisfaction.

Instead, technical payment failures are forcing satisfied customers to leave.

Recommended Actions
Stop the Bleeding

Implement:

Smart Payment Retries

In-app payment alerts

before subscription expiration.

Dunning Campaigns

For customers with:

CSAT 4–5

Payment failure

communication should be supportive and proactive, not just a generic payment failure notification.

Executive Business Report
SaaS Churn Analysis & Revenue Recovery
Objective

Reduce churn and recover lost recurring revenue.

1. Overall Churn Situation

The company currently has a 10.4% churn rate.

However, a significant portion of this churn is caused not by dissatisfaction, but by billing friction.

We identified:

$69,350 Monthly Recurring Revenue (MRR) at risk

from customers who are satisfied but experiencing payment issues.

2. Key Insights
   A. Billing Friction — The Hidden Churn

Problem

Customers with payment failures show double the churn rate (9.16%), even when they report high satisfaction.

Insight

We are losing healthy customers who actually want to stay.

Impact

Approximately $69k MRR at risk.

B. The Feature Adoption "Magic Number"

Problem

Customers using fewer than 10 features maintain a churn rate around 10%.

Insight

Once customers reach 14 features used, churn drops close to 0%.

Impact

Feature adoption becomes a powerful retention shield.

C. Usage Engagement & Retention

Problem

Churn is highest in the first 6 months.

Insight

Customers with fewer than 20 logins per month are 3× more likely to churn.

Customer inactivity is often the first warning signal before cancellation.

D. Support Frustration

Using the Frustration Index:

Frustration Index = Support Tickets × Resolution Time

We found that extreme delays in support resolution create trust breakdowns, leading to churn among high-value customers.

3. Strategic Action Plan
   Department Action Expected Impact
   Finance Smart Retries + Dunning Emails Recover up to 30% of involuntary churn
   Product Gamified onboarding to reach 14 feature usage threshold Higher adoption and retention
   Customer Success Proactive outreach for customers with <15 logins/month Early churn prevention
   Support Priority queue for high Frustration Index customers Retain frustrated high-value clients
4. Machine Learning Prediction

A Random Forest / XGBoost churn prediction model was developed.

The model predicts customer churn probability with >80% accuracy.

Class imbalance was handled using:

SMOTE (Synthetic Minority Oversampling)

Feature Scaling

Revenue-Based Churn Prioritization

Not all churn risks are equally important.

Example:

A customer with 90% churn risk paying €10 is less critical than a customer with 60% churn risk paying €500.

Priority Framework
customer churn % monthly_fee priority
C102 65% €400 HIGH
C087 92% €30 MEDIUM

We therefore calculate:

Expected Loss = churn_probability × monthly_fee
Business Impact

With this system:

The Customer Success team can focus on the Top 100 customers representing the highest Revenue at Risk, instead of searching blindly across 10,000 accounts.

This allows for:

targeted retention campaigns

efficient resource allocation

measurable revenue protection

If you want, I can also help you add three things that make this README look like a senior data science project:

1️⃣ a project architecture section
2️⃣ a model performance section (ROC-AUC, Precision, Recall)
3️⃣ a final churn prediction dashboard
