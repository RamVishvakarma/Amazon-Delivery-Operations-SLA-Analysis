# Amazon Delivery Operations & SLA Analysis

## Project Overview

This project analyzes an Amazon-style delivery dataset to evaluate
**delivery performance, SLA compliance, delivery attempts, partner
performance, location patterns, and operational factors**.

The analysis was completed using **Microsoft Excel / PivotTables /
PivotCharts** with calculated delivery and SLA fields.

> **Dataset size:** 1,033 orders\
> **Delivered:** 995 (96.3%)\
> **Failed:** 38 (3.7%)\
> **Early:** 813 (78.7%)\
> **On Time:** 175 (16.9%)\
> **SLA Breached:** 45 (4.4%)

------------------------------------------------------------------------

## Business Objective

The objective is to answer operational questions such as:

1.  What is the overall delivery success rate?
2.  How many deliveries meet, beat, or breach the SLA?
3.  How does a second delivery attempt affect delivery time?
4.  Which delivery partners show higher SLA-breach rates?
5.  Which buyer/seller locations have higher breach or failure rates?
6.  How do traffic and weather relate to delivery performance?
7.  Which vehicle and product categories show different delivery
    patterns?
8.  What operational actions could be considered from the analysis?

------------------------------------------------------------------------

## Dataset

The dataset contains **1,033 records and 23 columns**.

### Main Fields

  Field                     Description
  ------------------------- ----------------------------------
  Order_ID                  Unique order identifier
  Delivery_Partners         Delivery service/partner
  Agent_Rating              Delivery agent rating
  Sellers location          Seller location
  Buyers Location           Buyer location
  Order_Date                Order date
  Order_Time                Order time
  Pickup_Time               Pickup time
  Weather                   Weather condition
  Traffic                   Traffic condition
  Vehicle                   Delivery vehicle
  Area                      Area classification
  Exp 1st Attempt days      Expected days for first attempt
  Actual 1st Attempt days   Actual days for first attempt
  Status                    Result of first attempt
  Exp 2nd Attempt days      Expected days for second attempt
  Actual 2nd Attempt days   Actual days for second attempt
  Final delivery Status     Final delivered/failed result
  Total Attempt             Number/result of attempts
  Exp Total Days            Expected total delivery days
  Actual Total Days         Actual total delivery days
  SLA Status                Early / On Time / SLA Breached
  Category                  Product category

------------------------------------------------------------------------

## Data Preparation

The following preparation was performed before analysis:

-   Removed leading/trailing spaces from categorical fields.
-   Converted delivery-day and rating fields to numeric values.
-   Checked for missing values.
-   Standardized the interpretation of delivery status and SLA status.
-   Added/used calculated fields for total attempts, expected total
    days, actual total days, and SLA status.
-   Built PivotTables and PivotCharts for operational analysis.

### SLA Logic

The analysis compares **Actual Total Days** with **Expected Total
Days**:

-   **Early:** Actual Total Days \< Expected Total Days
-   **On Time:** Actual Total Days = Expected Total Days
-   **SLA Breached:** Actual Total Days \> Expected Total Days

------------------------------------------------------------------------

# KPI Summary

  KPI                                      Result
  -------------------------------- --------------
  Total Orders                              1,033
  Delivered Orders                            995
  Failed Orders                                38
  Delivery Success Rate                    96.32%
  Delivery Failure Rate                     3.68%
  Early Deliveries                   813 (78.70%)
  On-Time Deliveries                 175 (16.94%)
  SLA Breaches                         45 (4.36%)
  Average Expected Delivery Days             5.25
  Average Actual Delivery Days               2.32
  Average Agent Rating                       4.08
  First-Attempt Deliveries                    818
  Second-Attempt Deliveries                   177

------------------------------------------------------------------------

# Key Questions and Answers

## 1. What is the overall delivery performance?

**Answer:** 995 of 1,033 orders were delivered, giving a delivery
success rate of **96.32%**. 38 orders were recorded as failed.

**Interpretation:** The dataset shows a high overall delivery completion
rate, but the failed orders should still be investigated because
failures represent direct operational exceptions.

------------------------------------------------------------------------

## 2. How is SLA performance distributed?

-   **Early:** 813 orders (78.70%)
-   **On Time:** 175 orders (16.94%)
-   **SLA Breached:** 45 orders (4.36%)

**Answer:** The majority of records are classified as early, while 45
orders are classified as SLA breached.

