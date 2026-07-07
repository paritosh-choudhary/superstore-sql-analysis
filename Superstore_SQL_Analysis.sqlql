--                SUPERSTORE SALES ANALYSIS USING SQL


-- Project  : Superstore Sales Analysis using SQL
-- Dataset  : Sample Superstore (9,994 Records)

-- Objective:
-- Analyze sales, profit, customer segments, products,
-- shipping modes, and regional performance using SQL.

-- Skills Demonstrated:
-- • Data Exploration
-- • Data Cleaning
-- • Aggregate Functions
-- • GROUP BY
-- • ORDER BY
-- • CASE Statements
-- • HAVING Clause
-- • Subqueries
-- • Common Table Expressions (CTEs)
-- • Window Functions
-- • Views
-- • Business Insights


-- 1. DATA EXPLORATION

-- Display complete dataset
SELECT *
FROM superstore;

-- Count total number of records
SELECT COUNT(*)
FROM superstore;

-- Display unique countries
SELECT DISTINCT Country
FROM superstore;

-- Display unique cities
SELECT DISTINCT City
FROM superstore;

-- Display unique states
SELECT DISTINCT State
FROM superstore;

-- Display unique product categories
SELECT DISTINCT Category
FROM superstore;

-- Display maximum, minimum and average sales
SELECT
    MAX(Sales),
    MIN(Sales),
    AVG(Sales)
FROM superstore;

-- Display maximum and minimum profit
SELECT
    MAX(Profit),
    MIN(Profit)
FROM superstore;



-- 2. DATA QUALITY CHECKS

-- Display all loss-making orders
SELECT *
FROM superstore
WHERE Profit < 0;

-- Display total profit by sub-category
SELECT
    Sub_Category,
    SUM(Profit) AS Total_Profit
FROM superstore
GROUP BY Sub_Category
ORDER BY Total_Profit;


-- 3. SALES & PROFIT ANALYSIS

-- Display total sales
SELECT SUM(Sales) AS Total_Sales
FROM superstore;

-- Display total profit
SELECT SUM(Profit) AS Total_Profit
FROM superstore;

-- Display average sales
SELECT AVG(Sales) AS Average_Sales
FROM superstore;

-- Display average profit
SELECT AVG(Profit) AS Average_Profit
FROM superstore;

-- Display average discount
SELECT AVG(Discount) AS Average_Discount
FROM superstore;

-- Display average profit for each discount level
SELECT
    Discount,
    AVG(Profit) AS Average_Profit
FROM superstore
GROUP BY Discount
ORDER BY Discount;


-- CATEGORY ANALYSIS

-- Display total sales by category
SELECT
    Category,
    SUM(Sales) AS Total_Sales
FROM superstore
GROUP BY Category;

-- Display top 10 highest sales orders
SELECT *
FROM superstore
ORDER BY Sales DESC
LIMIT 10;

-- Display total profit by category
SELECT
    Category,
    SUM(Profit) AS Total_Profit
FROM superstore
GROUP BY Category;

-- Display top 10 highest profit orders
SELECT *
FROM superstore
ORDER BY Profit DESC
LIMIT 10;

-- Display total number of orders by category
SELECT
    Category,
    COUNT(Quantity) AS Orders
FROM superstore
GROUP BY Category
ORDER BY Orders DESC;


-- REGION ANALYSIS

-- Display total sales by region
SELECT
    Region,
    SUM(Sales) AS Total_Sales_By_Region
FROM superstore
GROUP BY Region;

-- Display total profit by region
SELECT
    Region,
    SUM(Profit) AS Total_Profit_By_Region
FROM superstore
GROUP BY Region;


-- STATE ANALYSIS

-- Display top 10 states by sales
SELECT
    State,
    SUM(Sales) AS Total_Sales_By_State
FROM superstore
GROUP BY State
ORDER BY Total_Sales_By_State DESC
LIMIT 10;

-- Display top 10 states by profit
SELECT
    State,
    SUM(Profit) AS Total_Profit_By_State
FROM superstore
GROUP BY State
ORDER BY Total_Profit_By_State DESC
LIMIT 10;


