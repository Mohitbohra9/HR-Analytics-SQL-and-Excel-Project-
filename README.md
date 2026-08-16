📊 HR Analytics — Employee Attrition Analysis using SQL & Excel






📌 Project Overview

This project analyzes employee data to understand workforce size, employee attrition, compensation, job satisfaction, overtime, tenure, performance, promotion history, and departmental trends.

The project combines SQL for data analysis and Microsoft Excel for reporting and dashboard development.

The objective is to convert raw employee records into actionable HR insights that can support:

Employee retention

Workforce planning

Compensation analysis

Department-level decision making

Employee engagement

HR performance monitoring

🎯 Business Problem

Employee attrition can increase recruitment costs, reduce productivity, and create workforce planning challenges.

This project investigates the factors associated with employee turnover and answers 13 business-focused HR questions using SQL.

The analysis is later extended into Excel for visualization and dashboard reporting.

🛠️ Tools & Technologies

Tool

Purpose

SQL Server / SSMS

Data analysis, KPI calculation and business queries

Microsoft Excel

Data cleaning, Pivot Tables, charts and dashboard

GitHub

Project documentation and portfolio

CSV / Excel Dataset

Employee data source

📂 Dataset

The project uses an employee-level dataset containing fields related to:

Employee demographics

Department

Job role

Attrition

Overtime

Job satisfaction

Years at company

Monthly salary

Performance rating

Promotion history

Important fields used in SQL

Department
Job_Role
Attrition
Overtime
Job_Satisfaction
Years_At_Company
Monthly_Salary
Performance_Rating
Promotion_Last_5Yrs

📊 Initial Business KPIs

Based on the SQL analysis completed so far:

KPI

Result

👥 Total Employees

30,000

🚪 Employees Left

5,512

📈 Overall Attrition Rate

18.37%

👤 Employees Retained

24,488

Initial Finding

The dataset contains 30,000 employees, of whom 5,512 have left, resulting in an overall attrition rate of 18.37%.

This company-level attrition rate is used as a benchmark for department-level analysis.

🗄️ SQL Analysis

Q1. What is the total number of employees?

SELECT COUNT(*) AS Total_Employees
FROM employees;

<img width="198" height="110" alt="image" src="https://github.com/user-attachments/assets/2e9c5139-2bcc-4cf2-b716-de7e87f6f69f" />

Q2. How many employees have left the company, and what is the attrition rate?

SELECT
    COUNT(*) AS Total_Employees,
    SUM(CASE WHEN Attrition = 1 THEN 1 ELSE 0 END) AS Employees_Left,
    ROUND(
        100.0 * SUM(CASE WHEN Attrition = 1 THEN 1 ELSE 0 END)
        / COUNT(*), 2
    ) AS Attrition_Rate
FROM employees;

<img width="397" height="93" alt="image" src="https://github.com/user-attachments/assets/d0d52a61-f5b1-405a-87e5-85a078852e84" />


Q3. Which department has the highest attrition rate?

SELECT
    Department,
    COUNT(*) AS Total_Employees,
    SUM(CASE WHEN Attrition = 1 THEN 1 ELSE 0 END) AS Employees_Left,
    ROUND(
        100.0 * SUM(CASE WHEN Attrition = 1 THEN 1 ELSE 0 END)
        / COUNT(*), 2
    ) AS Attrition_Rate
FROM employees
GROUP BY Department
ORDER BY Attrition_Rate DESC;

<img width="612" height="225" alt="image" src="https://github.com/user-attachments/assets/0ba48bb5-2d00-4ba4-9527-37614e7a2309" />


Q4. Which job roles have the highest attrition?

SQL Logic

SELECT
    Job_Role,
    COUNT(*) AS Total_Employees,
    SUM(CASE WHEN Attrition = 1 THEN 1 ELSE 0 END) AS Employees_Left,
    ROUND(
        100.0 * SUM(CASE WHEN Attrition = 1 THEN 1 ELSE 0 END)
        / COUNT(*), 2
    ) AS Attrition_Rate
FROM employees
GROUP BY Job_Role
ORDER BY Attrition_Rate DESC;

<img width="676" height="713" alt="image" src="https://github.com/user-attachments/assets/b9b6f1a3-e6d0-46db-b537-04131cd41f8c" />

Q5. Does overtime affect employee attrition?

SQL Logic

SELECT
    Overtime,
    COUNT(*) AS Total_Employees,
    SUM(CASE WHEN Attrition = 1 THEN 1 ELSE 0 END) AS Employees_Left,
    ROUND(
        100.0 * SUM(CASE WHEN Attrition = 1 THEN 1 ELSE 0 END)
        / COUNT(*), 2
    ) AS Attrition_Rate
