# Hotel Booking Cancellation Analysis & Risk Prediction

> Root cause analysis of hotel booking cancellations using Python, hypothesis testing, API-driven weather enrichment, and business intervention modeling.

---

## Overview

Booking cancellations are one of the largest sources of revenue leakage in the hospitality industry. They create inventory uncertainty, distort demand forecasts, increase operational costs, and reduce profitability.

This project investigates cancellation behavior across a hotel booking platform experiencing an overall cancellation rate of approximately **19%**, significantly above the hospitality industry benchmark of **12%**.

The objective was to:

- Identify where cancellations are concentrated.
- Understand the underlying causes of cancellation behavior.
- Design interventions capable of reducing cancellation rates.
- Quantify the expected business impact of those interventions.

Rather than stopping at descriptive analytics, this project focuses on **hypothesis testing, root cause identification, and business decision-making**.

---

## Business Objective

### Current Situation
- Platform cancellation rate: **19.15%**
- Industry benchmark: **12%**
- Board target: **14% within two quarters**

### Goal
Reduce platform-wide cancellations through targeted interventions while minimizing customer friction and revenue loss.

---

## Dataset

The dataset contains approximately **12,000 hotel bookings** across multiple Indian cities and booking channels.

### Dataset Features

- Customer demographics
- Customer segment
- Loyalty tier
- Booking channel
- Booking status
- Booking date
- Check-in date
- Check-out date
- Property city
- Review ratings
- Number of rooms booked

---

# Project Workflow

```text
Raw Booking Data
        ↓
Data Validation
        ↓
Data Cleaning
        ↓
Exploratory Data Analysis
        ↓
Cancellation Landscape Analysis
        ↓
Hypothesis Testing
        ↓
Root Cause Analysis
        ↓
Intervention Design
        ↓
Business Impact Simulation
        ↓
Weather Enrichment Analysis
```

---

# Repository Structure

```text
hotel-booking-cancellation-analysis/
│
├── data/
│   ├── raw/
│   │   └── hotel_bookings.csv
│   │
│   └── processed/
│       └── cleaned_bookings.csv
│
├── notebooks/
│   └── hotel_booking_analysis.ipynb
│
├── src/
│   ├── data_cleaning.py
│   ├── hypothesis_testing.py
│   ├── weather_api_fetcher.py
│   └── impact_simulation.py
│
├── images/
│   ├── cancellation_heatmap.png
│   ├── lead_time_effect.png
│   ├── ota_city_analysis.png
│   ├── ota_month_analysis.png
│   ├── intervention_impact.png
│   ├── rainfall_analysis.png
│   └── temperature_analysis.png
│
├── reports/
│   └── hotel_booking_case_study.pdf
│
├── requirements.txt
├── README.md
└── .gitignore
```

---

# Data Cleaning & Validation

Before analysis, multiple data quality checks were performed to ensure reliable business insights.

## Validation Checks

### 1. Invalid Stay Periods
Bookings where:

```text
checkout_date <= checkin_date
```

### 2. Booking Before Customer Signup

Bookings where:

```text
booking_date < customer_signup_date
```

### 3. Zero-Room Bookings

Bookings with:

```text
num_rooms = 0
```

### 4. Cancelled Bookings with Reviews

Records where:

```text
booking_status = Cancelled
AND review exists
```

---

## Cleaning Results

| Metric | Value |
|-------|------|
| Original Records | 12,000 |
| Final Records | 11,661 |
| Removed Records | 339 |

Additional cleaning steps:

- Converted date columns to datetime format.
- Converted review scores to numeric values.
- Preserved loyalty tier `"None"` as a valid category rather than treating it as missing data.

---

# Cancellation Landscape Analysis

Cancellation rates were analyzed across:

- Property city
- Booking month
- Booking channel
- Customer segment

## Key Insight

Cancellations were not evenly distributed across the platform.

The largest concentration occurred in:

> **Goa during the monsoon season (June-August)**

This finding suggested that targeted interventions would likely outperform platform-wide policy changes.

---

## Cancellation Heatmap

![Cancellation Heatmap](images/cancellation_heatmap.png)

---

# Rate vs Volume Analysis

A high cancellation rate does not necessarily imply high business impact.

Therefore, cancellation segments were analyzed using two independent metrics:

## Highest Cancellation Rate Segments

- Goa OTA
- Jaipur OTA
- Bangalore OTA

## Highest Cancellation Volume Segments

- Bangalore OTA
- Chennai OTA
- Pune OTA

### Business Insight

Reducing cancellations in high-volume segments produces significantly larger platform-wide improvements than targeting only high-rate segments.

---

# Root Cause Analysis

Three competing hypotheses were tested to determine the primary drivers of cancellation behavior.

---

## Hypothesis 1 — Lead-Time Effect

### Hypothesis

Customers booking further in advance are more likely to cancel.

### Method

Cancellation rates were compared across:

- 0–7 days
- 8–30 days
- 31–90 days
- 90+ days

### Result

OTA bookings exhibited higher cancellation rates across every lead-time bucket.

The largest gap occurred in the:

> **31–90 day booking window**

### Verdict

