# Global-Electronic-Retailer-Dashboard
📊 Turning Raw Sales Data into Business Insights | Power BI Story
In today’s data-driven world, it’s not about having more data — it’s about finding the right insights that drive decisions.
I recently worked on a Global Electronics Retailers KPI Dashboard using a dataset from Kaggle to explore how sales, cost, and profit vary across countries, categories, and time.

https://raw.githubusercontent.com/purvasavant92-sys/Global-Electronic-Retailer-Dashboard/refs/heads/main/Sales%20Dashboard.jpg
________________________________________
💡 The Challenge
The dataset represented a global retail business selling electronics through both online and offline stores.
The goal was to answer a few critical business questions:
•	Which product categories bring the highest profit margins?
•	How do sales trends change across years and regions?
•	Are we meeting our profit targets?
•	What could next year’s sales look like?
________________________________________
⚙️ My Approach
•	Built a clean data model in Power BI (star schema connecting Sales, Products, Stores, Customers & Calendar tables).
•	Created DAX measures for Total Sales, Profit, Cost, % Profit, Target Profit, and Forecasted Sales.
•	Added interactive filters for store type, product brand, category, and time period.
•	Designed visuals to tell a cohesive story — from KPIs to deep-dive breakdowns.
________________________________________
📈 Insights Uncovered
•	Home Appliances emerged as the highest contributor to overall profit.
•	United States and United Kingdom led in sales volume, but some European markets had stronger profit ratios.
•	The Year-over-Year trend revealed significant growth in 2018–2019 before flattening post-2020.
•	Forecast analysis projected steady recovery aligned with global retail trends.
________________________________________
🎯 Business Impact
This dashboard acts as a decision-support system — enabling stakeholders to:
•	Identify profitable product lines and underperforming regions
•	Adjust pricing strategies based on cost-profit insights
•	Plan future sales targets and budgets more accurately
In short, what started as raw transactional data transformed into a story of business performance, strategy, and growth.

DAX Measures: 
Total Sales =  SUMX(Sales,Sales[Quantity] * RELATED(Products[Unit Price USD]))/ 100

Total Cost = SUMX(Sales,Sales[Quantity] * RELATED(Products[Unit Cost USD]))/ 100

Forcaste Sales = 
VAR FOR_YEAR = CALCULATE(MAX('Calendar'[Year]) -1,ALL('Calendar')) // SAME AS SAMEPERIODLASTYEAR
VAR SALES_ = CALCULATE(SUM(Sales[Sales]),'Calendar'[Year] = FOR_YEAR)
VAR No_OF_MONTH = CALCULATE(DISTINCTCOUNT('Calendar'[Month]),'Calendar'[Year] = FOR_YEAR)
VAR AVG_SALES = SALES_/No_OF_MONTH
RETURN AVG_SALES *12

SELECTED PROFIT = 
VAR selectyr = SELECTEDVALUE(Sales[Year of order])
RETURN
IF(ISBLANK(selectyr),[Total Profit],
ABS(
CALCULATE(SUMX(Sales, Sales[Quantity] * RELATED(Products[Profit per Unit]))/ 100, Sales[Year of order] = selectyr )))


TARGET PROFIT VALUE = 
VAR Selectyr = SELECTEDVALUE('Calendar'[Year])
VAR tar =
(CALCULATE(SUMX(Sales,Sales[Total Profit]),'Calendar'[Year] = Selectyr - 1) - CALCULATE(SUMX(Sales,Sales[Total Profit]),'Calendar'[Year]= YEAR(TODAY()) -6)) * 2
RETURN 
IF(ISBLANK(Selectyr),[Total Profit] * 2,ABS(tar))


________________________________________
🧠 Tools & Techniques:
Power BI | DAX | Power Query | Data Modeling | KPI Visualization
________________________________________

#PowerBI #DataAnalytics #DataStorytelling #BusinessIntelligence #DAX #DataVisualization #Analytics #DataDriven #Kaggle #PowerQuery #DashboardDesign