-- CITY ANALYSIS

-- Display top 10 cities by profit
SELECT
    City,
    SUM(Profit) AS Total_Profit_By_City
FROM superstore
GROUP BY City
ORDER BY Total_Profit_By_City DESC
LIMIT 10;


-- CUSTOMER SEGMENT ANALYSIS

-- Display total sales by segment
SELECT
    Segment,
    SUM(Sales) AS Total_Sales
FROM superstore
GROUP BY Segment;

-- Display total profit by segment
SELECT
    Segment,
    SUM(Profit) AS Total_Profit
FROM superstore
GROUP BY Segment;

-- Display average discount by segment
SELECT
    Segment,
    AVG(Discount) AS Average_Discount
FROM superstore
GROUP BY Segment;


-- SHIPPING MODE ANALYSIS

-- Display sales and profit by shipping mode
SELECT
    Ship_Mode,
    SUM(Sales) AS Total_Sales,
    SUM(Profit) AS Total_Profit
FROM superstore
GROUP BY Ship_Mode;


-- PRODUCT ANALYSIS

-- Display total sales by sub-category
SELECT
    Sub_Category,
    SUM(Sales) AS Total_Sales
FROM superstore
GROUP BY Sub_Category
ORDER BY Total_Sales DESC;

-- Display total profit by sub-category
SELECT
    Sub_Category,
    SUM(Profit) AS Total_Profit
FROM superstore
GROUP BY Sub_Category
ORDER BY Total_Profit DESC;

-- Display total quantity sold by category
SELECT
    Category,
    SUM(Quantity) AS Total_Quantity
FROM superstore
GROUP BY Category;

-- Display total quantity sold by sub-category
SELECT
    Sub_Category,
    SUM(Quantity) AS Total_Quantity
FROM superstore
GROUP BY Sub_Category
ORDER BY Total_Quantity DESC;

-- WINDOW FUNCTIONS

-- Rank states based on total sales
SELECT
    State,
    SUM(Sales) AS Total_Sales,
    RANK() OVER (ORDER BY SUM(Sales) DESC) AS Ranking
FROM superstore
GROUP BY State;

-- Rank cities based on total profit
SELECT
    City,
    SUM(Profit) AS Total_Profit,
    RANK() OVER (ORDER BY SUM(Profit) DESC) AS Ranking
FROM superstore
GROUP BY City;

-- Dense rank sub-categories based on total sales
SELECT
    Sub_Category,
    SUM(Sales) AS Total_Sales,
    DENSE_RANK() OVER (ORDER BY SUM(Sales) DESC) AS Dense_Ranking
FROM superstore
GROUP BY Sub_Category;

-- Number all orders within each region based on sales
SELECT
    Region,
    Sales,
    ROW_NUMBER() OVER (
        PARTITION BY Region
        ORDER BY Sales DESC
    ) AS Order_Number
FROM superstore;

-- Top 5 most profitable cities in each region
WITH City_Profit AS
(
    SELECT
        Region,
        City,
        SUM(Profit) AS Total_Profit,
        RANK() OVER (
            PARTITION BY Region
            ORDER BY SUM(Profit) DESC
        ) AS Ranking
    FROM superstore
    GROUP BY Region, City
)

SELECT
    Region,
    City,
    Total_Profit
FROM City_Profit
WHERE Ranking <= 5
ORDER BY Region, Ranking;


-- CASE STATEMENTS

-- Classify orders based on profit
SELECT
    Category,
    Sub_Category,
    Sales,
    Profit,
    CASE
        WHEN Profit >= 100 THEN 'High_Profit'
        WHEN Profit >= 50 THEN 'Medium_Profit'
        ELSE 'Low_Profit'
    END AS Profit_Category
FROM superstore;

-- Display available discount values
SELECT DISTINCT Discount
FROM superstore
ORDER BY Discount;

-- Categorize discount levels
SELECT
    Category,
    Sub_Category,
    Sales,
    Profit,
    Discount,
    CASE
        WHEN Discount = 0 THEN 'No_Discount'
        WHEN Discount >= 0.4 THEN 'High_Discount'
        WHEN Discount >= 0.2 THEN 'Medium_Discount'
        ELSE 'Low_Discount'
    END AS Discount_Category