**Important:** SLA compliance should be interpreted separately from
final delivery success. An order can be delivered successfully but still
breach its expected delivery time.

------------------------------------------------------------------------

## 3. Does a second attempt affect delivery time?

There are **818 first-attempt deliveries** and **177 deliveries
requiring a second attempt** among successful deliveries.

The dataset's average actual total delivery time is **2.32 days**
overall.

**Answer:** Orders requiring additional attempts should be monitored
because repeated attempts can increase operational effort and delivery
duration. A PivotTable comparing `Total Attempt` against
`Actual Total Days` and `SLA Status` is recommended.

------------------------------------------------------------------------

## 4. Which delivery partners have higher SLA-breach rates?

  Partner        Orders   SLA Breach %   Failure %   Avg Actual Days
  ------------ -------- -------------- ----------- -----------------
  UPS               263          6.84%       4.18%              2.16
  India Post        163          5.52%       5.52%              2.51
  FedEx             213          5.16%       5.16%              2.36
  DHL               195          2.56%       2.56%              2.46
  Dehlivery         199          1.01%       1.01%              2.19

**Answer:** In this dataset, **UPS** has the highest observed SLA-breach
rate among the listed delivery partners (6.84%). This is a descriptive
result for this dataset and should not be interpreted as proof that the
partner causes delays; order mix and route characteristics may differ.

------------------------------------------------------------------------

## 5. Does traffic appear related to SLA performance?

  Traffic     Orders   SLA Breach %   Failure %   Avg Actual Days
  --------- -------- -------------- ----------- -----------------
  Jam            318          5.66%       5.35%              2.21
  Low            371          5.39%       4.31%              2.42
  Medium         249          2.41%       1.61%              2.39
  High            95          1.05%       1.05%              2.09

**Answer:** The highest observed SLA-breach rate is for **Jam traffic**
(5.66%). However, the relationship is not monotonic in this dataset, so
traffic alone should not be treated as the cause of SLA breaches.

------------------------------------------------------------------------

## 6. Does weather appear related to SLA performance?

  Weather        Orders   SLA Breach %   Failure %   Avg Actual Days
  ------------ -------- -------------- ----------- -----------------
  Stormy            167          6.59%       5.99%              2.11
  Sunny             158          6.33%       6.33%              2.63
  Windy             193          5.18%       4.15%              2.28
  Cloudy            168          3.57%       2.98%              2.31
  Sandstorms        161          2.48%       1.24%              2.16
  Fog               186          2.15%       1.61%              2.42

**Answer:** **Stormy** has the highest observed SLA-breach rate (6.59%).
This is an association within the dataset, not evidence of causation.

------------------------------------------------------------------------

## 7. Which areas show different delivery performance?

  Area              Orders   SLA Breach %   Failure %   Avg Actual Days
  --------------- -------- -------------- ----------- -----------------
  Urban                 55         18.18%       5.45%              1.64
  Metropolitian        978          3.58%       3.58%              2.36

The `Area` field is highly concentrated: most records are classified as
metropolitan, so comparisons with the smaller urban group should be
interpreted cautiously.

------------------------------------------------------------------------

## 8. Which buyer locations have higher SLA-breach rates?

The highest observed breach rates occur in some smaller buyer-location
groups. For example:

-   **Worli:** 18.18% breach rate across 55 orders.
-   **Vikhroli:** 14.29% breach rate across 56 orders.
-   **Khopoli:** 9.30% breach rate across 43 orders.
-   **Borivali:** 6.12% breach rate across 49 orders.
-   **Bandra:** 5.77% breach rate across 52 orders.

Location-level rates should always be viewed together with order volume.
A high percentage based on a small number of orders is less stable than
a similar percentage based on hundreds of orders.

------------------------------------------------------------------------

## 9. What categories show higher breach rates?

  Category         Orders   SLA Breach %   Failure %
  -------------- -------- -------------- -----------
  Toys                 77          9.09%       7.79%
  Sports               70          8.57%       5.71%
  Apparel              64          6.25%       6.25%
  Outdoors             51          5.88%       5.88%
  Skincare             60          5.00%       5.00%
  Cosmetics            63          4.76%       4.76%
  Grocery              62          3.23%       1.61%
  Kitchen              62          3.23%       3.23%
  Clothing             63          3.17%       1.59%
  Home                 63          3.17%       3.17%
  Books                65          3.08%       3.08%
  Jewelry              65          3.08%       1.54%
  Snacks               69          2.90%       2.90%
  Electronics          70          2.86%       2.86%
  Shoes                70          2.86%       1.43%
  Pet Supplies         59          1.69%       1.69%