FROM employees
GROUP BY Overtime
ORDER BY Attrition_Rate DESC;

<img width="508" height="109" alt="image" src="https://github.com/user-attachments/assets/af2b8480-1b0d-4d56-9e9a-ade8d699b155" />


Q6. Does job satisfaction affect attrition?

SQL Logic

SELECT
    Job_Satisfaction,
    COUNT(*) AS Total_Employees,
    SUM(CASE WHEN Attrition = 1 THEN 1 ELSE 0 END) AS Employees_Left,
    ROUND(
        100.0 * SUM(CASE WHEN Attrition = 1 THEN 1 ELSE 0 END)
        / COUNT(*), 2
    ) AS Attrition_Rate
FROM employees
GROUP BY Job_Satisfaction
ORDER BY Job_Satisfaction;

<img width="528" height="158" alt="image" src="https://github.com/user-attachments/assets/f40ec4dc-81f3-4c9c-97c5-882e867a650f" />


Q7. Does employee tenure affect attrition?

SELECT
    CASE
        WHEN Years_At_Company <= 2 THEN '0-2 Years'
        WHEN Years_At_Company <= 5 THEN '3-5 Years'
        WHEN Years_At_Company <= 10 THEN '6-10 Years'
        ELSE '10+ Years'
    END AS Tenure_Group,

    COUNT(*) AS Total_Employees,

    SUM(CASE WHEN Attrition = 1 THEN 1 ELSE 0 END) AS Employees_Left,

    ROUND(
        100.0 * SUM(CASE WHEN Attrition = 1 THEN 1 ELSE 0 END)
        / COUNT(*), 2
    ) AS Attrition_Rate

FROM employees

GROUP BY
    CASE
        WHEN Years_At_Company <= 2 THEN '0-2 Years'
        WHEN Years_At_Company <= 5 THEN '3-5 Years'
        WHEN Years_At_Company <= 10 THEN '6-10 Years'
        ELSE '10+ Years'
    END

ORDER BY Attrition_Rate DESC;

<img width="596" height="186" alt="image" src="https://github.com/user-attachments/assets/4e705cf3-63c6-4c84-8433-90f5589dacd0" />


Q8. Is salary associated with employee attrition?

SQL Logic

SELECT
    Attrition,
    COUNT(*) AS Total_Employees,
    ROUND(AVG(Monthly_Salary), 2) AS Average_Salary,
    MIN(Monthly_Salary) AS Minimum_Salary,
    MAX(Monthly_Salary) AS Maximum_Salary
FROM employees
GROUP BY Attrition;

<img width="552" height="109" alt="image" src="https://github.com/user-attachments/assets/87a0ddfa-9e9f-4053-9835-4f3b6f7cb117" />


Q9. Which salary band has the highest attrition?

Salary Bands

Salary

Band

< 30,000

Low

30,000–59,999

Medium

≥ 60,000

High

SQL Logic

SELECT
    CASE
        WHEN Monthly_Salary < 30000 THEN 'Low'
        WHEN Monthly_Salary < 60000 THEN 'Medium'
        ELSE 'High'
    END AS Salary_Band,

    COUNT(*) AS Total_Employees,

    SUM(CASE WHEN Attrition = 1 THEN 1 ELSE 0 END) AS Employees_Left,

    ROUND(
        100.0 * SUM(CASE WHEN Attrition = 1 THEN 1 ELSE 0 END)
        / COUNT(*), 2
    ) AS Attrition_Rate

FROM employees

GROUP BY
    CASE
        WHEN Monthly_Salary < 30000 THEN 'Low'
        WHEN Monthly_Salary < 60000 THEN 'Medium'
        ELSE 'High'
    END

ORDER BY Attrition_Rate DESC;

<img width="515" height="151" alt="image" src="https://github.com/user-attachments/assets/75757df7-6d90-4c39-af15-eab84d16683b" />


Q10. Does performance rating affect attrition?

SQL Logic

SELECT
    Performance_Rating,
    COUNT(*) AS Total_Employees,

    SUM(CASE WHEN Attrition = 1 THEN 1 ELSE 0 END) AS Employees_Left,

    ROUND(
        100.0 * SUM(CASE WHEN Attrition = 1 THEN 1 ELSE 0 END)
        / COUNT(*), 2
    ) AS Attrition_Rate,

    ROUND(AVG(Monthly_Salary), 2) AS Average_Salary

FROM employees

GROUP BY Performance_Rating
ORDER BY Performance_Rating;

<img width="696" height="169" alt="image" src="https://github.com/user-attachments/assets/53278431-2aa1-4c76-a73c-59bc46b1f974" />


Q11. Does promotion history affect employee attrition?

<img width="559" height="110" alt="image" src="https://github.com/user-attachments/assets/049a8fc2-7957-4a06-a815-94f957916eb9" />