FROM superstore;

-- Classify orders as profitable, break-even or loss
SELECT
    Category,
    Sub_Category,
    Sales,
    Profit,
    CASE
        WHEN Profit > 0 THEN 'Profitable'
        WHEN Profit = 0 THEN 'Break_Even'
        ELSE 'Loss'
    END AS Profit_Status
FROM superstore;


-- HAVING CLAUSE

-- Display state-wise sales
SELECT
    State,
    SUM(Sales)
FROM superstore
GROUP BY State
ORDER BY SUM(Sales) DESC;

-- Categories with total sales greater than 150000
SELECT
    Category,
    SUM(Sales) AS Total_Sales
FROM superstore
GROUP BY Category
HAVING Total_Sales >= 150000;

-- States with total profit greater than 15000
SELECT
    State,
    SUM(Profit) AS Total_Profit
FROM superstore
GROUP BY State
HAVING Total_Profit >= 15000;

-- Sub-categories with quantity sold greater than 1500
SELECT
    Sub_Category,
    SUM(Quantity) AS Total_Quantity
FROM superstore
GROUP BY Sub_Category
HAVING Total_Quantity >= 1500;

-- Cities ordered by number of orders
SELECT
    City,
    COUNT(Quantity) AS Orders
FROM superstore
GROUP BY City
ORDER BY Orders DESC;

-- Cities having at least 500 orders
SELECT
    City,
    COUNT(Quantity) AS Orders
FROM superstore
GROUP BY City
HAVING Orders >= 500;


-- SUBQUERIES

-- Display orders with sales greater than the average sales
SELECT *
FROM superstore
WHERE Sales >
(
    SELECT AVG(Sales)
    FROM superstore
);

-- Display orders with profit lower than the average profit
SELECT *
FROM superstore
WHERE Profit <
(
    SELECT AVG(Profit)
    FROM superstore
);

-- Display sub-categories with total sales greater than the average sales of all sub-categories
SELECT
    Sub_Category,
    SUM(Sales) AS Total_Sales
FROM superstore
GROUP BY Sub_Category
HAVING SUM(Sales) >
(
    SELECT AVG(Total_Sales)
    FROM
    (
        SELECT SUM(Sales) AS Total_Sales
        FROM superstore
        GROUP BY Sub_Category
    ) AS AvgSales
);

-- Display states with total profit greater than the average state profit
SELECT
    State,
    SUM(Profit) AS Total_Profit
FROM superstore
GROUP BY State
HAVING SUM(Profit) >
(
    SELECT AVG(Total_Profit)
    FROM
    (
        SELECT
            State,
            SUM(Profit) AS Total_Profit
        FROM superstore
        GROUP BY State
    ) AS Avg_Profit
);


-- COMMON TABLE EXPRESSIONS (CTEs)

-- Top 3 states by total sales
WITH TotalSales_State AS
(
    SELECT
        State,
        SUM(Sales) AS Total_Sales
    FROM superstore
    GROUP BY State
)

SELECT *
FROM TotalSales_State
ORDER BY Total_Sales DESC
LIMIT 3;

-- Top 3 categories by total profit
WITH TotalSales_Category AS
(
    SELECT
        Category,
        SUM(Profit) AS Total_Profit
    FROM superstore
    GROUP BY Category
)

SELECT *
FROM TotalSales_Category
ORDER BY Total_Profit DESC
LIMIT 3;

-- Compare total sales by region
WITH TotalSales_Region AS
(
    SELECT
        Region,
        SUM(Sales) AS Total_Sales
    FROM superstore
    GROUP BY Region
)

SELECT *
FROM TotalSales_Region
ORDER BY Total_Sales DESC;

-- Display segments with positive total profit
WITH Segment_Summary AS
(
    SELECT
        Segment,
        SUM(Sales) AS Total_Sales,
        SUM(Profit) AS Total_Profit
    FROM superstore
    GROUP BY Segment
)

