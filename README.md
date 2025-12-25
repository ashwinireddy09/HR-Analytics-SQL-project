# HR-Analytics-SQL-project
Analyzed employee data using SQL to identify attrition trends, department-wise turnover, salary patterns, and performance impact. Used joins, aggregations, and CTEs to generate insights that support HR retention and workforce planning decisions.


## Project Overview
This HR Analytics SQL project analyzes employee data to understand workforce trends and identify factors affecting employee attrition. The project uses structured SQL queries to explore employee demographics, job roles, salaries, and performance metrics to support data-driven HR decisions.

# Objectives
The main objectives are to analyze employee attrition, identify department-wise turnover, understand the impact of salary and performance on attrition, and generate meaningful HR insights that help improve employee retention and workforce planning.

Project Structure
The project is organized into database setup, data loading, data exploration, analysis queries, and reporting. SQL scripts are structured for easy understanding, starting from table creation to final insight generation.

# Database and Table Creation
A relational database was created using SQL, and employee-related tables were designed with appropriate data types. Data was cleaned and validated during insertion to ensure accuracy and consistency for analysis.

-- 1. Create Database
```sql
CREATE DATABASE hr_analytics;
USE hr_analytics;

-- 2. Create Employee Table
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    age INT CHECK (age > 18),
    gender VARCHAR(10),
    department VARCHAR(50),
    job_role VARCHAR(50),
    monthly_income DECIMAL(10,2) CHECK (monthly_income > 0),
    years_at_company INT CHECK (years_at_company >= 0),
    performance_rating INT CHECK (performance_rating BETWEEN 1 AND 5),
    attrition VARCHAR(5) CHECK (attrition IN ('Yes','No'))
);
```
-- 3. Insert Cleaned & Validated Data

INSERT INTO employees (
    employee_id, age, gender, department, job_role,
    monthly_income, years_at_company, performance_rating, attrition
)
VALUES
(101, 29, 'Male', 'Sales', 'Sales Executive', 45000, 3, 4, 'No'),
(102, 35, 'Female', 'HR', 'HR Manager', 60000, 7, 5, 'No'),
(103, 26, 'Male', 'IT', 'Developer', 38000, 1, 3, 'Yes');
```
-- 4. Remove Invalid Records (Data Cleaning)
DELETE FROM employees
WHERE monthly_income <= 0
   OR age < 18
   OR performance_rating NOT BETWEEN 1 AND 5;
```
-- 5. Verify Data
```sql
SELECT * FROM employees;

```
# Questionnaire 
1. What is the average attrition rate for each department
2. What is the average hourly rate of male Research Scientists?
3. How does attrition relate to monthly income?
4. What is the average total working years per department?
5. What does Work-Life Balance look like across Job Roles?
6. Is there a relationship between attrition and years since last promotion? i need queries these questions

   
# Answers
1. What is the average attrition rate for each department
```sql
SELECT 
    Department,
    ROUND(AVG(CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END) * 100, 2) AS Attrition_Rate_Percentage
FROM hr_employee
GROUP BY Department;
```
2. What is the average hourly rate of male Research Scientists?
```sql
SELECT 
    ROUND(AVG(HourlyRate), 2) AS Avg_Hourly_Rate
FROM hr_employee
WHERE Gender = 'Male'
  AND JobRole = 'Research Scientist';

```
3. How does attrition relate to monthly income?
```sql
SELECT 
    Attrition,
    ROUND(AVG(MonthlyIncome), 2) AS Avg_Monthly_Income
FROM hr_employee
GROUP BY Attrition;
```
4. What is the average total working years per department?
```sql
SELECT 
    Department,
    ROUND(AVG(TotalWorkingYears), 2) AS Avg_Total_Working_Years
FROM hr_employee
GROUP BY Department;
```
5. What does Work-Life Balance look like across Job Roles?
```sql
SELECT 
    JobRole,
    ROUND(AVG(WorkLifeBalance), 2) AS Avg_Work_Life_Balance
FROM hr_employee
GROUP BY JobRole
ORDER BY Avg_Work_Life_Balance DESC;
```
6. Is there a relationship between attrition and years since last promotion? i need queries these questions
```sql
SELECT 
    Attrition,
    ROUND(AVG(YearsSinceLastPromotion), 2) AS Avg_Years_Since_Last_Promotion
FROM hr_employee
GROUP BY Attrition;

```
# Findings / Reports
The analysis revealed higher attrition in specific departments and job roles, with noticeable trends related to salary levels, experience, and performance ratings. Summary reports were generated using aggregations and filters to highlight key HR metrics.

# Conclusion
This project demonstrates effective use of SQL for HR analytics and shows how data insights can support strategic HR decisions. The findings can help organizations reduce attrition and improve employee engagement through targeted interventions.


