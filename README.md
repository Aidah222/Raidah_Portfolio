# HR Analytics Dashboard
## Table of Contents

- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tool](#tool)
- [Data Preparation or Data Cleaning](#data-preparation-or-data-cleaning)
- [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)
- [Data Analysis](#data-analysis)
- [Results](#results)
- [Recommendation](#recommendations)
- [Limitations](#limitations)
  
### Project Overview
---
This data analysis project aims to create a  comprehensive HR Analytics Dashboard for analyzing key HR metrics such as employee headcount, attrition rates, and performance trends.By combining and displaying these essential metrics, the dashboard will provide valuable insights for HR professionals, helping them make informed decisions related to workforce management, employee retention, and overall performance optimization.

### Data Sources

HRDataset_v14 : A publicly available HR datasets from Kaggle. [Link HERE](https://www.kaggle.com/datasets/rhuebner/human-resources-data-set/data?select=HRDataset_v14.csv)

### Tool

- Power Bi - Used to build an interactive dashboard and detailed report.

###  Data Preparation or Data Cleaning

During data preparation phase, I performed the following tasks:
1. Data loading and Transform Data in Power Query Editor

- After Imported Data into Power BI, convert first row into column headers.

- Convert Data Types into whole numbers, decimals, currency and date.

2. Duplicates check
- To make sure there were no duplicate entries in the dataset, I checked the "EmpID" column directly in Power BI’s Data View. First,clicked Data View. Next, I created a new column using a DAX formula to check for duplicates. The formula I used looks for any "EmpID" that appears more than once and labels it as either "Duplicate" or "Unique". After the column was created, I could easily filter the data to see if there were any duplicates. Fortunately, no duplicates were found, which means all "EmpIDs" in the dataset are unique. 

- DAX formula i used :

```Power BI
Is Duplicate = IF(CALCULATE(COUNTROWS('HRDataset_v14'), 'HRDataset_v14'[EmpID] = EARLIER('HRDataset_v14'[EmpID])) > 1, "Duplicate",  "Unique")  
```

- Duplicates Check: Conducted a check for duplicate entries based on the EmpID column. Result: No duplicates were found in the dataset.

### Exploratory Data Analysis (EDA)

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

6. Develop an Age Bucket column in the HRDataset_v14 table to classify employees into age categories, helping HR analyze age-based trends in the workforce:

 ```Power BI
Age Bucket = SWITCH(TRUE(),
HRDataset_v14[Age]>=18 && HRDataset_v14[Age]<= 25,"18-25",
HRDataset_v14[Age]>=26 && HRDataset_v14[Age]<= 35,"26-35",
HRDataset_v14[Age]>=36 && HRDataset_v14[Age]<= 45,"36-45",
HRDataset_v14[Age]>=46 && HRDataset_v14[Age]<= 55,"46-55",
HRDataset_v14[Age]>=56, "55+")
```

7. Calculate "Cumulative Headcount" column in Measure table:

```Power BI
Cummulative Headcount =
var last_date = LASTDATE(HRDataset_v14[DateofHire])
return
CALCULATE([Headcount], ALL(HRDataset_v14[DateofHire]), HRDataset_v14[DateofHire]<= last_date)
```

8. Calculate new measure in Measure table and name it as "Salary":
```Power BI
Salary = SUM(HRDataset_v14[Salary])
```

### Results

The HR Analytics Dashboard has been successfully developed and deployed, providing valuable insights into key HR metrics, including employee headcount, attrition, attrition rates(%), salary averages, and Average age. Other than that, the dashboard has five slicers (Department, Employment Status, State, Gender, and Position), which allow users to dig into the data that matters to them and narrow down the information to specific groups. Below are the key findings from the analysis:

Some of the key business questions we aimed to answer include:

1. What is the total number of employees?
   
- The current total headcount is 311 employees across all departments and states

2. What is the number of employees who have left the organization (Attrition)?
   
- The total number of employees who have left the organization (Attrition) is 104. The department with high Attrition is the production department with 83 employees.

3. What is the Attrition rate (Attrition%)?
   
- The Attrition Rate is 33.44%, indicating the percentage of employees who left the company relative to the total headcount.

4. What is the Average Salary within a company?
   
- The Average Salary within a company is 69.02K

5. What is the Average Age of employees?
    
- The Average Age of employees is 46.41 years

6. Headcount by Department
   
- The Production Department has the highest headcount, with 209 employees.

- The Admin Offices and Executive Office departments have the least headcount, with only 9 and 1 employee respectively, suggesting they may need additional staff to meet operational demands.

7. Headcount by Age Bucket

- The age group 36-45 has the highest headcount, with 153 employees, representing 49.2% of the total workforce.

- The age group 26-35 has the lowest headcount, with only 11 employees, making up 3.54% of the total workforce.

8. Headcount by Marital Status and Gender

- There are a total of 176 female employees and 135 male employees.

- For marital status:

  a. Single: 62 males and 75 females

  b. Married: 52 males and 72 females

  c. Divorced: 14 males and 16 females

  d. Separated: 3 males and 9 females

  e. Widowed: 4 males and 4 females

9. Cumulative Headcount and Headcount by Year

- From 2011 to 2015, the Cumulative Headcount grew steadily, showing consistent hiring and a healthy recruitment trend. The Headcount by Year indicates regular employee inflows, reflecting ongoing recruitment efforts.

- From 2015 to 2018, the Cumulative Headcount remained mostly flat, with occasional small increases. During this period, the company hired only 1 to 2 employees per year, resulting in minimal growth in overall headcount.

10. Attrition by Year

- The Attrition by Year chart shows a fluctuating pattern of employee turnover over the years, with certain years experiencing higher attrition than others.

- The highest attrition occurred in 2011, with 11 employees leaving the company that year. This represents a sharp spike in turnover, significantly higher than the other years, suggesting that 2011 was a year of heightened employee departures.

11. Headcount by Recruitment Source
    
- The Headcount by Recruitment Source chart shows the distribution of employees across various recruitment channels. The highest bar is for Indeed, with 87 headcount, followed by LinkedIn with 76 headcount. Other notable channels include Google Search, Employee Referrals, and Diversity Job Fair, with moderate contributions. CareerBuilder, the Company Website, and the Other category also played a role, though with smaller numbers of hires. Finally, the Online Web Application channel had the least impact, contributing only 1 headcount.

### Recommendations

Based on the analysis, I recommend the following actions:

1. Given that the Admin Offices and Executive Office departments have notably low headcount, HR should consider evaluating the staffing needs and possibly hiring additional employees in these departments. 

2. HR should focus on improving recruitment strategies like targeting job postings to attract younger age groups (26-35), as this demographic currently represents the smallest segment of the workforce. 

3. HR should take a closer look at why so many employees are leaving, especially in the Production department. They can start by reviewing exit interview feedback and checking salary trends. By understanding these issues, HR can work on improving retention and making sure employees feel more satisfied and valued.

4. Focus on strengthening job boards or explore new recruitment avenues like university recruitment programs to diversify the talent pool, while continuing to use platforms like Indeed and linkedin.

### Limitations

1. The dataset has limited historical data, only covering the period from September 2006 to September 2018. This may not fully capture longer-term trends in employee behavior, attrition, or recruitment patterns.

2. Although the HR Analytics Dashboard includes slicers to filter data, it may still feel too basic for some users. They might require more advanced filtering options or the ability to explore data in greater depth—such as examining specific metrics or comparing multiple factors simultaneously.

