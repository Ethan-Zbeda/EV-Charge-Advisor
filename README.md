# EV Charge Advisor

## Overview

EV Charge Advisor is an AI-powered forecasting and recommendation platform designed to improve the workplace EV charging experience. Instead of relying on incomplete real-time charger telemetry, the platform leverages historical charging data and machine learning to forecast charging demand, identify congestion patterns, and recommend optimal charging opportunities for employees.

The solution helps employees plan charging sessions more effectively while providing leadership with actionable insights into charger utilization, congestion trends, and future infrastructure needs.

---

## Problem Statement

Workplace EV charging presents several challenges:

- Limited real-time visibility into charger availability
- Growing EV adoption and increasing demand for charging resources
- Employees spending time searching for available chargers
- Limited data availability due to partially connected charging infrastructure

With hundreds of employees enrolled in the workplace charging program and limited charger telemetry, a forecasting-based approach provides a scalable solution for improving charger accessibility.

---

## Solution

EV Charge Advisor uses historical charging session data to:

- Forecast charging demand
- Predict congestion levels
- Recommend optimal charging windows
- Estimate charger availability probability
- Provide AI-generated recommendations and explanations
- Support infrastructure planning and future charger deployment decisions

---

# Employee Dashboard

The Employee Dashboard provides personalized charging guidance to help employees maximize their chances of successfully finding charging opportunities.

### Features

#### Office Selector
Allows employees to select their office location.

#### Day / Time Selector
Enables employees to choose a desired charging day and arrival time.

#### Forecasted Congestion
Displays predicted charging demand and congestion levels throughout the day.

#### Recommended Charging Window
Identifies the optimal charging window based on forecasted demand patterns.

#### Availability Probability
Provides an estimated probability of finding an available charging opportunity during the selected time period.

#### AI Explanation
Generates a natural language explanation describing:

- Why a recommendation was made
- Expected congestion trends
- Best charging opportunities
- Confidence in the recommendation

---

# Leadership Dashboard

The Leadership Dashboard provides strategic insights into workplace charging utilization and infrastructure planning.

### Features

#### Fleet Overview KPIs
At-a-glance fleet metrics with month-over-month deltas: total charging sessions, total energy delivered (kWh), unique EV drivers, estimated charging ports, average energy per session, and average session duration.

#### Sustainability Impact
Translates energy delivered into environmental and cost outcomes using configurable assumptions (electricity cost and CO₂ saved per kWh): CO₂ avoided (tonnes), tree-year equivalents, gasoline offset (litres), and estimated fleet charging cost.

#### Utilization by Office
Side-by-side comparison of total charging sessions and total energy delivered across offices.

#### Monthly Demand Trend
Per-office monthly session and energy trends, plus a fleet-wide volume chart with a linear-regression trendline and a 3-month demand projection (reported as growing/declining at an estimated month-over-month rate).

#### Charger Utilization Rate
Average fraction of chargers in simultaneous use during business hours (6 AM – 8 PM) by office, color-coded by status — Healthy (< 45%), Moderate (45–70%), and Critical (≥ 70%, signalling a need for additional infrastructure).

#### Demand Heatmap
Day-of-week vs. hour-of-day utilization heatmap for a selected office, highlighting peak congestion windows.

#### Peak Demand Hours
Average charger utilization by hour across offices to pinpoint when demand concentrates.

#### Charging Efficiency – Idle Time Analysis
Quantifies time vehicles stay plugged in after charging completes (Total Duration − Charging Time): average idle time and total wasted charger-hours by office, plus a fleet-wide idle summary. Reducing idle time reclaims capacity without adding hardware.

#### Infrastructure Planning Summary
A sortable table ranking offices by utilization, with sessions, unique users, energy delivered, charger ports, sessions-per-charger, and capacity status to prioritize expansion.

#### Top Power Users
Top 10 drivers by energy consumed and by session count, anonymized to the last four digits of the User ID — useful for at-home charging subsidy or fleet-policy decisions.

#### AI Assistant
A natural-language assistant (local Ollama model) primed with live fleet context — utilization, trends, sustainability, and idle-time figures — for ad-hoc questions and capacity-planning guidance.

#### Filters & Assumptions
Filter by office and month; adjust electricity cost ($/kWh) and CO₂ saved per kWh to recalculate sustainability and cost estimates on the fly.

---

# Model Validation

The forecasting engine includes validation metrics to ensure prediction quality and transparency.

### Baseline vs Model Performance

The MVP forecast is a **historical occupancy model** rather than a black-box regressor, which keeps every recommendation explainable.

**Baseline — arrival-count average.** A naive forecast counts only when sessions *start*, averaging arrivals per office/day/hour. This systematically understates congestion because it ignores that a vehicle keeps occupying a charger long after it plugs in.

**Model — duration-weighted occupancy.** The dashboards spread every session across each hour the car stays plugged in (Total Duration), then average concurrent occupancy across all observed dates. Dividing by the number of charging ports yields an occupancy rate that drives the congestion level and availability probability. This captures sustained mid-day congestion the arrival-count baseline misses — e.g., a car that plugs in at 7 AM and unplugs at 11 AM counts against 7–10 AM, not just 7 AM.

**Demand projection.** For forward-looking planning, the Leadership Dashboard fits a least-squares linear regression over historical monthly session volume and projects the next three months, reporting the trend as a month-over-month growth rate.

> Note: figures are based on a sample of each site's chargers and reflect historical patterns, not live telemetry. Formal accuracy metrics (e.g., MAE / RMSE against held-out weeks) are a planned enhancement as connected-charger coverage grows.

---

# Business Value

## Time Saved

Reduces time spent searching for available chargers by helping employees identify optimal charging opportunities before arriving at a charging location.

## Reduced Employee Frustration

Provides greater visibility into charging demand and improves planning capabilities.

## Improved Charger Utilization

Encourages more balanced charger usage throughout the day by identifying lower-demand charging windows.

## Infrastructure Planning

Provides data-driven insights to support:

- Future charger expansion
- Site prioritization
- Capacity planning
- EV adoption forecasting

---

# Technical Approach

### Data Sources

- ChargePoint Charging Session Data
- Historical Charging Utilization Data

### Forecasting Inputs

- Office Location
- Day of Week
- Time of Day
- Historical Charging Sessions
- Seasonal Trends
- Charger Utilization Metrics

### Technologies

- Python
- Pandas
- Streamlit
- Plotly
- Scikit-Learn / XGBoost
- Azure OpenAI

---

# Future Enhancements

- Multi-office forecasting
- Real-time charger integrations
- Mobile application support
- Teams chatbot integration
- Personalized charging recommendations
- Infrastructure demand forecasting
- Reservation and scheduling capabilities

---

# Expected Outcomes

- Improved employee charging experience
- Reduced congestion during peak periods
- Better utilization of existing charging infrastructure
- Increased visibility into charging demand trends
- Data-driven infrastructure planning decisions

---

## Project Vision

> EV Charge Advisor empowers employees and leadership with AI-driven charging intelligence, transforming workplace EV charging from a reactive search process into a proactive planning experience.