SELECT
    Promotion_Last_5Yrs,
    COUNT(*) AS Total_Employees,

    SUM(CASE WHEN Attrition = 1 THEN 1 ELSE 0 END) AS Employees_Left,

    ROUND(
        100.0 * SUM(CASE WHEN Attrition = 1 THEN 1 ELSE 0 END)
        / COUNT(*), 2
    ) AS Attrition_Rate

FROM employees

GROUP BY Promotion_Last_5Yrs
ORDER BY Attrition_Rate DESC;


Q12. Which departments have the highest average salary?

SELECT
    Department,
    COUNT(*) AS Total_Employees,
    ROUND(AVG(Monthly_Salary), 2) AS Average_Salary,
    MAX(Monthly_Salary) AS Highest_Salary,
    MIN(Monthly_Salary) AS Lowest_Salary
FROM employees
GROUP BY Department
ORDER BY Average_Salary DESC;
<img width="673" height="268" alt="image" src="https://github.com/user-attachments/assets/3704dc9e-c918-4653-a4f2-4cec4dd31e7b" />




📗 Excel Analysis

The same employee dataset will be analyzed in Excel after the SQL analysis.

Excel Workflow

Raw Dataset
     ↓
Data Cleaning
     ↓
Remove Duplicates
     ↓
Check Missing Values
     ↓
Calculated Columns
     ↓
Pivot Tables
     ↓
Charts
     ↓
Interactive HR Dashboard

Excel Dashboard KPIs

The final dashboard will include:

Total Employees

Employees Left

Employees Retained

Attrition Rate

Average Salary

Average Age

Average Tenure

Planned Excel Charts

Attrition by Department

Attrition by Job Role

Attrition by Overtime

Attrition by Job Satisfaction

Attrition by Tenure Group

Attrition by Salary Band

Attrition by Performance Rating

Attrition by Promotion History

Average Salary by Department

📊 Final Dashboard

<img width="1878" height="675" alt="image" src="https://github.com/user-attachments/assets/1274ada7-d315-4ca5-9eb7-ef3ab1f7a75a" />


The Excel dashboard will provide HR stakeholders with a single-page view of:

Workforce → Attrition → Compensation → Performance → Satisfaction → Career Growth

The dashboard will help identify employee groups and departments that may require additional retention attention.

💼 Business Recommendations

Recommendations will be finalized after completing the SQL and Excel analysis.

Potential areas of focus include:

Investigate departments with attrition above the company average.

Review job roles with unusually high turnover.

Analyze overtime patterns to identify potential workload issues.

Examine salary bands with higher attrition.

Investigate low job-satisfaction groups.

Review early-tenure employee retention.

Evaluate whether promotion opportunities are associated with better retention.

Monitor high-performing employees for unexpected turnover.

Compare compensation differences across departments.

Develop targeted retention strategies based on the highest-risk employee segments.

📁 GitHub Repository Structure

HR-Analytics-SQL-Excel/
│
├── Dataset/
│   └── HR_Employee_Data.csv
│
├── SQL/
│   └── HR_Analytics.sql
│
├── Images/
│   ├── Q1_Total_Employees_Query.png
│   ├── Q1_Total_Employees_Output.png
│   ├── Q2_Attrition_Query.png
│   ├── Q2_Attrition_Output.png
│   ├── Q3_Department_Attrition_Query.png
│   ├── Q3_Department_Attrition_Output.png
│   └── ...
│
├── Excel/
│   └── HR_Analytics.xlsx
│
├── Dashboard/
│   └── HR_Analytics_Dashboard.pdf
│
└── README.md

🧠 SQL Skills Demonstrated

SQL Server

Data Exploration

Aggregate Functions

COUNT()

SUM()

AVG()

MIN()

MAX()

CASE WHEN

GROUP BY

ORDER BY

Conditional Aggregation

Percentage Calculations

CTEs

CROSS JOIN

Business KPI Development

📊 Excel Skills Demonstrated

Data Cleaning

Data Validation

Pivot Tables

Pivot Charts

Calculated Columns

Conditional Formatting

KPI Cards

Dashboard Design

HR Reporting

Business Insights

🚀 Project Outcome

This project demonstrates an end-to-end data analytics workflow:

Raw Employee Data
        ↓
SQL Data Analysis
        ↓
HR KPI Calculation
        ↓
Business Questions
        ↓
Excel Analysis
        ↓
Dashboard
        ↓
Business Recommendations

The project demonstrates the ability to use SQL and Excel together to solve practical HR analytics problems and communicate data-driven insights to business stakeholders.

👤 Author

Mohit Bohra

Aspiring Data Analyst | SQL | Excel | Power BI | Python