**Answer:** **Toys** has the highest observed SLA-breach rate (9.09%) in
this dataset. This should be treated as a segment to investigate rather
than a causal conclusion.

------------------------------------------------------------------------

# PivotTable Design

## PivotTable 1 --- KPI Summary

**Values** - Count of Order_ID - Count of Final delivery Status - Count
of SLA Status - Average Actual Total Days - Average Total Attempt

## PivotTable 2 --- SLA by Area

**Rows:** Area\
**Columns:** SLA Status\
**Values:** Count of Order_ID

## PivotTable 3 --- Delivery Partner Performance

**Rows:** Delivery_Partners\
**Columns:** SLA Status\
**Values:** Count of Order_ID, Average Actual Total Days

## PivotTable 4 --- Attempt Analysis

**Rows:** Total Attempt\
**Values:** Count of Order_ID, Average Actual Total Days

## PivotTable 5 --- Root-Cause Analysis

Use: - Traffic - Weather - Vehicle - Category - Buyer Location

against: - SLA Status - Final delivery Status - Actual Total Days

------------------------------------------------------------------------

# Recommended Dashboard

The final Excel dashboard can contain:

1.  **Total Orders**
2.  **Delivery Success %**
3.  **SLA Breach %**
4.  **Average Actual Delivery Days**
5.  **SLA Status chart**
6.  **Delivery Partner comparison**
7.  **Area/location comparison**
8.  **First vs second attempt analysis**
9.  **Traffic and weather analysis**
10. **Slicers** for partner, area, weather, traffic, vehicle, category,
    and SLA status.

### Suggested Dashboard Flow

`Order Volume → Delivery Outcome → SLA → Attempts → Partner/Location → Root Cause`

------------------------------------------------------------------------

# Operational Insights

Based on the dataset:

-   Delivery completion is high at **96.32%**.
-   **45 orders (4.36%)** are classified as SLA breached.
-   Second-attempt orders represent an operational workload that should
    be monitored separately.
-   Partner-level performance varies and should be evaluated using rates
    as well as order volume.
-   Traffic and weather show different breach rates across categories,
    but the dataset does not establish causality.
-   Some buyer locations have materially different breach/failure rates.
-   Product categories also show different delivery patterns.
-   Smaller groups should be interpreted cautiously because percentages
    can be sensitive to sample size.

------------------------------------------------------------------------

# Recommendations

1.  **Monitor SLA breaches by partner and location** rather than relying
    only on overall SLA.
2.  **Track first-attempt success** because repeated attempts add
    operational workload.
3.  **Investigate high-breach locations** using route, distance, and
    delivery-volume information.
4.  **Segment traffic/weather conditions** when reviewing exceptions.
5.  **Use both counts and percentages** to avoid overreacting to small
    samples.
6.  **Create an exception report** for failed deliveries and
    SLA-breached orders.
7.  **Review data-quality rules** before using the dashboard for real
    operational decisions.

------------------------------------------------------------------------

# Limitations

-   This is a dataset-level descriptive analysis, not a causal study.
-   The `Area` field is heavily concentrated in one category.
-   Some location/category groups have relatively small order volumes.
-   Traffic and weather should not be interpreted as direct causes
    without additional controlled analysis.
-   The analysis does not contain all potentially important operational
    variables such as route distance, warehouse processing time,
    capacity, or geographic coordinates.
-   The calculated `Actual Total Days` and `SLA Status` should be
    validated against the exact business definition used by the
    organization before production use.

------------------------------------------------------------------------

# Tools Used

-   Microsoft Excel
-   Excel PivotTables
-   Excel PivotCharts
-   Excel formulas
-   CSV dataset
-   Data cleaning and exploratory analysis

------------------------------------------------------------------------

# Skills Demonstrated

**Operations Analytics \| SLA Analysis \| Delivery Performance \| KPI
Reporting \| Excel \| PivotTables \| PivotCharts \| Data Cleaning \|
Root-Cause Analysis \| Operational Reporting**

------------------------------------------------------------------------

# Project Outcome

This project demonstrates how raw delivery records can be transformed
into an operations-focused performance dashboard covering **delivery
success, SLA compliance, attempts, partner performance, location
patterns, and potential operational drivers**.

The project is designed to demonstrate practical analytical thinking for
**Operations, Quality, Supply Chain, Logistics, and Business Operations
roles**.
