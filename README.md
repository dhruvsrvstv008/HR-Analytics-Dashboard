# HR-Analytics-Dashboard

### Dashboard Link : https://public.tableau.com/app/profile/dhruv.srivastava6179/viz/shared/K4YFHNBX7

## Problem Statement

This dashboard helps the HR department understand why people are leaving the organisation. Instead of looking at attrition as a single number, it breaks the same 1,470 employee records down across department, age group, gender, education field & job role, so that the HR team can see exactly which pockets of the workforce are losing people the fastest and plan their retention efforts accordingly.

It also captures how satisfied employees are in each job role, which helps connect the attrition numbers with a possible reason behind them.

Since 237 employees out of 1,470 have left, the overall attrition rate stands at 16.12 %, thus roughly one out of every six employees is walking out of the organisation & this needs to be addressed.

Also since 133 of those 237 exits (56.12 %) are coming from the R&D department alone, thus the retention strategy cannot be uniform across the company — R&D needs a focused intervention.




### Steps followed

- Step 1 : The raw HR data was first cleaned & transformed in Microsoft Excel. Column headers were standardised, blank & duplicate records were removed, and supporting columns like "CF_age band" (age band grouping) & "Employee Count" were prepared in the sheet itself so that they could be used directly for aggregation in Tableau.
- Step 2 : Load data into Tableau Desktop, the dataset was connected using the Microsoft Excel connector.
- Step 3 : In the Data Source tab, the field data types were verified — Age, Employee Count, Job Satisfaction & Employee Number were kept as numeric, while Attrition, Gender, Department, Education Field, Job Role & CF_age band were kept as dimensions.
- Step 4 : A calculated field was created to flag every employee who has left the organisation, so that attrition could be counted as a measure instead of being filtered manually every time.

for creating the calculated field following expression was written;

        attrition count =

        IF [Attrition] = "yes" THEN 1 ELSE 0 END

- Step 5 : A calculated field was created to find the attrition rate, i.e. what share of the total workforce has left.

Following expression was written for the same,

        attition rate =

        SUM([attrition count]) / SUM([Employee Count])

  This field was then formatted as a percentage from the Default Properties > Number Format option.

- Step 6 : A calculated field was created to find the number of employees who are still with the organisation.

Following expression was written for the same,

        active employes =

        SUM([Employee Count]) - SUM([attrition count])

- Step 7 : A parameter named "bin size" was created (range type, minimum 2, maximum 10, step 1) so that the user can control how wide each age bucket should be on the histogram.

- Step 8 : A bin was then created on the Age field & the "bin size" parameter was passed as the bin size, instead of typing a fixed number. This makes the age distribution chart adjustable directly from the dashboard.

        Age (bin) = [Age]   , with bin size driven by the [bin size] parameter

- Step 9 : A worksheet named "kpi" was created. Measure Names was placed on columns & the five KPIs — Employee Count, attrition count, attition rate, active employes & Avg. Age — were shown together as a single strip using text marks.
- Step 10 : A worksheet named "department by attrition" was created. Department was placed on colour, attrition count on angle, and the mark type was changed to Pie. Labels were set to show both the value & the percent of total.
- Step 11 : A worksheet named "No. of Employees by Age Group" was created. The "Age (bin)" field was placed on columns & Employee Count on rows to build a histogram of the workforce age distribution. The "bin size" parameter control was shown on this sheet so that the bucket width can be changed while reading the chart.
- Step 12 : A worksheet named "Job Satisfaction Rating" was created. Job Role was placed on rows & Job Satisfaction on columns, the mark type was changed to Square, and Employee Count was placed on both colour & label. Row & column grand totals were switched on from the Analysis menu, turning the sheet into a heatmap of satisfaction ratings per role.
- Step 13 : A worksheet named "Education Field Wise Attrition" was created. Education Field was placed on rows & attrition count on columns as a horizontal bar chart, with attrition count also placed on colour so that the heaviest education fields stand out.
- Step 14 : A worksheet named "attrition by gender" was created showing the split of the 237 exits between female & male employees.
- Step 15 : A worksheet named "attrition by gender by differnt age group" was created. CF_age band was placed on columns & attrition count on angle, Gender was placed on colour, and the mark type was changed to Pie. The inner circle was created using a dual axis so that each age band renders as a donut instead of a plain pie, and the labels were set to show both the count & the percent of total.
- Step 16 : All the worksheets were then assembled into a single dashboard named "HR Analytics" with a custom size of 1580 x 900. A background image was added from the Objects pane, and text objects were used for the dashboard title & the section headings.
- Step 17 : Filters were applied on Education & Job Role, and they were made to "Apply to all worksheets using this data source" so that a single selection updates every visual on the dashboard together.
- Step 18 : Dashboard actions were configured on Department, Gender, Education Field & Age (bin), so that clicking on any one chart cross filters the rest of the dashboard.
- Step 19 : The workbook was then published to Tableau Public.

