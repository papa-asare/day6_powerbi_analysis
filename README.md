# Day 6 – Power BI Data Modelling and DAX Measures

## Project Overview

This project uses Microsoft Power BI Desktop to analyse 180 accounting transactions covering January to June 2026. It builds on the Excel and SQL analyses completed during earlier stages of the AmaliTech Data Analytics Training.

The objective is to develop a financial reporting model using Power Query and DAX, evaluate financial performance, assess departmental budget utilisation, and reconcile Power BI results with SQL.

## Tools Used

- Microsoft Power BI Desktop
- Power Query Editor
- DAX (Data Analysis Expressions)
- SQL (for reconciliation)

## Data Preparation

The original accounting CSV dataset was imported into Power BI using the Text/CSV connector.

The dataset contains 180 records and nine columns, including transaction identifiers, dates, departments, categories, transaction types, actual amounts, budgeted amounts, payment methods, and locations.

Power Query was used to inspect the data types and confirm that date, numeric, and text fields were correctly recognised.

## Data Model

A single-table financial analysis model was created using the `accounting_analytics_practice_dataset` transaction table.

Seven DAX measures were developed to calculate financial performance and budget utilisation dynamically. Departmental analysis was performed using Power BI's filter context.

No table relationships were required for this single-table model.

## DAX Measures

### Total Revenue

```dax
Total Revenue =
CALCULATE(
    SUM('accounting_analytics_practice_dataset'[Actual_Amount_GHS]),
    'accounting_analytics_practice_dataset'[Type] = "Revenue"
)
```

### Total Expenses

```dax
Total Expenses =
CALCULATE(
    SUM('accounting_analytics_practice_dataset'[Actual_Amount_GHS]),
    'accounting_analytics_practice_dataset'[Type] = "Expense"
)
```

### Net Profit

```dax
Net Profit =
[Total Revenue] - [Total Expenses]
```

### Profit Margin

```dax
Profit Margin % =
DIVIDE([Net Profit], [Total Revenue], 0)
```

### Total Expense Budget

```dax
Total Expense Budget =
CALCULATE(
    SUM('accounting_analytics_practice_dataset'[Budget_Amount_GHS]),
    'accounting_analytics_practice_dataset'[Type] = "Expense"
)
```

### Expense Budget Variance

```dax
Expense Budget Variance =
[Total Expenses] - [Total Expense Budget]
```

### Budget Utilisation

```dax
Budget Utilisation % =
DIVIDE([Total Expenses], [Total Expense Budget], 0)
```

## Financial Performance Results

| Financial Metric | Result |
|---|---:|
| Total Revenue | GH₵318,721 |
| Total Expenses | GH₵456,287 |
| Net Profit / Loss | -GH₵137,566 |
| Profit Margin | -43.16% |
| Total Expense Budget | GH₵472,293 |
| Expense Budget Variance | -GH₵16,006 |
| Budget Utilisation | 96.61% |

## Departmental Budget Analysis

| Department | Actual Expenses (GH₵) | Budget (GH₵) | Utilisation |
|---|---:|---:|---:|
| Administration | 97,042 | 100,097 | 96.95% |
| Finance | 126,197 | 131,865 | 95.70% |
| Operations | 98,095 | 102,026 | 96.15% |
| Sales | 134,953 | 138,305 | 97.58% |

All four departments recorded actual expenses below their respective budgets.

## Key Insights

1. The business recorded an overall net loss of GH₵137,566.
2. The profit margin was negative at approximately 43.16%.
3. Actual expenses were GH₵16,006 below the expense budget.
4. Sales recorded the highest departmental expenditure and budget utilisation.
5. Budget compliance did not translate into overall profitability, indicating that revenue performance requires further investigation.

## Reconciliation

The financial totals and departmental budget calculations were cross-checked against the Day 5 SQL analysis.

Power BI results were consistent with the previously calculated SQL figures.

## Project Structure

```text
day6_powerbi_analysis/
├── README.md
├── day6_financial_analysis.pbix
└── screenshots/
    ├── day6_financial_kpis.png
    ├── day6_department_budget.png
    └── day6_data_model.png
```

## How to Reproduce

1. Open `day6_financial_analysis.pbix` in Power BI Desktop.
2. If the source CSV cannot be found, open **Transform data → Data source settings** and update the source path to your local copy of the accounting dataset.
3. Select **Close & Apply**, then refresh the model.
4. Review the seven DAX measures and the departmental budget analysis.
5. Compare the results with the financial figures documented above.

## Conclusion

This project demonstrates practical Power BI skills in data preparation, financial data modelling, DAX measure development, budget analysis, and reconciliation with SQL. It provides a foundation for the interactive financial dashboard to be developed on Day 7.