SELECT *
FROM Segment_Summary
WHERE Total_Profit > 0;


-- VIEWS

-- Create a view for state-wise sales
CREATE VIEW Total_State_Sales AS
SELECT
    State,
    SUM(Sales) AS Total_Sales
FROM superstore
GROUP BY State;

-- Display all records from the view
SELECT *
FROM Total_State_Sales;

-- Display the top 5 states by sales
SELECT *
FROM Total_State_Sales
ORDER BY Total_Sales DESC
LIMIT 5;

-- Create a view for category-wise profit
CREATE VIEW Category_Profit AS
SELECT
    Category,
    SUM(Profit) AS Total_Profit
FROM superstore
GROUP BY Category;

-- Display all records from the view
SELECT *
FROM Category_Profit;

-- Display the most profitable category
SELECT *
FROM Category_Profit
ORDER BY Total_Profit DESC
LIMIT 1;

-- Create a view for sub-category summary
CREATE VIEW SubCategory_Summary AS
SELECT
    Sub_Category,
    SUM(Sales) AS Total_Sales,
    SUM(Profit) AS Total_Profit,
    SUM(Quantity) AS Total_Quantity
FROM superstore
GROUP BY Sub_Category;

-- Display profitable sub-categories
SELECT *
FROM SubCategory_Summary
WHERE Total_Profit > 0;


-- BUSINESS INSIGHTS

-- State contributing the highest percentage of total sales
SELECT
    State,
    SUM(Sales) AS Total_Sales,
    ROUND(
        (SUM(Sales) / (SELECT SUM(Sales) FROM superstore)) * 100,
        2
    ) AS Sales_Percentage
FROM superstore
GROUP BY State
ORDER BY Sales_Percentage DESC
LIMIT 1;

-- Category contributing the highest percentage of total profit
SELECT
    Category,
    SUM(Profit) AS Total_Profit,
    ROUND(
        (SUM(Profit) / (SELECT SUM(Profit) FROM superstore)) * 100,
        2
    ) AS Profit_Percentage
FROM superstore
GROUP BY Category
ORDER BY Profit_Percentage DESC
LIMIT 1;

-- Bottom 5 loss-making sub-categories
SELECT
    Sub_Category,
    SUM(Profit) AS Total_Profit
FROM superstore
GROUP BY Sub_Category
ORDER BY Total_Profit
LIMIT 5;

-- Top 5 most profitable cities in each region
WITH City_Profit AS
(
    SELECT
        Region,
        City,
        SUM(Profit) AS Total_Profit,
        RANK() OVER
        (
            PARTITION BY Region
            ORDER BY SUM(Profit) DESC
        ) AS Ranking
    FROM superstore
    GROUP BY Region, City
)

SELECT
    Region,
    City,
    Total_Profit
FROM City_Profit
WHERE Ranking <= 5
ORDER BY Region, Ranking;

-- Compare average profit of discounted and non-discounted orders
SELECT
    CASE
        WHEN Discount = 0 THEN 'Non-Discounted'
        ELSE 'Discounted'
    END AS Discount_Type,
    AVG(Profit) AS Average_Profit
FROM superstore
GROUP BY Discount_Type;

-- Shipping mode with the highest average profit
SELECT
    Ship_Mode,
    AVG(Profit) AS Average_Profit
FROM superstore
GROUP BY Ship_Mode
ORDER BY Average_Profit DESC
LIMIT 1;

-- Analyze the relationship between discount and profit
SELECT
    CASE
        WHEN Discount = 0 THEN 'No Discount'
        WHEN Discount < 0.2 THEN 'Low Discount'
        WHEN Discount < 0.4 THEN 'Medium Discount'
        ELSE 'High Discount'
    END AS Discount_Category,
    AVG(Profit) AS Average_Profit,
    SUM(Profit) AS Total_Profit,
    COUNT(*) AS Total_Orders
FROM superstore
GROUP BY Discount_Category;

-- Conclusion:
-- Based on the results,
-- higher discount categories tend to have lower
-- average profit than low or no discount categories.
