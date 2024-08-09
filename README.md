# Coffee Shop Sales Analysis (Power BI, Excel, DAX, Data Modeling)
Tools & Technologies: Power BI, Excel, DAX, Data Modeling
Data Visualization: Created interactive Power BI dashboards showcasing sales performance by store location, product category, and transaction time.
Key Metrics: Calculated key performance indicators (KPIs) like total sales, average transaction value, and top-performing products.
Data Modeling: Modeled the data to create relationships between various tables for efficient data analysis.
Report Automation: Automated the report refresh and data update process to ensure up-to-date insights.



Here are some suggested keywords and example code snippets for your Coffee Shop Sales Analysis project:

**Power BI Dashboard Design (Sample Power Query M Code)**
let
    Source = Excel.Workbook(File.Contents("sales_data.xlsx"), null, true),
    Sales_Sheet = Source{[Item="Sales",Kind="Sheet"]}[Data],
    PromotedHeaders = Table.PromoteHeaders(Sales_Sheet, [PromoteAllScalars=true]),
    ChangedType = Table.TransformColumnTypes(PromotedHeaders,{{"SalesAmount", type number}, {"TransactionTime", type datetime}, {"ProductCategory", type text}, {"StoreLocation", type text}})
in
    ChangedType

**Python Data Cleaning (Using Pandas)**

# Load data
data = pd.read_csv('sales_data.csv')

# Data Cleaning
data.dropna(inplace=True)  # Remove missing values
data['TransactionTime'] = pd.to_datetime(data['TransactionTime'])  # Convert to datetime

# Data Transformation
data['Month'] = data['TransactionTime'].dt.to_period('M')
monthly_sales = data.groupby(['StoreLocation', 'ProductCategory', 'Month']).agg(
    TotalSales=('SalesAmount', 'sum'),
    AverageTransactionValue=('SalesAmount', 'mean')
).reset_index()
**SQL Query for Data Extraction**
-- Extract sales data with relevant details
SELECT 
    StoreLocation, 
    ProductCategory, 
    TransactionTime, 
    SUM(SalesAmount) AS TotalSales, 
    AVG(SalesAmount) AS AverageTransactionValue
FROM 
    Sales
GROUP BY 
    StoreLocation, 
    ProductCategory, 
    TransactionTime
ORDER BY 
    TotalSales DESC;
**Power BI Data Analysis (DAX Example)**
-- Total Sales
TotalSales = SUM(Sales[SalesAmount])

-- Average Transaction Value
AverageTransactionValue = AVERAGEX(Sales, Sales[SalesAmount])

-- Top Performing Products
TopProducts = 
    TOPN(10, 
        SUMMARIZE(Sales, Sales[ProductName], "TotalSales", [TotalSales]), 
        [TotalSales], 
        DESC
    )

