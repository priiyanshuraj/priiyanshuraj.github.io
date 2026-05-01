---
layout: post
title: "SaaS Sales Operation (GTM Ops) Dashboard Breakdown"
date: 2026-04-29 00:00:00 +0800
categories: [Dashboard]
tags: [SaaS,Dashboard,BI,GTM,Sales,Ops]
---
[Access the Dashboard here](https://priyanshuraj.online/dashboard/salesops.html "Click to go to Dashboard")


This dashboard is not just tracking sales performance, it is quietly mapping the entire journey of how deals are created, nurtured, and eventually closed. If you read it carefully, every section connects to the next, forming a complete picture of how the sales engine is functioning. What makes it powerful is that nothing here is random. Every card, every chart, and every number is the result of a calculation, and those calculations reflect real actions happening inside a sales team.

At the top, before any numbers appear, the filters and controls define the entire scope of analysis. The time filter, shown as year to date September 2025, is typically implemented using a condition like YEAR([Date]) = YEAR(TODAY()) along with a cutoff using TODAY() to restrict data to the current period. This means every metric, whether it is pipeline value or win rate, is calculated only for deals that fall within that timeframe. There is also a segment control, which allows KPIs to be broken down by a specific category. This is usually built using a parameter and a conditional calculation such as IF [Breakdown Toggle] = "Yes" THEN [Metric by Segment] ELSE [Overall Metric] END. This single control changes how every formula behaves, either aggregating everything together or slicing it into meaningful segments.

The dashboard begins with total pipeline value, which represents the sum of all active deals. This is calculated using Total Pipeline Value = SUM(IF [Stage] != "Closed Won" AND [Stage] != "Closed Lost" THEN [Deal Value] END). This number reflects potential revenue sitting in the pipeline, not revenue that has already been realized. The change indicator next to it is calculated using a year over year formula such as YoY % = (Current Period − Previous Period) / Previous Period × 100, often implemented in Tableau using LOOKUP or a date offset comparison. This immediately tells you whether the pipeline is growing or shrinking.

Right beside it, weighted pipeline value adds realism to this number. Not every deal has the same chance of closing, so each deal is multiplied by its probability. The formula becomes Weighted Pipeline Value = SUM([Deal Value] × [Win Probability]). The win probability is usually assigned based on the stage of the deal, for example early stage deals might have 10 percent probability while negotiation stage deals might have 80 percent. This transforms the pipeline into an expected value rather than just a raw total.

The average sales cycle length introduces a time perspective. It measures how long deals take to close and is calculated as Average Sales Cycle Length = AVG(DATEDIFF('day', [Created Date], [Closed Date])). If deals are still open, they are often excluded or calculated using TODAY() as a temporary end date. This metric shows whether deals are moving efficiently or getting stuck somewhere in the process.

Below these, the pipeline value by sales agent shows how deal value is distributed across individuals. It is calculated as SUM([Deal Value]) grouped by Sales_Rep. The weighted version of this uses SUM([Deal Value] × [Win Probability]) grouped the same way, which reveals not just who has the largest pipeline, but who has the most likely revenue. Similarly, average sales cycle length by agent is calculated as AVG(DATEDIFF('day', [Created Date], [Closed Date])) grouped by Sales_Rep, which helps identify who is closing deals faster or slower.

Win rate is where performance becomes measurable in terms of outcomes. It is calculated as Win Rate = COUNTD(IF [Stage] = "Closed Won" THEN [Deal ID] END) / COUNTD([Deal ID]). In many cases, this is refined to consider only closed deals, making it COUNTD(Closed Won) divided by COUNTD(Closed Won + Closed Lost). This metric shows how effectively opportunities are being converted into wins.

Closed won value translates this into actual revenue. It is calculated as Closed Won Value = SUM(IF [Stage] = "Closed Won" THEN [Deal Value] END). This is the portion of the pipeline that has successfully turned into business. When compared with total pipeline value, it reveals how much potential is actually being realized.

The top agent activity score introduces a behavioral layer. This is not about outcomes but about effort. It is typically calculated using a weighted formula such as Activity Score = (Calls × W1) + (Emails × W2) + (Meetings × W3) + (Demos × W4). Each activity is assigned a weight depending on its importance. The total score is then aggregated as SUM(Activity Score) grouped by Sales_Rep. This allows you to compare effort with results and understand whether higher activity leads to better performance.

The opportunity funnel on the right side shows how deals move through stages such as Lead, Qualified, Proposal, Negotiation, and Closed. The number of deals in each stage is calculated as COUNTD([Deal ID]) filtered by stage. The conversion between stages is calculated as Conversion Rate = Deals in Current Stage / Deals in Previous Stage × 100. This stepwise structure highlights exactly where deals are dropping off, making it easier to identify bottlenecks in the pipeline.

The deal size distribution within the funnel adds another layer of insight. Deals are grouped into buckets using a calculated field like IF [Deal Value] < 200000 THEN "0–200K" ELSEIF [Deal Value] < 400000 THEN "200–400K" END. The number of deals in each bucket is then calculated using COUNTD([Deal ID]). This helps you understand whether larger deals are progressing differently compared to smaller ones.

When the segment breakdown is enabled, additional analytical layers appear. Pipeline coverage becomes visible, which measures whether the pipeline is sufficient to meet targets. It is calculated as Pipeline Coverage = Total Pipeline Value / Sales Target. A value around three times the target is generally considered healthy, so anything lower indicates risk.

The win probability distribution shows how deals are spread across probability ranges. Deals are grouped into buckets such as 0 to 25 percent, 25 to 50 percent, and so on, and the percentage in each bucket is calculated as COUNTD(Deals in Bucket) / COUNTD(All Deals) × 100. This gives a sense of how risky or secure the pipeline is.

Average days in each funnel stage highlights where deals are slowing down. It is calculated as AVG(DATEDIFF('day', [Stage Entry Date], [Stage Exit Date])) for each stage. If one stage shows significantly higher values, it indicates a bottleneck that needs attention.

The reasons for lost deals provide insight into why deals are failing. Each reason is counted using COUNTD(IF [Stage] = "Closed Lost" THEN [Deal ID] END) grouped by Loss Reason. This helps identify patterns such as pricing issues, lack of response, or budget constraints.

The relationship between deals won and activities is shown using a scatter plot where deal value is plotted against activity score. The underlying calculations are SUM([Deal Value]) and SUM([Activity Score]) at the deal or agent level. This helps determine whether increased effort is actually leading to better outcomes.

The distribution of sales activities shows how effort is allocated across different actions such as calls, emails, meetings, and demos. It is calculated as SUM([Activity Count]) grouped by Activity Type. This reveals how the sales team is spending its time and whether that aligns with what drives conversions.

When you look at the entire dashboard as a whole, a very clear picture emerges. There is significant pipeline value and a high level of activity, but not all of it is translating into closed deals. The formulas behind each metric make this visible. The weighted pipeline is lower than the total pipeline, indicating uncertainty. The funnel shows drop offs at key stages. The activity scores show effort, but the win rate determines whether that effort is effective.

In the end, this dashboard is not just measuring sales performance. It is diagnosing the entire sales process. Every number is tied to a formula, and every formula reflects a real action inside the system. Once you understand those relationships, you are no longer just looking at a dashboard. You are understanding how the sales engine actually works.
