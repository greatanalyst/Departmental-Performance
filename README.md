# Departmental Performance  : Building An Interactive Power BI Dashboard For Staff Attendance 
## Table Of Content
- [Description](#description)
- [Business Introduction](#business-introduction)
- [Business Problem](#business-problem)
- [Aim of the Project](#aim-of-the-project)
- [Solution](#solution)
- [Metrics Defined](#metrics-defined)
- [Features](#features)
- [Insights And Recommendations](#insights-and-recommendations)
- [Tech Stack](#tech-stack)


## Description 
The Project Review Overview Dashboard is a data visualization project built using Power BI and SQL  to analyze and monitor organizational project performance. It provides a comprehensive view of project budgets, costs, departmental contributions, and employee-level insights in a single interactive interface.

The dashboard enables users to track how financial resources are allocated across departments such as Sales, Marketing, Engineering, IT, and Human Resources, while also comparing project status (completed vs. upcoming). It integrates key business metrics like capital investment, salary costs, and project budgets to support effective decision-making.

With dynamic filtering options and detailed visualizations, the project helps stakeholders identify inefficiencies, monitor spending patterns, and optimize resource allocation. Ultimately, it serves as a decision-support tool for improving financial planning, enhancing operational performance, and ensuring better project management across the organization.

![WhatsApp Image 2026-04-02 at 1 43 58 PM](https://github.com/user-attachments/assets/a810c319-34a6-4c62-8197-e36c34017419)


## Business Introduction

This project focuses on analyzing organizational project performance across multiple departments. It provides a centralized view of project budgets, costs, employee contributions, and departmental efficiency. The dashboard is designed to support decision-makers in monitoring financial performance and optimizing resource allocation.

## Business Problem
- Management often struggles to see the "big picture" when individual employee data is siloed from project financial data. Specifically, the company needed to answer:
- Are departments staying within their allocated project budgets?
- How does salary cost compare to the actual capital generated or spent by each department?
- Lack of visibility into project spending across departments
- Difficulty tracking budget utilization and cost overruns
- Inefficient allocation of resources and capital
- Limited insight into employee-level contributions and performance
- Challenges in comparing project status (completed vs. ongoing)
- Which departments are currently over-utilizing resources on "upcoming" vs. "completed" projects?
  
## Aim of the Project

- Identify Departments and Projects in the Red: Understand which departments or projects are over budget or underperforming, so we can take corrective action.

- Data Organization: Ensure that data from various sources (e.g., employee information, salary data, department budgets, and project details) is structured correctly and accessible for reporting

- Power BI Dashboard Development: Collaborate with us to create a comprehensive dashboard that provides visibility into employee performance, salary distribution, and departmental project management.:


  
## Solution

This project followed a standard Data Analysis Expression (DAX) and ETL (Extract, Transform, Load) workflow.

Step 1: Data Cleaning Tool: Microsoft SQL
- Source Connection: Imported raw attendance data (CSV/Excel) containing daily status codes into SQL platform (project_id,project_name,project_budget,project_start_date,project_end_date,department_id
)(assignment_id	employee_id	project_id) etc..


- Joined Tables and Queried the data : 
The following Microsoft SQL queries  was used to query the data and formulate a table

` with project_status as (
select
project_id,
project_name,
project_budget,
'upcoming' as status
from [upcoming projects]
union all
select
project_id,
project_name,
project_budget,
'completed' as status
from completed_projects)`


`select
e.employee_id,
e.first_name,
e.last_name,
e.job_title,
e.salary,
d.Department_Name,
pa.project_id,
p.project_name,
p.status
from employees e
join departments d
on e.department_id = d.Department_ID
join project_assignments pa
on pa.employee_id = e.employee_id
join project_status p
on p.project_id = pa.project_id `

Step 2:Power BI 
- Calendar Table: Created a dedicated Date Table to allow for time-intelligence functions (filtering byEmploy_ID, Headshot, and Department).

- Relationships: Established a One-to-Many relationship between the Employee Master list and the Attendance Fact table.

Step 3: DAX Measure Development
- I authored several custom columsa and formulate a reference table to calculate the KPIs seen on the dashboard:
 <img width="1002" height="777" alt="image" src="https://github.com/user-attachments/assets/642fd282-e3b3-44bc-8db2-e883464cc3ae" />
 <img width="1910" height="768" alt="image" src="https://github.com/user-attachments/assets/e63bfab4-6b60-4d9c-8cb5-0731239843c5" />

##  Metrics Defined 

- Total Capital Invested: $1.29M
- Total Project Budget: $60K
- Project Cost: Cost incurred per department/project
- Salary Cost: Employee-related expenses
- Departmental Contribution (%): Share of total cost by department
- Project Status Distribution: Completed vs. Upcoming projects
- Budget Allocation: Budget assigned per project and department
  
## Features

- Employee Profile Card: Displays headshot, job title, and salary for quick HR reference.

- Donut Chart Visualization: Highlights the "Project Cost by Department," showing that Sales (26.32%) and Marketing (20.18%) are the primary cost drivers.

- Departmental Goal Tracker: A tabular view linking high-level strategy (e.g., "Develop new products") directly to financial performance.

- Ranking Bars: Horizontal bar charts showing "Project Budget by Project Name" to identify the most expensive initiatives (e.g., "Product Launch" at $80k).

##  Insights And Recommendations

**Insights**
- Sales department has the highest project budget allocation (~$150K), indicating a strong focus on revenue-driven initiatives
- Engineering and Marketing also receive significant funding, supporting product development and brand growth
Human Resources shows lower capital allocation, suggesting underinvestment in employee engagement initiatives
- A noticeable portion of projects are still upcoming (~64%), indicating future financial commitments
- Some departments show high salary costs relative to project cost, which may affect profitability

**Recommendations**

- Audit HR Spending: Investigate the negative capital in the HR department to see if operational efficiencies can be improved or if the data reflects a specific one-time investment.

- Reallocate Sales Budget: Since Sales is the highest contributor to capital, consider shifting budget from lower-performing "Upcoming" projects in IT or Engineering to Sales to maximize ROI.

- Project Milestone Review: Given the high percentage of "Upcoming" projects, management should implement a monthly milestone review to ensure these projects don't exceed their $1.6M total budget.

## Tech Stack
Tool: Power BI Desktop, Excel, SQL 

Data Source: Excel / SQL (Internal HR & Project Logs)

Visuals: Custom KPI Cards, Donut Charts, Stacked Bar Charts, Table with Conditional Formatting.


