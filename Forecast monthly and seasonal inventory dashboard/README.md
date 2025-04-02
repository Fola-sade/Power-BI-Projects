## Data Storytelling

Before diving into the technical aspects, here’s a brief data story. I worked with a sales dataset containing 1,366,863 records alongside a Product lookup table that provided additional details about agricultural products from an Acumatica ERP system. To ensure data quality, I performed data cleansing on the Product Table, removing null and empty cells. Out of 10,237 records, I retained 9,763 after cleaning. This step was necessary because the dataset 
wouldn’t load properly without resolving these errors. However, I did not remove any null or empty observations from the sales dataset, as these represented actual sales records. Maintaining consistency in the data was crucial for accurate analysis.
## Objective: 
Forecast monthly and seasonal inventory levels and sales at both the SRID and Price Class levels using the provided datasets. Present your findings in a Power BI dashboard that’s easy to use for sales reps and purchasing managers.
## Challenges Before Analysis
One major challenge was data ambiguity, which could result in inconsistencies, such as having identical values for both forecasted and actual revenue. This required careful handling to ensure the integrity and reliability of the analysis.

In the Data Modeling phase, I addressed issues related to duplicate Unique ID values before establishing the relationship cardinality between the two tables. This was thoroughly documented in the Data Preparation section of this handbook. During the Analysis phase, I created several calculated columns within each table and defined explicit measures, such as the Forecast_Cast measure, to help generate insightful 
charts and Key Performance Indicators (KPIs). On the Sales Team Page of the dashboard, we have four KPI cards displaying key metrics about the business. The Vegetable product class is performing well, showing positive contributions. However, we need to focus on increasing the sales of the Flowers category. One possible approach could be to offer free flowers during Valentine's Day to attract more customers. Additionally, the Unknown category needs further categorization for better clarity.

On the Purchase Page, I have included a line chart that shows the sum of amounts by Price Class. The HSB2B price class is performing the best, making it the most successful in terms of sales.
Note: I have used two slicers in the zip file to filter the charts. These slicers allow you to view the total revenue accumulated by Item Grouping, Genus, or Product Class Category.

### Data Preparation
###### Order Details:
  Please check the Python data script to clean my Product Table. This is the first step.
   - I created a Bridge Table that unified the GP VFS and the Item VFS in a custom column by using the unpivoting then identify this two columns in the new custom column. I removed duplicated in the Bridge Table.
   - For the several sales data. I loaded the three then combined the three data set. The formula can be seen in the data view by clicking the table Combined_Sales. Please ignore the 2023, 2024, 2025 data.
   - I was able to separate all Units, and the calculated_column created for this was able to identify HALFPOUND as 0.5 POUND, Case of as Case, SDS as seeds. Columns to check is UOM_No and UOM_Text in the combined dataset. 
   - I observed that each instance in the ComponentQtyMap includes the unit of measure, which appears in the sales data. Therefore, I believe the data is updated whenever a new unit of measure is encountered.
       - I considered converting all other units to pounds (LB) and then standardizing the LB value. I believe this is a valid approach to accurately measure the total quantity of products.
###### Item Grouping (VFS):
   - For 2023/2024 data: Grouped items using the first 9 characters of the ItemNumber. I made a chart to see how I have ItemNumber looks now.
   - For 2025 data: Grouped items using all characters before the hyphen. I made a chart to see how I have ItemNumber looks now.
   - Combine the complete sales data into Combined_Sales.
###### Relationship Cardinality Done:
1. One -to-One : Bridge Product table ItemNumber column – Product Table Inventory ID column.
2. One-to-Many: Bridge Product table ItemNumber column – Combined_Sales Item Number column.
3. One-to-Many: Date Table Date column to Combined_Sales Date column.

