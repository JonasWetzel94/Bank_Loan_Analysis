# Bank Loan Analysis - Power BI Project

🏦 **Comprehensive Bank Loan Portfolio Analysis**: This project is focused on analyzing the performance and health of a bank's loan portfolio. By using Power BI's advanced capabilities, we track loan applications, funding amounts, repayments, and loan quality across multiple dimensions such as regions, loan purpose, and borrower profiles.

🔍 **Explore the dynamic dashboard with advanced DAX functions, Power Query transformations, and custom measures to gain valuable insights into the bank's loan operations.**

# Background

The Bank Loan Analysis project was developed to provide the bank with a deeper understanding of its loan portfolio, focusing on critical metrics like loan quality (good vs. bad loans), borrower risk profiles, repayment performance, and loan distribution by regions and demographics. This analysis helps the bank make data-driven decisions regarding its lending strategies and risk management.

### Key Questions Addressed:
1. **What is the distribution of loan applications across regions, loan terms, and borrower types?**
2. **How does loan performance (good vs bad loans) vary by region and purpose?**
3. **What are the trends in loan disbursements and repayments over time?**
4. **Which borrowers are most likely to default based on their debt-to-income ratios and other risk factors?**
5. **How does the bank's lending portfolio compare month-over-month in terms of funded amounts and repayments?**

# Tools I Used

For this analysis, the following tools were utilized:
- **Power BI:** The primary platform for building interactive and dynamic dashboards.
- **DAX (Data Analysis Expressions):** Advanced DAX was employed for complex calculations like risk scoring, good vs bad loan segmentation, and cohort analysis.
- **M Code (Power Query):** Used to clean, transform, and model data before importing it into Power BI for further analysis.
- **Conditional Formatting:** Applied to visually emphasize key metrics such as default rates and risk scores, allowing for quick identification of high-risk areas.

# The Analysis

### 1. Loan Performance KPIs

We tracked the overall loan performance with key KPIs:
- **Good Loan vs. Bad Loan Performance:** This includes measures such as the percentage of good vs. bad loans, total funded amounts for each category, and repayment metrics.
- **Average Debt-to-Income Ratio (DTI):** Helps assess borrower risk.
- **Average Interest Rate:** To understand the cost of borrowing across the loan portfolio.

**Advanced DAX Example**:
```dax
Good Loan Percentage = 
DIVIDE(
    [Total Good Loans], 
    [Total Loan Applications], 
    0
)
```

This advanced DAX measure calculates the percentage of good loans relative to the total number of loan applications.

### 2. Regional Analysis with Filled Maps

Using **Filled Maps**, we analyzed regional disparities in loan performance, funding amounts, and application rates.
- **Loan Applications by State:** Visualized using a filled map, providing a geographical breakdown of where loan applications are most frequent.
- **Regional Loan Performance:** Highlighting regions with higher rates of bad loans using conditional formatting.

**DAX for Loan Default Rate by Region**:
```dax
Loan Default Rate = 
DIVIDE(
    [Total Bad Loans], 
    [Total Loans in Region], 
    0
)
```

This DAX measure calculates the default rate for loans by dividing the number of bad loans by the total number of loans in each region.

### 3. Time Intelligence for Loan Metrics

By leveraging Power BI's **Time Intelligence** functions, we created dynamic year-over-year and month-over-month trends for key loan metrics:
- **Monthly Loan Applications & Funded Amounts:** Line charts displaying month-over-month (MoM) and year-over-year (YoY) changes in loan applications, funded amounts, and total repayments.
- **Loan Interest Trends:** By applying advanced DAX, we tracked changes in average interest rates and interest income over time.

**Advanced Time Intelligence DAX for MTD Funded Amounts**:
```dax
MTD Funded Amount = 
CALCULATE(
    [Total Funded Amount], 
    DATESMTD('Date'[Date])
)
```

This DAX measure calculates the Month-to-Date (MTD) funded amount, helping the bank track short-term trends.

### 4. Cohort Analysis

A more advanced technique, **Cohort Analysis**, was used to analyze borrower behavior and loan performance over time. This helps identify the groups of borrowers that are most likely to default based on when they took out their loans and their repayment performance.

