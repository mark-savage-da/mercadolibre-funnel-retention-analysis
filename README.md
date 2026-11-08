# MercadoLibre Funnel & Retention Analysis

## Project Overview

Where do shoppers drop out of the purchase journey, and when are new users less likely to return? This project uses SQL and Excel to examine the steps from a first visit to a purchase and measure activity during the first 28 days after signup. The largest drop in the funnel occurred between selecting an item and adding it to the cart. Only **14.32%** of users who selected an item added it to their cart.

## Business Context

The product team needs to decide where to focus its efforts. A drop before users add an item to the cart points to a different part of the shopping experience than a drop during checkout. Tracking activity after signup helps the team decide when to test a message that encourages users to return.

## Datasets Used

### 1. `mercadolibre_funnel`

The shopping events table records actions by user and session, along with the event date and country. These records describe the steps shoppers took between their first visit and a purchase. The funnel covers January 1 through August 31, 2025.

### 2. `mercadolibre_retention`

The retention table records activity after signup. It supports comparisons at 7, 14, 21, and 28 days and a breakdown by country. The executive retention summary covers users who signed up from January 1 through June 1, 2025.

## Project Objectives

- Identify the step where the largest share of users dropped out of the purchase journey.
- Measure how activity changed after signup and compare the results by country.
- Propose actions the product team can evaluate with conversion and retention metrics.

## Analytical Workflow

### 1. Data Loading and Initial Exploration

I used SQL to inspect the first rows of both tables and identify the events that make up the purchase journey. This established which events represented steps such as selecting an item, adding it to the cart, and completing a purchase.

### 2. Data Quality Review

I reviewed the table structure to identify the user, session, date, and activity fields used in the analysis. These fields distinguish actions during a shopping session from activity measured after signup.

### 3. Data Cleaning

Each part of the analysis uses a different date. The funnel uses the event date to define the shopping period. Retention uses each user's signup date as the starting point for measuring activity on the four follow-up days.

### 4. User-Level Aggregation

The funnel summarizes how users moved through the shopping journey from first visit to purchase. For retention, I grouped users by signup month. Each group of users who signed up in the same month is a **cohort**.

### 5. Descriptive Analysis

For the funnel, I compared the share of users who reached each next step. For retention, I compared the share of users who were active on each follow-up day. The workbook shows the overall results and the breakdown by country.

### 6. Data Visualization

Each bar shows the share of users who advanced from one funnel step to the next. The highlighted bar marks the step with the lowest conversion rate.

<p align="center">
  <img src="images/1_mercadolibre-funnel-conversion.png" alt="Conversion rates for five funnel steps. Item selection to cart has the lowest rate at 14.32%." width="760">
</p>

*Source · [Analysis workbook](mercadolibre-funnel-retention-analysis.xlsx), `Resumen` worksheet.*

The retention chart follows users who signed up in March 2025. Each point shows the share of that cohort who were active on the indicated day after signup.

<p align="center">
  <img src="images/2_mercadolibre-march-2025-cohort-retention.png" alt="Retention for users who signed up in March 2025. The active share was 87.7% on Day 7, 56.8% on Day 14, 26.6% on Day 21, and 3.0% on Day 28." width="760">
</p>

*Source · [Analysis workbook](mercadolibre-funnel-retention-analysis.xlsx), `Retencion x Cohort` worksheet.*

### 7. Outlier Detection

Among users who signed up in August 2025, **70.8%** were active on Day 7 and **0.2%** on Day 28. August falls outside the signup period used in the executive retention summary, so its results are presented separately here.

### 8. Customer Segmentation

The country breakdown shows how activity varied across markets. On Day 28, **3.2%** of users in Peru were active, compared with **3.1%** in Mexico and **1.6%** in Colombia.

### 9. Executive Insights

The funnel points to the product page as the first place to test a conversion improvement. The decline in activity during the second week after signup suggests a window to test a reminder. Each test would address a different point in the user journey.

## Key Tasks Performed

I explored the source tables in SQL, documented funnel and retention results in Excel, and compared results across countries and signup months. I prepared two charts to communicate the main conversion and retention patterns.

## Key Findings

- **Conversion.** From January through August 2025, **85.68%** of users who selected an item did not add it to the cart. This was the largest drop among the measured steps and makes the product page the first place to test a change.
- **Retention.** In the executive summary, **86.6%** of users were active on Day 7, **55.4%** on Day 14, and **2.6%** on Day 28. The **31.2 percentage-point** drop from Day 7 to Day 14 identifies when to test a reminder.

## Business Recommendations

- **Make delivery information easier to find.** Test whether showing shipping costs and estimated delivery dates on the product page increases the share of users who add an item to the cart. Track completed purchases to see whether the effect carries through checkout.
- **Test a reminder during the second week after signup.** Send a reminder between Day 7 and Day 14 to one group and compare its return rate with a similar group that receives no reminder.

## Tools and Skills

I used **SQL** to explore the tables and structure the conversion and retention analysis. I used **Excel** to organize the results, compare markets, and prepare the executive summary.

## Professional Value

The project connects two product decisions to measurable outcomes. A change to the product page can be evaluated through cart additions and completed purchases. A reminder can be evaluated through the share of registered users who return.

## Personal Voice & Learning

I learned to look at each step of the purchase journey before choosing where to intervene. Finding the largest drop between item selection and cart addition helped me propose a specific test of the information shoppers see before they decide.

## Repository Structure

```text
mercadolibre-funnel-retention-analysis/
├── images/
│   ├── 1_mercadolibre-funnel-conversion.png
│   └── 2_mercadolibre-march-2025-cohort-retention.png
├── README.md
└── mercadolibre-funnel-retention-analysis.xlsx
```

### File Guide

- [Analysis workbook](mercadolibre-funnel-retention-analysis.xlsx) · Executive summary and conversion and retention tables.
- [Charts](images/) · PNG files for the purchase funnel and the March 2025 signup cohort.

## Reproducibility Note

The [analysis workbook](mercadolibre-funnel-retention-analysis.xlsx) contains the values used in both charts. The `Resumen` worksheet shows conversion between steps, and `Embudo General` shows cumulative progress through the funnel. The retention chart uses the March 2025 row in `Retencion x Cohort`.
