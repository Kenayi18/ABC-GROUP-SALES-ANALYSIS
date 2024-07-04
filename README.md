## BI Project Using Power BI

### The Brief
You’ve just been hired by ABC GROUP, a fictional global manufacturing company, to design and deliver an end-to-end business intelligence solution – from scratch!
The Business needs a way to track KPIs (Cost, Revenue, profit), compare current year against previous year sales, Visualise revenue by continent and country, profit by Category and cumulative revenue todate.

![Projectshot](https://github.com/Kenayi18/ABC-GROUP-SALES-ANALYSIS/assets/173837738/eeae1768-a670-4fe8-b03f-55b841c50a1f) [View The Interactive Report Here](https://app.powerbi.com/reportEmbed?reportId=dcccbc40-a3c9-4a52-a9da-335efbee78b0&autoAuth=true&ctid=516d080c-5b7a-4154-ba3a-5404fc5e59cc)

### Dataset
The fictional dataset used for this report "ABC Dataset.xlsx" can be found on this page.

### Tools
Power BI Desktop [Free Download](https://www.microsoft.com/en-us/power-platform/products/power-bi/desktop)

### Data Cleaning and Preparation
I began by importing the dataset into Power Bi's Query editor for data cleaning and transformation, a seperate Calendar table was created by dublicating the order table and using the orderdate column alone to create a new calendar table.

### Modelling
Power BI automatically detected and established relationships between all the tables, except for the Date table. I manually created this relationship by linking 'Order' orderdate to 'Calendar' orderdate in Power BI's Model view.

### Calculated Columns
FullName = Employee[Title]&" "&Employee[FirstName]&" "&Employee[LastName]

Cost = RELATED(Products[UbitCost])

Price = RELATED(Products[UnitPrice])

TotalCost = 'Order'[Cost]*'Order'[Quantity]

Total Sales = 'Order'[Quantity]*'Order'[Price]

Income Group = IF(Customers[AnnualIncome] <= 30000, "Low",
                IF(Customers[AnnualIncome] <= 50000, "Medium",
                IF(Customers[AnnualIncome] <= 80000, "High",
                "Very High")))
                
New Colour = IF(Products[ProductColor] = BLANK(), "No Colour", Products[ProductColor])

### Measures
Revenue = SUM('Order'[Total Sales])

Total_Cost = SUM('Order'[TotalCost])

Average Revenue = AVERAGE('Order'[Total Sales])

Average Cost = AVERAGE('Order'[TotalCost])

Profit = [Revenue] - [Total_Cost]

Previous Year Sales = CALCULATE(SUM('Order'[Total Sales]),
                    SAMEPERIODLASTYEAR('Calendar'[Dates]))
                    
% Variance = DIVIDE([Revenue]-[Previous Year Sales],[Previous Year Sales])

Cumulative_Revenue = CALCULATE(SUM('Order'[Total Sales]),
              Filter(ALL('Calendar'),
              'Calendar'[Dates] <= MAX('Calendar'[Dates])))

TotalCost = SUMX('Order','Order'[Price]*'Order'[Quantity])

### Final Report
[View The Interactive Report Here](https://app.powerbi.com/reportEmbed?reportId=dcccbc40-a3c9-4a52-a9da-335efbee78b0&autoAuth=true&ctid=516d080c-5b7a-4154-ba3a-5404fc5e59cc)

### References
1. [Power BI Forums](https://community.fabric.microsoft.com/t5/Power-BI-forums/ct-p/powerbi)
2. [Google search](https://www.google.com/)
3. [Youtube](https://www.youtube.com/)






