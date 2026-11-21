# Task 3: Technical Documentation

## 1. Data preparation (Power Query)

**Source:** `data/telco_customer_churn.csv` (7,043 customers, 21 columns, one row per customer, no duplicate IDs).

| Step | Action | Reason |
|---|---|---|
| 1 | `TotalCharges`: Trim, change to Decimal Number, replace null with 0 | Stored as text with 11 blanks. All 11 are customers with tenure 0 (new, not yet billed), none of whom churned. |
| 2 | Set types: `tenure` whole number; `MonthlyCharges` decimal; `SeniorCitizen` whole number | |
| 3 | Add `ChurnFlag` (whole number) | Allows churn to be counted and averaged. |
| 4 | Add `Tenure Band` and `Tenure Band Order` | Six 12-month cohorts, with a numeric sort column. |
| 5 | Add `Charge Band` and `Charge Band Order` | Four monthly-charge bands, with a sort column. |
| 6 | Add `Senior Citizen` (Yes/No) | Readable label for slicers. |
| 7 | Name the query `Telco_Customers` | |

```
ChurnFlag = if [Churn] = "Yes" then 1 else 0

Tenure Band =
if [tenure] <= 12 then "0-12"
else if [tenure] <= 24 then "13-24"
else if [tenure] <= 36 then "25-36"
else if [tenure] <= 48 then "37-48"
else if [tenure] <= 60 then "49-60"
else "61-72"

Tenure Band Order =
if [tenure] <= 12 then 1 else if [tenure] <= 24 then 2 else if [tenure] <= 36 then 3
else if [tenure] <= 48 then 4 else if [tenure] <= 60 then 5 else 6

Charge Band =
if [MonthlyCharges] <= 35 then "$0-35"
else if [MonthlyCharges] <= 70 then "$35-70"
else if [MonthlyCharges] <= 90 then "$70-90"
else "$90+"

Charge Band Order =
if [MonthlyCharges] <= 35 then 1 else if [MonthlyCharges] <= 70 then 2
else if [MonthlyCharges] <= 90 then 3 else 4

Senior Citizen = if [SeniorCitizen] = 1 then "Yes" else "No"
```

`Tenure Band` is sorted by `Tenure Band Order`, and `Charge Band` by `Charge Band Order`.

**Note on service columns:** several columns (for example `TechSupport`) contain a third value, "No internet service", which is kept separate from "No".

## 2. DAX measures

```
Total Customers = COUNTROWS(Telco_Customers)
Churned Customers = SUM(Telco_Customers[ChurnFlag])
Churn Rate % = DIVIDE([Churned Customers], [Total Customers], 0)
Retention Rate % = DIVIDE([Total Customers] - [Churned Customers], [Total Customers], 0)
Avg Monthly Charges = AVERAGE(Telco_Customers[MonthlyCharges])
```

## 3. Cohort definition
The dataset records tenure but not signup dates, so a calendar cohort matrix is not possible. Cohorts are **tenure bands** crossed with **contract type**. The retention curve compares customers of different tenures at one point in time, so it approximates a retention curve and does not follow one group across time.

## 4. Report pages

**Cohort Retention.** Heatmap matrix of Retention Rate % (Tenure Band by Contract, gradient colouring), a matching matrix of customer counts, a retention curve by contract type, and slicers for Internet Service and Payment Method.

**High-Risk Segments.** Cards (Total Customers, Churn Rate %, Churned Customers), churn by payment method, churn by monthly charge band, a heatmap of churn by Internet Service and Tech Support (high churn shown red), and slicers for Senior Citizen and Contract.

## 5. Validation

| Check | Result |
|---|---|
| Customers / churned / churn rate | 7,043 / 1,869 / 26.54% |
| Contract churn | Month-to-month 42.71%; One year 11.27%; Two year 2.83% |
| Tenure band churn | 47.44%; 28.71%; 21.63%; 19.03%; 14.42%; 6.61% |
| Payment method churn | Electronic check 45.29%; Mailed check 19.11%; Bank transfer 16.71%; Credit card 15.24% |
| Monthly charge band churn | $0-35 10.89%; $35-70 23.94%; $70-90 37.80%; $90+ 32.78% |
| Fiber optic, no Tech Support | 49.37% (1,101 of 2,230) |
| Senior citizens | 41.68% (476 of 1,142) |

Each figure was checked against an independent calculation from the source CSV.

## 6. Deliverables
- Cohort retention matrix: `Cohort Retention` page of the Power BI file
- Churn analysis report and strategic retention recommendations: `reports/Telco_Churn_Analysis_Report.pdf`