**DAX for Cohort Grouping**:
```dax
CohortGroup = 
CALCULATE(
    COUNTROWS('LoanData'),
    FILTER(
        'LoanData', 
        YEAR('LoanData'[LoanIssueDate]) = YEAR(TODAY()) - 1
    )
)
```

This measure calculates the number of borrowers who took out loans last year to identify trends in loan defaults or repayment patterns.

### 5. Loan Purpose and Borrower Profile Analysis

A **Loan Purpose Breakdown** was created to visualize the distribution of loans by the reason they were taken out (e.g., home improvement, education, medical expenses). We also analyzed borrower profiles based on their debt-to-income ratio, home ownership status, and employment length.

**DAX for Debt-to-Income Ratio**:
```dax
Avg DTI = 
AVERAGEX(
    LoanData,
    LoanData[Debt] / LoanData[Income]
)
```

This advanced DAX function calculates the average Debt-to-Income ratio, a key indicator of borrower risk.

# M Code for Data Transformation

In Power Query, **M Code** was used to clean and structure the data efficiently. Here are two examples:

- **Replacing Nulls in Loan Amounts**:
```m
= Table.ReplaceValue(#"PreviousStep", null, 0, Replacer.ReplaceValue, {"LoanAmount"})
```

This M code replaces all null values in the loan amount column with 0, ensuring data consistency for further calculations.

- **Appending Data from Multiple Sources**:
```m
= Table.Combine({LoanData2021, LoanData2022})
```

Multiple loan datasets were appended together to create a unified table for analysis.

# Conditional Formatting

Conditional formatting was applied to the **Bad Loan** percentage metric, allowing the bank to quickly see regions or loan types that are underperforming:
- **Red** for bad loan percentages above 30%.
- **Yellow** for bad loan percentages between 15% and 30%.
- **Green** for bad loan percentages below 15%.

```Power BI
In the "Format" pane, select Conditional Formatting -> Based on the field value for Bad Loan %.
```

# Advanced Power BI Techniques

1. **What-If Analysis with Parameters**: A **What-If Analysis** was implemented using parameters to simulate how changes in loan approval rates, interest rates, or DTI could affect the overall loan performance.

```Power BI
Modeling -> New Parameter -> Define Min, Max, and Increment -> Create What-If Parameter
```

This allows users to simulate various scenarios in real-time, giving the bank insights into potential outcomes of different loan strategies.

2. **Drillthrough and Report Page Tooltips**: **Drillthrough** functionality was enabled to allow users to click on summary metrics (e.g., Total Funded Amount) and drill through to a detailed page showing granular data for that metric. **Report Page Tooltips** were used to display additional data when hovering over visuals.

```Power BI
Right-click on a visual -> Enable Drillthrough -> Set up a detailed page for drillthrough.
```

# What I Learned

🧩 **Cohort Analysis and Advanced DAX:** Mastered the use of cohort analysis and complex DAX measures to uncover deep insights into borrower behavior and loan performance over time.

📊 **Time Intelligence and Dynamic Metrics:** Leveraged Power BI’s time intelligence functions to dynamically track changes in key loan metrics month-to-month and year-to-year.

💡 **Risk and Performance Insights:** Developed advanced methods to assess borrower risk and identify areas for improvement in loan portfolio performance, helping the bank mitigate default risks and improve its lending strategies.

# Conclusions

### Key Insights:
1. **Loan Risk Assessment:** Advanced DAX metrics helped identify high-risk borrowers based on debt-to-income ratio and historical default rates, providing critical information for risk management.
2. **Regional Disparities:** Regional analysis revealed significant disparities in loan performance, particularly in areas with high concentrations of bad loans.
3. **Loan Performance Trends:** By leveraging time intelligence, the bank can now track loan performance and borrower repayment patterns more effectively, allowing for real-time decision-making.
4. **What-If Scenarios:** The What-If analysis enabled the bank to simulate different loan strategies, providing insights into how changes in loan approvals or interest rates could impact profitability.
5. **Cohort and Purpose Analysis:** Deep insights into borrower cohorts and loan purposes allow the bank to tailor its lending strategies to different borrower profiles and loan use cases.
