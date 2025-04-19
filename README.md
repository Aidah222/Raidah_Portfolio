# HR Analytics Dashboard

### Project Overview

This data analysis project aims to create a  comprehensive HR Analytics Dashboard for analyzing key HR metrics such as employee headcount, attrition rates, and performance trends.By combining and displaying these essential metrics, the dashboard will provide valuable insights for HR professionals, helping them make informed decisions related to workforce management, employee retention, and overall performance optimization.

### Data Sources

HRDataset_v14 : A publicly available HR datasets from Kaggle. [Link HERE](https://www.kaggle.com/datasets/rhuebner/human-resources-data-set/data?select=HRDataset_v14.csv)

### Tool

- Power Bi - Used to build an interactive dashboard and detailed report.

###  Data Preparation/Data Cleaning

During data preparation phase, I performed the following tasks:
1. Data loading and Transform Data in Power Query Editor

- After Imported Data into Power BI, convert first row into column headers.

- Convert Data Types into whole numbers, decimals, currency and date.

2. Duplicates check
- To make sure there were no duplicate entries in the dataset, I checked the "EmpID" column directly in Power BI’s Data View. First,clicked Data View. Next, I created a new column using a DAX formula to check for duplicates. The formula I used looks for any "EmpID" that appears more than once and labels it as either "Duplicate" or "Unique". After the column was created, I could easily filter the data to see if there were any duplicates. Fortunately, no duplicates were found, which means all "EmpIDs" in the dataset are unique. 

- DAX formula i used :
    
Is Duplicate = IF(CALCULATE(COUNTROWS('HRDataset_v14'), 'HRDataset_v14'[EmpID] = EARLIER('HRDataset_v14'[EmpID])) > 1, "Duplicate",  "Unique")  

- Duplicates Check: Conducted a check for duplicate entries based on the EmpID column. Result: No duplicates were found in the dataset.

### Exploratory Data Analysis (EDA) :

In this section, we conduct an Exploratory Data Analysis (EDA) to address several key business questions that will help in building an HR Analytics Dashboard. These questions provide critical insights into the company's workforce and will guide HR decision-making.

Some of the key business questions we aimed to answer include:

- What is the total number of employees?
- What is the number of employees who have left the organization (Attrition)?
- What is the Attrition rate (Attrition%)?
- What is the Average Salary within a company?
- What is the Average Age of employees?


3. Analyzing the HR data some KPIs i want to find out, then create separate table and include all the measures:

- Count the employee ID (click new measure) and name it as “Headcount” , to track the total number of employees.

- Calculate the number of employees who have left the organization, Attrition in HRDataset_v14 table,
