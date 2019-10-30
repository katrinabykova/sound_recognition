# Challenge Set 9
## Part I: W3Schools SQL Lab 

*Introductory level SQL*

--

This challenge uses the [W3Schools SQL playground](http://www.w3schools.com/sql/trysql.asp?filename=trysql_select_all). Please add solutions to this markdown file and submit.

1. Which customers are from the UK?

   SELECT * FROM Customers WHERE Country='UK';

   

2. What is the name of the customer who has the most orders?

   CREATE VIEW customers_orders AS
   SELECT CustomerID, COUNT(OrderID) FROM Orders
   GROUP BY CustomerID
   ORDER BY COUNT(OrderID) DESC;

   SELECT customers_orders.*, Customers.CustomerID, Customers.CustomerName
   FROM customers_orders LEFT JOIN Customers
   ON customers_orders.CustomerID=Customers.CustomerID;

   

3. Which supplier has the highest average product price?

   CREATE VIEW x AS
   SELECT Suppliers.SupplierName, Products. Price  
   FROM Supplier LEFT JOIN Products
   ON Suppliers.SupplierID = Products.SupplierID

   SELECT Avg(Price), SupplierName FROM [Supplier_prod]
   GROUP BY SupplierName
   ORDER BY Avg(Price) DESC

4. How many different countries are all the customers from? (*Hint:* consider [DISTINCT](http://www.w3schools.com/sql/sql_distinct.asp).)

   SELECT DISTINCT Country FROM Customers;

5. What category appears in the most orders?

CREATE VIEW order_cat AS
SELECT OrderDetails.OrderID, Products.CategoryID
FROM OrderDetails LEFT JOIN Products
ON OrderDetails.ProductID=Products.ProductID

SELECT * , COUNT(OrderID) FROM order_cat
GROUP BY CategoryID
ORDER BY COUNT(OrderID) DESC

6. What was the total cost for each order?

CREATE VIEW order_total_cost AS 
SELECT OrderDetails.*, Products.ProductID, Products.Price FROM OrderDetails LEFT JOIN Products ON OrderDetails.ProductID = Products.ProductID;

SELECT *, SUM(Price) FROM [order_total_cost]
GROUP BY OrderID

7. Which employee made the most sales (by total price)?

CREATE VIEW order_coast AS
SELECT OrderDetails.OrderID, sum(Price) AS order_price
FROM OrderDetails LEFT JOIN Products
ON Products.ProductID=Products.ProductID
GROUP BY OrderID

SELECT employee_order.order_price, Employees.LastName, Employees.FirstName
FROM employee_order LEFT JOIN Employees
ON employee_order.EmployeeID=Employees.EmployeeID;



8. Which employees have BS degrees? (*Hint:* look at the [LIKE](http://www.w3schools.com/sql/sql_like.asp) operator.)

SELECT * FROM Employees
WHERE Notes
LIKE 'BS';



9. Which supplier of three or more products has the highest average product price? (*Hint:* look at the [HAVING](http://www.w3schools.com/sql/sql_having.asp) operator.)

   CREATE VIEW supp_price AS
   SELECT SupplierID, Avg(Price) 
   AS avg_price 
   FROM Products 
   GROUP BY SupplierID 
   HAVING count(ProductID) >= 3 
   ORDER BY avg_price DESC;

   SELECT supp_price.*, Suppliers.SupplierName
   FROM supp_price LEFT JOIN Suppliers 
   ON supp_price.SupplierID=Suppliers.SupplierID;