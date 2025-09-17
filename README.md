# SALES-DASHBOARD-🔹 Step 1: Data Preparation

Load Orders, People.xlsx, and Returns.xlsx into Power BI.

Clean data (check nulls, fix data types: dates, numbers, text).

Create a Date Table using DAX:

DateTable = CALENDAR (MIN(Orders[Order Date]), MAX(Orders[Order Date]))


Add Year, Month, Quarter, Month-Year, etc.

Mark it as the official Date Table.

🔹 Step 2: Data Modeling

Ensure a star schema:

Fact Table: Orders

Dimensions: People (Employee info), Date, Returns

Relationships:

Orders ↔ Returns (OrderID)

Orders ↔ People (Region/Employee)

Orders ↔ DateTable (Order Date)

🔹 Step 3: DAX Measures

You need YoY measures. Examples:

Return Rate %

Return Rate % = DIVIDE(COUNTROWS(Returns), COUNTROWS(Orders), 0)
Return Rate YoY = 
    CALCULATE([Return Rate %], SAMEPERIODLASTYEAR(DateTable[Date]))


Avg. Return Value

Avg Return Value = AVERAGEX(Returns, Returns[ReturnAmount])
Avg Return Value YoY = 
    CALCULATE([Avg Return Value], SAMEPERIODLASTYEAR(DateTable[Date]))


Top 5 Employees by Return Count

Return Count = COUNTROWS(Returns)
Return Count YoY = 
    CALCULATE([Return Count], SAMEPERIODLASTYEAR(DateTable[Date]))


Monthly Return Trend

Line chart with DateTable[Month] and [Return Count]

Add YoY line overlay with [Return Count YoY].

% Contribution of Each Employee

Employee Contribution % = 
    DIVIDE([Return Count], CALCULATE([Return Count], ALL(People)))
Employee Contribution YoY = 
    CALCULATE([Employee Contribution %], SAMEPERIODLASTYEAR(DateTable[Date]))

🔹 Step 4: Dashboard Design

KPI Cards: Return Rate %, Avg Return Value, Return Count (with YoY up/down indicators).

Line Chart: Monthly return trends with YoY overlay.

Bar Chart: Top 5 employees by returns with YoY difference.

Donut Chart: Employee contribution % (with YoY in tooltip).

Slicers: Employee, Region, Date.

Keep consistent theme & layout (avoid clutter, use corporate-style colors).
