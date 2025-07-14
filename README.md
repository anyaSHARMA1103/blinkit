# blinkit
## SQL CODE--

## Total Sales in Millions (2022)

SELECT * FROM blinkit_data;

SELECT CAST(SUM(Total_Sales) / 1000000 AS DECIMAL(10,2)) AS Total_Sales_Millions
FROM blinkit_data
WHERE Outlet_Establishment_Year = 2022;

##  Average Sales (2022)

SELECT CAST(AVG(Total_Sales) AS DECIMAL(10,1)) AS Avg_Sales 
FROM blinkit_data 
WHERE Outlet_Establishment_Year = 2022;

## Total Items Count (2022)

SELECT COUNT(*) AS No_Of_Items 
FROM blinkit_data 
WHERE Outlet_Establishment_Year = 2022;

## Average Rating

SELECT CAST(AVG(Rating) AS DECIMAL(10,2)) AS Avg_Rating 
FROM blinkit_data;

## Sales by Fat Content

SELECT Item_Fat_Content, SUM(Total_Sales) AS Total_Sales 
FROM blinkit_data 
GROUP BY Item_Fat_Content;

SELECT * FROM blinkit_data;

SELECT CAST(SUM(Total_Sales) / 1000000 AS DECIMAL(10,2)) AS Total_Sales_Millions
FROM blinkit_data
WHERE Outlet_Establishment_Year = 2022;

SELECT CAST(AVG(Total_Sales) AS DECIMAL(10,1)) AS Avg_Sales 
FROM blinkit_data 
WHERE Outlet_Establishment_Year = 2022;

SELECT COUNT(*) AS No_Of_Items 
FROM blinkit_data 
WHERE Outlet_Establishment_Year = 2022;

SELECT CAST(AVG(Rating) AS DECIMAL(10,2)) AS Avg_Rating 
FROM blinkit_data;

SELECT Item_Fat_Content, SUM(Total_Sales) AS Total_Sales 
FROM blinkit_data 
GROUP BY Item_Fat_Content;

## Top 5 Item Types by Sales

SELECT Item_Type,
    CAST(SUM(Total_Sales) AS DECIMAL(10,2)) AS Total_Sales,
    CAST(AVG(Total_Sales) AS DECIMAL(10,1)) AS Avg_Sales,
    COUNT(*) AS No_Of_Items,
    CAST(AVG(Rating) AS DECIMAL(10,2)) AS Avg_Rating
FROM blinkit_data
GROUP BY Item_Type
ORDER BY Total_Sales DESC
LIMIT 5;

## Fat Content Sales by Outlet Location (Pivot)

SELECT Outlet_Location_Type,
    ISNULL([Low Fat], 0) AS Low_Fat,
    ISNULL([Regular], 0) AS Regular
FROM
(
    SELECT Outlet_Location_Type, Item_Fat_Content,
        CAST(SUM(Total_Sales) AS DECIMAL(10,2)) AS Total_Sales
    FROM blinkit_data
    GROUP BY Outlet_Location_Type, Item_Fat_Content
) AS SourceTable
PIVOT
(
    SUM(Total_Sales)
    FOR Item_Fat_Content IN ([Low Fat], [Regular])
) AS PivotTable
ORDER BY Outlet_Location_Type;

##  Outlet Type Sales Summary

SELECT Outlet_Type,
    CAST(SUM(Total_Sales) AS DECIMAL(10,2)) AS Total_Sales,
    CAST((SUM(Total_Sales) * 100.0 / SUM(SUM(Total_Sales)) OVER ()) AS DECIMAL(10,2)) AS Sales_Percentage,
    CAST(AVG(Total_Sales) AS DECIMAL(10,1)) AS Avg_Sales,
    COUNT(*) AS No_Of_Items,
    CAST(AVG(Rating) AS DECIMAL(10,2)) AS Avg_Rating
FROM blinkit_data
GROUP BY Outlet_Type
ORDER BY Total_Sales DESC;

<img width="1886" height="518" alt="image" src="https://github.com/user-attachments/assets/0e8c4be4-dc3c-46aa-bc8c-bc4d38f2bbe2" />

Used PowerBI to analyse-
1) Total Sales by fat content(Donut Chart)
2) Total Sales by Item type(Bar Chart)
3) Fat content by outlet for total sales(Stacked column chart)
4) Total Sales by Outlet Establishment(Line Chart)
   

<img width="2879" height="1430" alt="image" src="https://github.com/user-attachments/assets/cb25a7db-fcd4-4f04-b9ef-1ac2e513c582" />


