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

### Visualization Plan

Below are the key visualizations that we will generate for the HR Analytics Dashboard:

- Headcount by Department
- Headcount by Age Bucket
- Headcount by Marital Status and Gender
- Cumulative Headcount and Headcount by Date of Hire
- Attrition by Date of Hire
- Headcount by Recruitment Source

### Data Analysis

Analyzing the HR data some KPIs i want to find out, then create separate table (name as "Measure" table) and include all the measures:

1. To track the total number of employees,
- Count the employee ID (click new measure) and name it as “Headcount”:
  
```Power BI
Headcount = COUNT(HRDataset_v14[EmpID])
```

2. Calculate the number of employees who have left the organization (Attrition),
- Firstly, we will created a calculated column in the HRDataset_v14 table to identify if an employee is "Active" or has "Left" (Attrition). We will using the following formula:

```Power BI
Attrition = IF(HRDataset_v14[EmploymentStatus]="Active",1,0)
```
- This formula assigns value "1" to employees who are still active and "0" to those who have left the organization.
  
- Next, we will calculate Attrition in Measure table:

```Power BI
Attrition = var a
          = CALCULATE(COUNT(HRDataset_v14[EmpID]), FILTER(HRDataset_v14,HRDataset_v14[Attrition]=0))
return a
```

- This formula counts the number of employees with Attrition = 0 in the HRDataset_v14 table, which represents employees who have left the organization.


3. Determine the Attrition Rate (Attrition %),
- Now, calculate the percentage of employees who have left in relation to the total number of employees (Headcount):
  
```Power BI
Attrition % = ([Attrition]/[Headcount])
```

4. Compute the Average Salary,
- To understand the compensation trends within the company, we calculate the average salary of employees in the organization:

```Power BI
Avg Salary = var a
           = CALCULATED(AVERAGE(HRDataset_v14[Salary]))
return a
```

5. Calculate Employee Age, 
- Create new column and name it as "Age" in the HRDataset_v14 table to determine the age of each employee based on their date of birth (DOB) and current date:
  
```Power BI
Age = DATEDIFF(HRDataset_v14[DOB], TODAY(),YEAR)
```

, then we calculate the Average Age of employees in Measure table:

```Power BI
Avg Age = AVERAGE(HRDataset_v14[Age])
```




### Results/Outcome

The analysis results are summarized as follows:
1. ss
2. ss
3. ss
4. ss
5. s

### Recommendations

Based on the analysis, I recommend the following actions:
-dd
-dd

### Limitations

I had to remove all zero values from budget and revenue columns because they would ha

### Referen-------
