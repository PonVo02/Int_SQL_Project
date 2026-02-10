# Intermediate SQL - Sales Analysis

## Overview
Analysis of customer behavior, retention, and life time value for an e-commerce company to improve customer retention and maximize revenue.

## Business Questions
1.**Customer Segmentation**: Who are our most valuable customer?

2.**Cohort Analysis**: How do different customer groups genarate revenue?

3.**Retention Analysis**: Who hasn't purchased recently?

## Analysis Approach

### 1. Customer Segmentation
- Categorized customer based on total lifetime value (LTV)
- Assigned customers to High, Mid, Low - value segments
- Calculated key metrics: total revenue

Query: [1_customer_segmentation.sql](/1_customer_segmentation.sql)

**Visualization**

![Customer_segment](/images/Customer_segment.png)

**Key Findings**
- **High-value** generates ~ 65.74% of total LTV with only ~ 25% of customer
- **Mid-value** accounts for ~32.17% of total LTV and ~ 50% of customer
- **Low-value** contributes ~ 2.08% of total LTV while representing ~ 25% of customers.

**Business Insights**
- **High-value** Retaining High-value customers should be the top priority because small churn changes can create outsized revenue impact. Because a large share of LTV sits in the High-value segment, revenue is higly sensitive to High-value churn. 

- **Mid-value** is the largest customer base and the most scalable source for growth. -> Sustainable growth is driven by moving a portion of Mid-value customer into High-value (increase purchase frequency, basket size, and cross-sell adoption), not only by acquiring new users
- **Low-value** customers contribute little to total LTV, so heavy-touch campaigns can hurt unit economics -> use low-cost automation and lightweight win-back while keepiing acquistion and servicing costs under tight control.


### 2. Cohort Analysis
- Tracked revenue and customer count per cohorts
- Cohorts were grouped by year of first purchase
- Analyzed customer retention at a cohort level

Query: [2_cohort_analysis.sql](/Scripts/2_cohort_analysis.sql)

**Visualization**

![cohort_analysis](/images/Cohort_analysis.png)


**Key Findings**
- **Peak scale:** total_net_revenue highest in 2019 (~22.26M), strong years also 2018(~20.64M) and 2022(~20.57M)
- **Best customer value:** customer_revenue highest in 2016–2017 (~3.03k/customer) -> cohorts with higher first-order value.
- **Value deterioration after 2020:** customer_revenue drops from ~2.87k (2019) to 2.29k (2020), then continues down to 1.88k (2024).
- **Volume vs value mismatch:** 2022 has the largest customers (9,010) and high total revenue, but low avg value (~2.28k/customer) → growth driven more by volume than customer quality.


**Business Insights**
- **Cohort quality is declining:** Newer cohorts (2020→2024) spend less on their first purchase, suggesting changes in product mix, pricing/discount intensity, acquisition channels, or customer targeting.
- **Growth mode shift:** 2022 looks like acquisition-led growth (more customers) but with weaker first-order value. If costs rose (ads/discount), profitability may be pressured even when revenue holds.


### 3. Retention Analysis
- Identified customer at risk of churning
- Analyzed last purchase patterns
- Calculated customer - specific metrics

Query: [3_retention_analysis](/3_retention_analysis.sql)

**Visualization**

![retention_analysis](/images/retention_analysis.png)

**Key Findings**
- **Churn dominates across cohorts:** Most cohorts show very high churn share (~90%+) with a small active share (~8–11%) based on the stacked bars.
- **Retention pattern is relatively flat:** Active share does not vary dramatically by cohort year -> the business likely has a systemic retention issue, not a single-year anomaly.
- **Slight pockets of better retention:** Some cohorts (e.g., around 2022) appear marginally higher active share, but differences are small.

**Business Insights**
- Retention is the biggest growth unlock: With churn this high, acquisition will “leak” unless lifecycle programs improve repeat buying.
- Win-back window is critical: Customers crossing the 6-month inactivity threshold are likely already cold; intervention needs to happen earlier (e.g., 30/60/90-day triggers).
- Segment-driven retention: Retention programs should prioritize High/Mid-value because the ROI is much higher than saving Low-value customers.

{Repeat for each analysis approach}


## Strategic Recommendations

### 1) Protect High-value 

- Prioritize retention for High-value customers (largest LTV share).
- Set early-warning triggers at 30/60/90 days since last purchase (don’t wait 6 months).
- Use personalized perks/offers (VIP benefits, targeted bundles) instead of broad discounting.

### 2) Upgrade Mid-value → High-value 

- Move part of the Mid-value base into High-value via:
- Increase frequency (reminders, lifecycle journeys)
- Increase basket size (bundles, threshold perks)
- Cross-sell (next-best product)

### 3) Improve Cohort Quality

- Cohort value is declining → optimize acquisition for quality, not just volume.
- Add guardrails using first-purchase value/customer and repeat within 60/90 days (if available).
- Reduce reliance on deep discounts that may drive low-value cohorts.

### 4) Lifecycle Retention System 

- Build retention actions by inactivity windows: 30 / 60 / 90 / 120 days.
- Run A/B tests for message + incentive levels; keep holdout to measure real lift.

### 5) Low-value = Automation Only 

- Use low-cost win-back (email/SMS/push) with strict promo caps.
- Avoid heavy-touch campaigns; focus resources on High/Mid.

## Technical Details
- **Database** PostgreSQL
- **Analysis Tools** PostgreSQL
- **Visualization:** ChatGPT