# Power BI Best Practices

## Power BI Report Development Process

![](https://github.com/SStej/Portfolio/blob/072d5c463d0b48cc0ef14558cb32fa95be1c01ed/Power%20BI%20Best%20Practices/Assets/Development.png)

## Power BI Confusing Vocabulary for Users

![](https://github.com/SStej/Portfolio/blob/072d5c463d0b48cc0ef14558cb32fa95be1c01ed/Power%20BI%20Best%20Practices/Assets/Vocab%201.png)
![](https://github.com/SStej/Portfolio/blob/072d5c463d0b48cc0ef14558cb32fa95be1c01ed/Power%20BI%20Best%20Practices/Assets/Vocab%202.png)

## Report Wireframing
- Preparing a mockup of the report
  - List the information and KPI that are to be visualized
  - For each information type and KPI, decide on the type of visualization
  - Arrance the confirmed visualizations and KPIs in the report
- Acquire the company colour palate, report theme and standards if available
- Document requirements for each element
  - For each visualization and element document the type, filter settings, design settings, data source column(s)

##	Data Cleaning 
- Garbage In Garbage Out
  - We can only get expected result from Power BI if we perform data cleaning to ensure the data is in the expected format
- Data Cleaning steps
  - Check columns statistics and value distribution
    - Sometimes simply looking at the Min/Max values can already help to spot abnormal behaviors in the data
  - Handel Null/Empty/Zero/Error/Duplicates
    - Remove
    - Replace (To a static value or a mapping to correct values if available)
  - Set data types for columns
    - Avoid having “Any” as data type
    - Any column that are not meant for calculation should be treated as text
    - Align case for text values to be consistently upper or lower to avoid errors

##  Query Folding
- Query folding in Power BI Power Query refers to the process of converting M code into native queries for the data source. This allows complex transformations to be executed directly on the data source engine, improving performance by using the data source’s processing power and reducing the data transferred to Power BI which means shorter load time
![](https://github.com/SStej/Portfolio/blob/fada2372ef3047f50bbc66bfa1eaafee654e4e9d/Power%20BI%20Best%20Practices/Assets/Query%20folding.png)

- There are three levels of query folding
  - Full query folding: All transformations are pushed to the source
  - Partial query folding: Only part of the transformations are pushed back to the source
  - No query folding: Query that has transformations that cannot be translated to the language of the data source
- To know if the data source supports query folding, you can check on the query pare of the Power Query editor. Right click on any step in the query and click on View Native Query. If the option is greyed out, it cannot be folded

| Common compatible sources	| Common non-compatible sources |
| ----------- | ----------- |
| SharePoint Lists | Local files ( CSV or Excel) |
| OData feeds | SharePoint Excel files |
| Direct Query capable sources: Azure Synapse Analytics, Azure Data Lake Storage, Azure SQL Data Warehouse | Power Query connections |
| | NoSQL database (MongoDB or Cassandra) |

-	Best practices

:white_check_mark: Avoid complex custom steps and allow as much of data processing as possible on the initial steps that can be folded

:white_check_mark: Always check if the changes can be made of the data source side rather than the query in Power BI

:white_check_mark: After making every transformation step, check for “View Native Query” option to identify if the step can be folded

:white_check_mark: Use Power Query calculated columns instead of using calculated columns in Power BI. This is because DAX calculated columns are populated during refresh time and leverage the Power BI engine increasing the refresh time. 

- Avoid

:x: Applying filters and sorts after non-foldable transformations

:x: Renaming columns and tables after another transformations

:x: Creating calculated columns in DAX. This leads to longer refresh time since it heavily relies on the Power BI engine.

- Example of common foldable transformations
  - Removing or renaming columns
  - Pivoting and unpivoting columns
  - Merging tables that are from the same data source
  - Appending tables that are from the same data source

- Example of common non- foldable transformations
  - Converting a text to date
  - Converting datetime to date
  - Using some logical functions (List.ContainsAny, Table.IsDistinct, Logical.FromText)
  - Cleaning text values
  - Removing characters in text
  - Merging or appending tables from a different source

## Datetable
-	The common practice is to create a datetime table using DAX and the merge with the datetime column of the data table. However, if the granularity is required down to the seconds level, it will create 31 million rows for each year, which causes serious performance issue to the report
-	The best practice is to create one standard date table and one standard time table. Then create relationships between the date and time columns in the data table with the two time intelligence tables separately
-	Create Date table
  - In table view, select New Table and add the following DAX
  -     CalendarDate=CALENDAR(MIN(Table[Date]), MAX(Table[Date]))
- Create Time table
  - In table view, select New Table and add the following DAX
  -     Time = GENERATESERIES(0,1439,1)
  -  Change the column title to Second of the day
  -     Time to second = TIMEVALUE(TIME(FLOOR(Time[Second of the day]/3600,1), MOD (Time[Second of the day]/3600),0))

## Timezone
- Sometimes the date setting in the data source is different to your location, it automatically converts to your location causing a shifted time data
- Switching back to original time zone
  - Check the time zone of the data source (UTC+?)
  - In Power Query, format the original Date column to DateTimeZone format
  - Create a custom column with the following formula
  -     =Table.AddColumn(#”Name of Previous Step”, “Actual Date Time”, each Date.TimeDAte(DateTimeZone.SwitchZone([ReferenceDateColumn], Number of hours to be changed)), type date)

## Connection Modes 
- Import
  - Data is highly compresses, optimized and then imported into Power BI semantic model

| Positives	| Negatives |
| ----------- | ----------- |
|	:white_check_mark: High performance for queries since data is compresses and optimized beforehand | :x: Manual data refresh |
| :white_check_mark: Wide range of capabilities as it supports advance data modeling, complex calculations and transformations | :x: Data imported size is restricted to 1 GB max
| :white_check_mark: Flexibility in data sources – allows for the connection to and combination of multiple data sources	| :x: Data security, governance and compliance concerns since the data is duplicated from the source system and stored within Power BI’s Service |

- Direct Query
  - Queries are sent directly to the data source in real-time as the report is being interacted with

| Positives	| Negatives |
| ----------- | ----------- |
|	:white_check_mark: No model size limitation since no data is imported into Power BI | :x: Not all data sources are supported for direct query |
|	:white_check_mark: No data duplication since the data remains at the source | :x: Limited transformation of data (No built in date hierarchy) |
| :white_check_mark: Data is always up-to-date as it is directly queried from the source	| :x: May cause several reporting performance issues. Aggregations or filters are done by sending two queries to the underlying source . If >1 million rows, queries may fail |

-	Composite
  - This mode allows users to combine data with Import and Direct Query modes within the same report

| Positives	| Negatives |
| ----------- | ----------- |
| :white_check_mark: Flexibility in querying | :x: Security implications as data sent to one data source includes data from another source |
| :white_check_mark: Can establish many-to-many relationships between tables without concerns about unique values in tables | :x: Similar performance issues to DirectQuery |
| :white_check_mark: Create a model that combines both direct query and imported datasets | 		|

- Live
  - Users can connect directly to following data sources like existing data in Power BI semantic model, Azure Analysis Services (AAS) and SQL Server Analysis Services (SSAS)

| Positives	| Negatives |
| ----------- | ----------- |
| :white_check_mark: No data duplication since data remains at the source | :x: Restricts users to 1 data source only |
| :white_check_mark: Ideal for connecting to large scale data source | :x: No transformation of data is allowed |
| :white_check_mark: Data is always up-to-date as it is directly queried from the source | :x: Limited modelling capabilities- cannot modify relationships or add new tables |

-	Direct lake
  - Retrieve data from parquet-formatted files stored in data lake without sending SQL queries

| Positives	| Negatives |
| ----------- | ----------- |
| :white_check_mark: Great performance since the data is read directly from OneLake | :x: Cannot mix with other tables having different connection modes |
| :white_check_mark: No data duplication since the data remains at the source | :x: Limited modelling capabilities- cannot create calculated columns or tables |
| :white_check_mark: Data is always up-to-date as it is directly queried from the source |  |


- Scenarios and Recommendations
![](https://github.com/SStej/Portfolio/blob/fada2372ef3047f50bbc66bfa1eaafee654e4e9d/Power%20BI%20Best%20Practices/Assets/Connection%20modes.png)

## Roles & access in Workspace/Reports/Semantic models/ App

![](https://github.com/SStej/Portfolio/blob/fada2372ef3047f50bbc66bfa1eaafee654e4e9d/Power%20BI%20Best%20Practices/Assets/Roles%20and%20access.png)

## Licenses – Where to publish reports for different license consumers?

![](https://github.com/SStej/Portfolio/blob/fada2372ef3047f50bbc66bfa1eaafee654e4e9d/Power%20BI%20Best%20Practices/Assets/Where%20to%20publish%20report.png)






