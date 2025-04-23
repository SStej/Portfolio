# Data Analytics Portfolio

Welcome to my portfolio! :blush:

My name is Sakar, I am a data analyst with experience using various data tools to clean, analyze, and visualize data to empower decision making and drive changes :chart_with_upwards_trend:. I am proficient in SQL, Excel, and Python, and have a good understanding of data analytics techniques including, but not limited to data preparation :wrench:, statistical analysis :mag:, charts design :bar_chart:, dashboard building :clipboard:, process documenting :open_file_folder:, training :straight_ruler: and data storytelling:notebook:.

In this portfolio, I have included some of my past projects and the best practices that showcase my technical skills as well as analytical capability. These projects demonstrate my ability to organize, analyze, and present data in a clear and visually appealing way, making it easy for anyone to understand and make informed decisions.

Technical Skills: Excel(VBA, Macros and Office Script), MySQL, Alteryx, Power BI, Python (Pandas, Numpy, Matplotlib)

## Certifications
  - Microdoft Certified Power BI Data Analyst
  - Alterix Designer Core Certification
  - Project Management Certification: PMI Certified Associate Project Manager

![](https://github.com/SStej/Portfolio/blob/6a2068249107e6340d4573dbf8e29a5279dfff67/Assets/Badges.png)

# Table of Contents
  - [Project Experience](https://github.com/SStej/Portfolio/blob/main/README.md#project-experience)
  - [Best Practices](https://github.com/SStej/Portfolio/edit/main/README.md#best-practices)
    
# Project Experience

## Project Portfolio Management

This project was for a major retail company operating in Europe, headquartered in Germany. The clients had a project portfolio with several projects running in parallel. At that time, the project teams and the management were using a google sheet to note all the updates, risks and achievements. However, with the different topics that each team needed to update on and multiple users updating the sheet at the same time, the users were having a hard time to fill in the information. The sheet was laggy and information would sometimes be deleted on accident. At the same time when reviewing the projects during the meeting, the managers would need to constantly scroll and find the information they were looking for. This overall was adding extra time not only in the addition of information but also on the review meetings which could go more than 2.5 hours at a time.

As a solution to optimize the process, a simple power apps interface was developed to enter the information by users that would be stored in a SharePoint list recording all the details and statuses. The SharePoint list was then used as a data source for the Power BI that visualized the information in a structured way providing additional information on the number of projects, their trends and highlights on the “At risk” projects.

![](https://github.com/SStej/Portfolio/blob/cf5dce7ad955e8100223b73b234038f4cda81f88/Assets/Project%20Portfolio_Report%20Hierarchy.png)

The Power BI had three report levels for different level of management. The Timeline view for the senior management for the projects going live over 12 months period. Portfolio view which displayed all the projects by the project stage and the Project Details page that showed specific details about the project. 

![](https://github.com/SStej/Portfolio/blob/cf5dce7ad955e8100223b73b234038f4cda81f88/Assets/Project%20Portfolio_Timeline%20Report.png)

In the Timeline report, the months would be automatically updated each month and bookmark buttons were placed on the month names to filter the entire report to a specific month. The report was also allowed users to drill down to the project details report level. 

![](https://github.com/SStej/Portfolio/blob/cf5dce7ad955e8100223b73b234038f4cda81f88/Assets/Project%20Portfolio_Portfolio%20Report.png)

In the Portfolio report, the key numbers were displayed on the left side with buttons to filter the report to In flight projects, At-risk projects and Blocked projects. The risk metrics counted the numbers by the trend of their status and the table listed all the projects with their status and status throughout the phases. There are also cards showing number of projects by phases. All the numbers had bookmark buttons to filter the report to the specific key number, risk status and project phase. The report was also allowed users to drill down to the project details report level. 

![](https://github.com/SStej/Portfolio/blob/cf5dce7ad955e8100223b73b234038f4cda81f88/Assets/Project%20Portfolio_Project%20Details%20Report.png)

The Project Details report visualized the project information added by the project teams and map the Gantt chart. The report also showed the past and status with the trend arrow moving up for positive change, level for maintained good status and lowered for degrading status. At the same time the status of all weeks was recorded on the top right.

After the implementation of this solution, the project team would open the Portfolio report for weekly review meeting and discussing the updates with the average meeting ranging from 1 – 1.5 hours. Users were pleased with the easy data entry and access to the power BI for reference cutting time spent on making updates and maintaining the data integrity.

## System Data Comparison

In one of the projects, the client company found discrepancy in the same data recorded regarding each project, the product managers and vendor details. The data set was recorded in a system used by all the different offices in different countries. One of country offices had their own separate system recording and maintaining the same information. In theory the global system should include the information separately logged in the local system of that one office, however it was found that the most updated information was mixed in both the datasets as the users were making updates to whichever data they had access to. This meant both the datasets were not accurate and complete. 

The two systems were to be merged into one global system as such the data needed to be cleaned. This was a big task for the users as they did not know where and what needed to be updated because of the turnover in teams. The global dataset had over 170k rows and the local dataset had 60k rows with no primary key column to easily match each row.
The management decided to make the global data set the single source of truth and update the global dataset from the local one. To manage resources effectively in the cleaning a report was needed to know how many rows were matching and missing on either side.

For this I decided to simply use excel to extract the missing rows out and inform the management of the breakdown of the discrepancy

![](https://github.com/SStej/Portfolio/blob/cf5dce7ad955e8100223b73b234038f4cda81f88/Assets/Data%20Comparision.png)

After the missing rows that were not in the global data were extracted into a file, I prepared a waterfall chart to show the breakdown of the discrepancy

![](https://github.com/SStej/Portfolio/blob/cf5dce7ad955e8100223b73b234038f4cda81f88/Assets/Data%20Comparison%20Report.png)

## Sustainability reporting

As part of the company’s sustainability commitments, we were preparing for the ECOVADIS assessment to get certified on the compliance with green initiatives and align with the client’s standards as vendors. As part of the assessment, we prepared an informative Power BI with details on the waste and carbon emission of the company, visualize it and prepare a report that could be submitted as a proof of tracking and at the same time be displayed in the company website.
After compiling data from the electricity bills, water bills and the waste recycling data over the period of time the information were visualized.

![](https://github.com/SStej/Portfolio/blob/cf5dce7ad955e8100223b73b234038f4cda81f88/Assets/Sustainability_Energy.png)
![](https://github.com/SStej/Portfolio/blob/cf5dce7ad955e8100223b73b234038f4cda81f88/Assets/Sustainability_Waste.png)
![](https://github.com/SStej/Portfolio/blob/cf5dce7ad955e8100223b73b234038f4cda81f88/Assets/Sustainability_Water.png)

# Best Practices

Over the period that i have worked using Power BI, I have collected some best practices to implement before and during the develppment process. 
I have complied all of them in this repo