✅ Partially Supported

Lead time increases cancellation risk but does not fully explain the OTA effect.

---

### Visualization

![Lead Time Effect](images/lead_time_effect.png)

---

## Hypothesis 2 — Geographic Effect

### Hypothesis

A small number of cities are driving the OTA cancellation problem.

### Method

OTA cancellation rates were compared across all cities.

### Result

OTA cancellation rates exceeded platform averages in nearly every city.

### Verdict

❌ Rejected

The issue is not driven by geographic outliers.

---

### Visualization

![OTA Cancellation by City](images/ota_city_analysis.png)

---

## Hypothesis 3 — Seasonal Effect

### Hypothesis

OTA cancellations increase only during specific seasons.

### Method

Monthly cancellation rates were compared across booking channels.

### Result

OTA cancellation rates remained consistently above Direct Website rates throughout the year.

### Verdict

❌ Rejected

The problem is not seasonal.

---

### Visualization

![OTA Monthly Analysis](images/ota_month_analysis.png)

---

# Final Conclusion

The strongest explanation was a:

> **Structural OTA Effect**

OTA bookings consistently demonstrate higher cancellation behavior regardless of:

- City
- Season
- Lead Time

This suggests customer behavior fundamentally differs by booking channel.

---

# Business Recommendation

## Target Segment

- OTA bookings
- 31–90 day lead times
- High-volume cities

## Proposed Intervention

Introduce a:

> **20–25% non-refundable deposit for OTA bookings made 31–90 days in advance**

Customers booking within shorter windows remain fully flexible.

---

## Why This Works

- Targets the highest-risk customer segment.
- Preserves flexibility for low-risk customers.
- Minimizes operational complexity.
- Reduces revenue leakage.

---

# Impact Simulation

Simulation results estimate:

| Scenario | Cancellation Rate |
|---------|------------------|
| Current Platform | 19.15% |
| OTA 31–90 Day Policy | 18.20% |
| All OTA 17% Deposit | 17.40% |
| All OTA 15% Deposit | 16.69% |
| OTA + Corporate Portal | 16.56% |
| Board Target | 14.00% |

### Estimated Outcome

- Prevent **207–291 cancellations**
- Reduce cancellation rate by **1.75–2.46 percentage points**

---

## Impact Visualization

![Impact Simulation](images/intervention_impact.png)

---

# Weather Cancellation Analyzer

As an extension project, historical weather information was integrated into booking data using the Open-Meteo Historical API.

---

## Motivation

The cancellation heatmap suggested that:

> Goa experiences unusually high cancellations during monsoon months.

The question became:

> Is it really the season causing cancellations, or is it specific weather conditions within that season?

---

## API Integration

Historical weather data was collected for:

- Goa
- Manali

Optimization strategy:

Instead of one API call per booking:

```text
booking rows → city-date aggregation → API calls
```

This reduced:

```text
1,582 potential API calls
↓
649 API calls
```

while preserving complete information.

---

## Weather Variables

### Rainfall Buckets

- No Rain
- Light Rain
- Moderate Rain
- Heavy Rain

### Temperature Buckets

- Cool
- Normal
- Hot
- Extreme

---

# Weather Findings

## Rainfall is More Important Than Temperature

Cancellation rate variation:

| Variable | Variation |
|---------|----------|
| Rainfall | 11.78 pp |
| Temperature | 6.63 pp |

---

## Heavy Rain Significantly Increases Cancellations

| Condition | Cancellation Rate |
|----------|------------------|
| Heavy Rain | 30.81% |
| Other Days | 21.38% |

Difference:

> **+9.43 percentage points**

---

## Effect Concentrated in Goa

| Segment | Cancellation Rate |
|---------|------------------|
| Goa Heavy Rain | 37.50% |
| Goa Other Days | 21.70% |

Difference:

> **+15.8 percentage points**

Interestingly, the same effect was almost absent in Manali.

---

## Business Opportunity

Combining booking data with weather forecasts enables:

- Dynamic cancellation risk scoring
- Proactive customer communication
- Free date-change offers
- Revenue protection strategies

---

# Tech Stack

## Languages
- Python
- SQL

## Libraries
- Pandas
- NumPy
- Matplotlib
- Requests

## Tools
- Jupyter Notebook
- Git
- GitHub

## APIs
- Open-Meteo Historical Weather API

---

# Skills Demonstrated

- Data Cleaning
- Exploratory Data Analysis
- Business Analytics
- Hypothesis Testing
- Root Cause Analysis
- API Integration
- Feature Engineering
- Data Storytelling
- Impact Simulation
- Stakeholder Communication

---

# Future Improvements

Potential extensions include:

- Machine Learning cancellation prediction model
- Customer-level risk scoring
- Dynamic pricing recommendations
- A/B testing framework
- Real-time weather forecasting integration
- Personalized intervention engine

---

# Author

**Mridul Kumar**

Delhi Technological University (DTU)  
Production and Industrial Engineering

Interested in:

- Business Analytics
- Product Analytics
- Data Analytics
- Consulting

---

## Connect

- LinkedIn: *Add your profile link*
- GitHub: *Add your GitHub profile link*