# Dashboard Snapshot (Tableau Desktop)

![HR_Analytics_Dashboard]([<img width="1555" height="847" alt="Image" src="https://github.com/user-attachments/assets/3cd0e6a0-33cc-415f-8e9b-a9df9351bd91" />](https://private-user-images.githubusercontent.com/260243159/636589703-3cd0e6a0-33cc-415f-8e9b-a9df9351bd91.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3ODY4MzcyNzMsIm5iZiI6MTc4NjgzNjk3MywicGF0aCI6Ii8yNjAyNDMxNTkvNjM2NTg5NzAzLTNjZDBlNmEwLTMzY2MtNDE1Zi04ZTliLWE5ZGY5MzUxYmQ5MS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYwODE1JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MDgxNVQyMzM2MTNaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT01NmNhZjU5NGYwY2IxMmQ4OTliNmU2Y2RlNjlmODE3M2E4MTA2ODNlNWZlYmZhYzFkYmI5OGVjNDU3YjQyNmJjJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZyZXNwb25zZS1jb250ZW50LXR5cGU9aW1hZ2UlMkZwbmcifQ.Rfb-3XXh7ipahzrW9Scr6U9sXk4a38_QzhtHQq2f4O0))

# Insights

A single page dashboard was created in Tableau Desktop & it was then published to Tableau Public.

Following inferences can be drawn from the dashboard;

### [1] Overall Workforce

    a) Total Employee Count - 1470
    b) Attrition Count      - 237
    c) Attrition Rate       - 16.12 %
    d) Active Employees     - 1233
    e) Average Age          - 37 years

           thus, close to one sixth of the workforce has already exited the organisation.

### [2] Department Wise Attrition

    a) R&D   - 133 exits (56.12 %)
    b) Sales - 92 exits  (38.82 %)
    c) HR    - 12 exits  (5.06 %)

           thus, more than half of the total attrition is coming out of the R&D department alone,
           which makes it the single biggest area of concern.

### [3] Attrition by Gender

    a) Male   - 150 exits
    b) Female - 87 exits

           thus, male employees are leaving in noticeably higher numbers than female employees.

### [4] Attrition by Gender across Age Bands

    a) 25 - 34  - 112 female & 69 male exits (highest attrition band overall)
    b) 35 - 44  - 51 female & 37 male exits
    c) 45 - 54  - 25 female & 16 male exits
    d) Under 25 - 38 female & 20 male exits
    e) Over 55  - 11 female & 8 male exits

           thus, the 25-34 age band is where the organisation is losing the most people,
           which is typically the stage where employees are most open to switching jobs.

### [5] Education Field Wise Attrition

    a) Life Sciences     - 89
    b) Medical           - 63
    c) Marketing         - 35
    d) Technical Degree  - 32
    e) Other             - 11
    f) Human Resources   - 7

           thus, employees from a Life Sciences & Medical background account for the bulk of the exits,
           which lines up with R&D being the worst hit department.

### [6] Age Distribution

The workforce peaks sharply around the 30 to 36 age range, with the single largest bucket holding 155 employees. Very few employees are below 20 or above 58, thus the organisation is dominated by mid career professionals & the average age of 37 reflects that.

### [7] Job Satisfaction Rating

7.1) Ratings are recorded on a scale of 1 to 4 across all nine job roles.

7.2) Sales Executive (326 employees), Research Scientist (292) & Laboratory Technician (259) are the three largest roles by headcount.

7.3) Across the organisation, 459 employees rated their satisfaction as 4 & 442 rated it as 3, while 289 rated it as 1 and 280 rated it as 2.

           thus, roughly 61 % of the workforce sits in the higher satisfaction bands (3 & 4),
           but the remaining 39 % sitting at 1 or 2 represents a sizeable at-risk group
           that overlaps closely with the roles showing the highest attrition.

All the numbers mentioned above are for the complete dataset with no filter applied. These values will change as soon as a particular Education or Job Role is selected, or when any chart is clicked to cross filter the dashboard.

## Tools Used

- Microsoft Excel - data cleaning & transformation
- Tableau Desktop Public Edition - calculated fields, parameters, bins & dashboard design
- Tableau Public - publishing & sharing
