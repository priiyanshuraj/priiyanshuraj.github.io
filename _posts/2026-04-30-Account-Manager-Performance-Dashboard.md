---
layout: post
title: "Account Manager Performance Dashboard Breakdown"
date: 2026-04-30 00:00:00 +0800
categories: [Dashboard]
tags: [SaaS,Dashboard,BI,GTM]
---
[Access the Dashboard here](https://priyanshuraj.online/dashboard/amperformance.html "Click to go to Dashboard")

This dashboard is not just tracking performance, it is quietly mapping how existing customers are being managed, expanded, and retained. Unlike acquisition focused views, this one lives deeper in the lifecycle, where the real money is made or lost. It tells you whether relationships are growing, whether renewals are secure, and whether upsell opportunities are being captured effectively. Every number here is tied to a calculation, and those calculations reflect real account level behavior.

At the top, the filters define the scope before anything else is interpreted. The account name filter works on a dimension like [Account Name], allowing metrics to be narrowed down to specific clients. Theater and rep name filters segment data by geography and ownership, typically using fields like [Region] or [Sales Rep]. The close date filter is driven by a range condition such as [Close Date] >= Start Date AND [Close Date] <= End Date, which ensures all calculations operate within the selected time window. Status and opportunity type filters further refine the dataset using categorical conditions like [Status] = "Open" or [Opportunity Type] = "Upsell". The threading filter separates deals based on relationship complexity, usually derived from a field like [Threading Type]. All of these filters are applied across the dashboard, meaning every formula you see is evaluated only within this filtered context.

The first metric, ARR, represents annual recurring revenue and is calculated as ARR = SUM([Recurring Revenue]). This is the baseline value of the customer base and reflects the total contract value normalized annually. It is the foundation on which all other metrics build.

Upsell measures how much additional revenue is being generated from existing customers. It is typically calculated as Upsell Revenue = SUM(IF [Opportunity Type] = "Upsell" THEN [Deal Value] END). The percentage shown alongside it is often calculated as Upsell Rate = Upsell Revenue / ARR × 100, which indicates how much expansion is happening relative to the existing base.

Forecasted upsell introduces a forward looking element. It estimates expected expansion revenue based on deal probability and is calculated as Forecasted Upsell = SUM([Deal Value] × [Probability]) where [Opportunity Type] = "Upsell". The percentage component is often derived as Forecast Accuracy or Coverage, comparing forecasted values to targets.

Renewal rate measures how effectively existing contracts are being retained. It is calculated as Renewal Rate = Renewed Revenue / Total Renewable Revenue × 100, where Renewed Revenue is SUM(IF [Status] = "Renewed" THEN [Deal Value] END) and Total Renewable Revenue includes all contracts up for renewal. This metric directly reflects customer satisfaction and retention strength.

Renewals at risk highlights potential revenue loss. It is calculated as At Risk Revenue = SUM(IF [Risk Flag] = "At Risk" THEN [Deal Value] END), and the percentage is At Risk % = At Risk Revenue / Total Renewable Revenue × 100. This gives an early warning signal about accounts that may churn.

The win loss ratio provides a direct measure of success versus failure in account level opportunities. It is calculated as Win Loss Ratio = COUNTD(IF [Status] = "Closed Won" THEN [Opportunity ID] END) / COUNTD(IF [Status] = "Closed Lost" THEN [Opportunity ID] END). In some cases, it is also expressed as a percentage using Wins divided by total opportunities.

The renewal detail donut chart breaks down the renewal base into categories such as at risk, closed, and pipeline. Each segment is calculated using conditional aggregation. For example, At Risk Portion = SUM(IF [Status] = "At Risk" THEN [Deal Value] END) divided by SUM([Deal Value]) × 100, and similar calculations are used for closed and pipeline segments. The center value represents the total renewal base, calculated as SUM([Renewal Value]). This chart shows how secure the renewal revenue actually is.

The month over month amount closed chart tracks revenue realization over time. It is calculated as Monthly Closed Revenue = SUM(IF [Status] = "Closed Won" THEN [Deal Value] END) grouped by DATETRUNC('month', [Close Date]). This allows you to see whether revenue is growing consistently or fluctuating.

The month over month product usage chart adds a behavioral dimension. It tracks how customer engagement evolves over time, calculated as Product Usage = SUM([Usage Metric]) grouped by DATETRUNC('month', [Usage Date]). Increasing usage often correlates with higher retention and upsell potential, while declining usage can signal churn risk.

The single threaded versus multi threaded chart examines relationship depth within accounts. Revenue is split based on whether deals involve one contact or multiple stakeholders. This is calculated as SUM([Deal Value]) grouped by [Threading Type] and [Status]. The classification itself is usually derived from a condition like IF COUNTD([Contact ID]) > 1 THEN "Multi Threaded" ELSE "Single Threaded" END. This helps identify whether deeper engagement leads to better outcomes.

The opportunity detail table provides the most granular view. Each row represents an opportunity, with fields such as account name, opportunity name, rep name, type, threading, status, close date, and deal value. The deal value is simply [Deal Value], while sorting and highlighting are often based on measures like SUM([Deal Value]) or conditional formatting rules. This table acts as the raw layer beneath all aggregated metrics.

When you step back and look at the dashboard as a whole, the story becomes clear. Revenue is not just coming from new deals, it is being shaped by how well existing accounts are managed. The formulas show that upsell contributes additional growth, but renewal rate determines stability. At risk renewals highlight potential losses before they happen. Product usage signals future behavior, while threading shows the strength of relationships.

In the end, this dashboard feels less like a performance report and more like a quiet conversation about how your existing customers are really behaving. It shows you where relationships are strong, where revenue is expanding naturally, and where things might start slipping if ignored. The formulas underneath are doing the heavy lifting, but what you actually see is a story about trust, engagement, and timing. Some accounts are growing because they are being nurtured well, others are sitting in risk zones waiting for attention, and a few are already signaling what might go wrong next. When you look at it this way, you are not just tracking numbers anymore, you are understanding how sustainable your revenue actually is and where your next move should come from.
