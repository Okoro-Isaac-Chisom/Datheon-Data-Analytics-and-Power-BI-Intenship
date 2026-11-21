# Datheon Data Analytics & Power BI Internship

**Author:** Okoro, Isaac Chisom  |  **LinkedIn:** [www.linkedin.com/in/isaac-chisom-okoro]

This repository contains my completed tasks for the Datheon Data Analytics & Power BI Internship. Each task has its own folder with the data, the work files, the reports and the technical documentation.

## Tasks completed

| Task | Topic | Tools | Deliverables |
|---|---|---|---|
| **1** | [Exploratory Data Analysis on Superstore Retail Sales](Task1_Superstore_EDA/) | Python (pandas, matplotlib, seaborn), Jupyter | Notebook with data cleaning code and 6 annotated business findings |
| **2** | [Interactive Executive Sales & Profit Dashboard](Task2_Superstore_PowerBI_Dashboard/) | Power BI Desktop, DAX, Power Query | `.pbix` file and exported PDF dashboard report |
| **3** | [Customer Cohort & Churn Analytics](Task3_Telco_Churn_Analytics/) | Power BI Desktop, DAX, Power Query | `.pbix` file with cohort retention matrix, churn analysis report (PDF) and retention recommendations |

## Repository structure

```
Datheon_Data_Analytics_Power_BI_Internship/
├── README.md
├── Task1_Superstore_EDA/
│   ├── notebook/         Task1_Superstore_EDA.ipynb
│   └── data/             superstore_sales.csv
├── Task2_Superstore_PowerBI_Dashboard/
│   ├── data/             superstore_sales.csv
│   ├── powerbi/          Power BI .pbix file
│   ├── reports/          exported PDF dashboard
│   └── docs/             Technical_documentation.md (model, Power Query steps, DAX)
└── Task3_Telco_Churn_Analytics/
    ├── data/             telco_customer_churn.csv
    ├── powerbi/          Power BI .pbix file
    ├── reports/          Telco_Churn_Analysis_Report.pdf, exported PDF dashboard
    └── docs/             Technical_documentation.md (model, Power Query steps, DAX)
```

## Key results

### Task 1: Superstore EDA
Cleaned 10,800 raw rows to **9,994 order lines** (806 non-order rows removed: a People table and a Returns list pasted below the data). Total sales **$2,297,200.86**, total profit **$286,397.02**.
1. Discounts above 20% are almost always loss-making (96.8% of those lines, against 6.1% at 20% or below).
2. Furniture earns 32.3% of sales but only a 2.49% margin; Tables lose $17,725.
3. September to December produce 51.6% of annual sales.
4. The Central region has the lowest margin (7.92%) and the deepest average discounts (24.0%).
5. 98.5% of customers are repeat buyers, but 155 customers are loss-making.
6. Sales grew 51.4% from 2015 to 2018, while margins levelled off at about 13%.

### Task 2: Executive Sales & Profit Dashboard
A two-page Power BI dashboard on a star schema (Fact_Orders, Dim_Customers, Dim_Product, Dim_Date): KPI cards, a monthly sales trend, category and regional treemaps, a product profitability matrix, and date, year and region slicers. Headline figures: **$2,297,201 sales, $286,397 profit, 12.47% margin, 5,009 orders**. Tables, Bookcases and Supplies are the only loss-making sub-categories.

### Task 3: Customer Cohort & Churn Analytics
Analysis of 7,043 telecom customers. Baseline churn is **26.54%** (1,869 customers).
- Month-to-month contracts churn at 42.71%, against 11.27% (one year) and 2.83% (two year).
- Customers in their first 12 months churn at 47.44%; first-year customers account for 55.5% of all churn.
- Electronic-check payers churn at 45.29%, against 15% to 19% for other methods.
- Fiber optic customers without Tech Support churn at **49.37%** (1,101 of 2,230 customers).

See `Task3_Telco_Churn_Analytics/reports/Telco_Churn_Analysis_Report.pdf` for the full report and recommendations.

## How to view the work
- **Task 1:** open the notebook on GitHub. All outputs and charts are saved in it. To re-run it, install pandas, matplotlib and seaborn, and keep the CSV in the `data` folder.
- **Tasks 2 and 3:** open the `.pbix` files in **Power BI Desktop** (free, Windows). The PDF exports and screenshots in each task folder show the finished dashboards without needing Power BI.

## Data sources
- Superstore sales data (Tasks 1 and 2)
- IBM Telco Customer Churn dataset (Task 3)
## Note
No work email to be able to publish power bi report.