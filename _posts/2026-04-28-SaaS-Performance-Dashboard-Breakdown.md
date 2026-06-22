---
layout: post
title: "SaaS Performance Dashboard Breakdown"
date: 2026-04-28 00:00:00 +0800
categories: [Dashboard]
tags: [SaaS,Dashboard,BI,GTM]
---
[Access the Dashboard here](https://priyanshuraj.online/dashboard/salesgtm.html "Click to go to Dashboard")

A great dashboard does not just present numbers, it tells a story about how a business actually works beneath the surface. This SaaS Performance Dashboard is a strong example of that. It connects acquisition, behavior, and revenue into one continuous flow, so instead of isolated metrics, you get a system. What makes it even more powerful is that every visual you see is backed by a clear calculation. Once you understand those formulas, the dashboard stops being something you look at and becomes something you can reason with.

At the very top, the filters quietly define everything that follows. The year filter is typically derived using a calculation like YEAR(Date) which extracts the year from a date field such as signup or transaction date. The acquisition channel filter comes from a categorical field like Channel, while payment method is based on a field such as Payment_Type. Plan type comes from a subscription tier column, and region is derived from geographic attributes. In Tableau, these filters are applied across all worksheets using the same data source, which means every formula in the dashboard is recalculated within the selected context. For example, if the year is filtered to 2024, then even a simple aggregation like total revenue becomes SUM(IF YEAR(Date)=2024 THEN Revenue END). This is important because it ensures consistency across all metrics.

The story begins with active customers, which is the most basic representation of growth. It is calculated as a distinct count of users, written as COUNTD(Customer_ID). To make this meaningful over time, the dashboard compares it with the previous year using a year over year growth formula defined as YoY Growth % = (Current Year Customers − Previous Year Customers) / Previous Year Customers × 100. In Tableau, the previous year value is often calculated using a table calculation such as LOOKUP(SUM([Customers]), -1). This immediately tells you whether growth is accelerating or slowing, but growth alone is not enough to understand the health of the business.

To add depth, the dashboard introduces average customer lifespan, which measures how long users stay before they churn. This is calculated using Avg Customer Lifespan = AVG(DATEDIFF('month', Signup_Date, Churn_Date)). If churn date is null for active users, it is often replaced with TODAY() using IFNULL(Churn_Date, TODAY()). This metric is critical because it directly impacts how much value each customer can generate over time.

Churn then provides the necessary counterbalance. The number of churned customers is calculated as COUNTD(IF Status = 'Churned' THEN Customer_ID END). The churn rate is derived by normalizing this value, using Churn Rate = Churned Customers / Total Customers. Retention works in the opposite direction and is calculated as Retention Rate = (Customers at End of Period − New Customers) / Customers at Start of Period. These three metrics together define whether growth is sustainable or just temporary.

The acquisition channel chart explains where users are coming from. It is calculated as COUNTD(Customer_ID) grouped by Channel. This allows you to compare the contribution of Paid Ads, Organic, Referral, and other channels. A more advanced layer that can be added here is Customer Acquisition Cost, calculated as CAC = Total Marketing Spend / New Customers Acquired. Even when CAC is not shown explicitly, the chart hints at the tradeoff between volume and efficiency.

The plan type distribution shifts the focus from acquisition to monetization. It is calculated as COUNTD(Customer_ID) grouped by Plan_Type. From this, an important derived metric can be calculated as Free to Paid Conversion Rate = Paid Customers / Total Customers. The dominance of free users in the dashboard indicates that while acquisition is strong, monetization is not fully optimized.

The customer journey funnel makes this gap even more visible. Each stage is calculated using conditional distinct counts. Trial users are calculated as COUNTD(IF Stage = 'Trial Started' THEN Customer_ID END), converted users as COUNTD(IF Stage = 'Converted' THEN Customer_ID END), and upgraded users similarly. The key performance ratios are then calculated as Conversion Rate = Converted Users / Trial Users, Upgrade Rate = Upgraded Users / Converted Users, and Downgrade Rate = Downgraded Users / Converted Users. This structure clearly shows where users drop off, and in this case, the largest drop occurs between trial and conversion, which signals friction in onboarding or pricing.

The monthly comparison between free and paid users adds a time dimension to this behavior. It is calculated using COUNTD(Customer_ID) grouped by MONTH(Date) and segmented by Plan_Type. This allows you to observe trends in monetization over time and confirms whether improvements are consistent or temporary.

Regional distribution provides geographic context and is calculated as Region Share % = COUNTD(Customer_ID for Region) / COUNTD(Customer_ID overall) × 100. This helps identify where the business is strongest and where expansion opportunities exist.

The cohort retention heatmap is one of the most analytical components of the dashboard. Users are grouped by their signup month using a cohort identifier such as DATETRUNC('month', Signup_Date). Retention is then calculated as Cohort Retention % = Active Users in Month N / Users in Cohort Month 0 × 100. In Tableau, this often requires a FIXED level of detail expression such as { FIXED Cohort : COUNTD(Customer_ID) } to lock the cohort size at the initial month. This visualization reveals that most users drop off early, but those who stay tend to remain for longer periods.

When the dashboard transitions into revenue, the formulas shift from user counts to financial performance. The CAC to CLTV ratio is one of the most important metrics here. CAC is calculated as CAC = Total Sales and Marketing Cost / New Customers Acquired. CLTV is calculated as CLTV = ARPU × Avg Customer Lifespan. ARPU itself is defined as ARPU = Total Revenue / Total Customers. The ratio is then CAC:CLTV = CAC / CLTV, which indicates how efficient the business is at acquiring customers relative to their value.

Total revenue is calculated as SUM(Revenue Amount), while average revenue per user is calculated as ARPU = SUM(Revenue Amount) / COUNTD(Customer_ID). Net revenue retention is calculated as NRR = (Starting Revenue + Expansion Revenue − Churned Revenue − Contraction Revenue) / Starting Revenue × 100. This metric shows whether existing customers are generating more or less revenue over time, independent of new acquisitions.

Revenue by channel and plan uses similar aggregation logic, calculated as SUM(Revenue Amount) grouped by Channel or Plan_Type. This reveals that while free users dominate in number, higher tier plans contribute the majority of revenue.

The revenue concentration chart applies the Pareto principle using a running total calculation. Customers are sorted by revenue contribution, and cumulative revenue percentage is calculated as Running Sum % = RUNNING_SUM(SUM(Revenue)) / TOTAL(SUM(Revenue)) × 100. This shows that a small percentage of customers generate a large portion of total revenue, which highlights both opportunity and risk.

Finally, the MRR movement chart explains how recurring revenue evolves over time. It is built using multiple components. New MRR is the revenue from newly acquired customers, Expansion MRR is additional revenue from existing customers, Churn MRR is lost revenue from customers who leave, and Contraction MRR is reduced revenue from downgrades. The final calculation is Ending MRR = Starting MRR + New MRR + Expansion MRR − Churn MRR − Contraction MRR. This ties together acquisition, retention, and monetization into a single financial flow.

When you step back and look at the entire dashboard, the story becomes very clear. The business is strong at acquiring users and is improving retention, but it struggles to convert users into paying customers at scale. The formulas behind each metric reinforce this conclusion by showing exactly where value is being created and where it is being lost. Growth is strong, revenue is increasing, and efficiency metrics are healthy, but the gap between free users and paying customers remains the central challenge.

In the end, this dashboard is not just a visual tool. It is a structured representation of how a SaaS business operates. Every chart is a reflection of a formula, and every formula represents a real process in the business. Once you understand both, you are no longer just reading a dashboard, you are understanding the system behind it.

