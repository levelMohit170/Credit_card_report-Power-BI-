## README for Credit Card Transaction Analysis Dashboard

This repository provides the necessary files and instructions to create an interactive dashboard using Power BI for analyzing credit card transactions and customer data.

### Overview

The Power BI dashboard uses credit card transaction and customer data to offer insights into spending patterns, customer demographics, and transaction trends. It includes various visualizations and interactive features for effective data analysis.

### Features

- **Transaction Analysis**: Overview of total transactions, average transaction value, and transaction trends over time.
- **Customer Insights**: Demographic breakdown of customers, including age, gender, and location.
- **Spending Patterns**: Analysis of spending categories, top merchants, and transaction frequency.
- **Interactive Filters**: Dynamic filters for detailed data exploration.

### Files Included

- `transactions.csv`: Contains credit card transaction data.
- `customers.csv`: Contains customer demographic data.
- `Credit_Card_Dashboard.pbix`: Power BI file with the dashboard and data model.
- all uploaded the pdf version to have a quick look


### Power BI Setup

1. **Load Data**: Import `transactions.csv` and `customers.csv` into Power BI.
2. **Data Cleaning**: Ensure correct data types (e.g., dates, numeric values).
3. **Data Modeling**: Create relationships between the `transactions` and `customers` tables using `CustomerID`.
4. **Calculated Columns and Measures**:
    - **IncomeGroup**:
      ```DAX
      IncomeGroup = SWITCH(
          TRUE(),
          'public cust_detail'[income] < 35000, "Low",
          'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] < 70000, "Med",
          'public cust_detail'[income] >= 70000, "High",
          "unknown"
      )
      ```
    - **Current Week Revenue**:
      ```DAX
      Current_week_Revenue = CALCULATE(
          SUM('public cc_detail'[Revenue]),
          FILTER(
              ALL('public cc_detail'),
              'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])
          )
      )
      ```
    - **Previous Week Revenue**:
      ```DAX
      Previous_week_Revenue = CALCULATE(
          SUM('public cc_detail'[Revenue]),
          FILTER(
              ALL('public cc_detail'),
              'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2]) - 1
          )
      )
      ```
    - **AgeGroup**:
      ```DAX
      AgeGroup = SWITCH(
          TRUE(),
          'cust detail'[customer_age] < 30, "20-30",
          'cust detail'[customer_age] >= 30 && 'cust detail'[customer_age] < 40, "30-40",
          'cust detail'[customer_age] >= 40 && 'cust detail'[customer_age] < 50, "40-50",
          'cust detail'[customer_age] >= 50 && 'cust detail'[customer_age] < 60, "50-60",
          'cust detail'[customer_age] >= 60, "60",
          "unknown"
      )
      ```
5. **Visualizations**:
    - Bar charts for transaction counts and amounts.
    - Pie charts for customer demographics.
    - Line charts for transaction trends over time.
    - Tables for detailed transaction and customer information.
      
6. **Interactive Features**: Add slicers and filters for dynamic data exploration.



### Contributions

Contributions are welcome! If you have suggestions for improvements or new features, please create an issue or submit a pull request.


### Contact

For any questions or inquiries, please contact Mohit Kumar Gond at mohitgond170@gmail.com.

---

