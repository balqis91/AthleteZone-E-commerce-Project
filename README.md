# 🏀 AthleteZone E-commerce Sales & Customer Insights

## 📌 Overview  
This project showcases a **MySQL-based E-commerce database** integrated with **Power BI dashboards** to provide actionable insights into sales, products, and customer trends.  
It tracks **customer purchases, product inventory, and revenue performance** while highlighting key metrics for business decision-making.  

The solution includes:  
- 🗄️ **MySQL Database** (Customers, Products, Orders, Date)  
- 🔑 **Data Cleaning & Updates** (Customer corrections, product renaming, price updates)  
- 📊 **Power BI Dashboards** for sales insights and inventory monitoring  
- 📈 **Key Metrics**: Revenue, Orders, Top Products, and Join Trends  

---

## 📊 Dashboards  

### E-commerce Sales & Customer Insights Dashboard  
<img width="1290" height="727" alt="image" src="https://github.com/user-attachments/assets/36a85d67-4832-4d2a-8005-b0437f5ece5c" />


### Data Model  
<img width="1108" height="627" alt="image" src="https://github.com/user-attachments/assets/aef5a0c3-461a-4c58-96b1-550daee0eacd" />


## ✅ Database Schema  

**Customers Table**
- `CustomerID` (PK)  
- `FirstName`  
- `LastName`  
- `Email_Address`  
- `JoinDate`  

**Products Table**
- `ProductID` (PK)  
- `Name`  
- `Price`  
- `Stock_Quantity`  
- `CustomerID` (FK → Customers)  

**Orders Table**
- `OrderID` (PK)  
- `CustomerID` (FK → Customers)  
- `ProductID` (FK → Products)  
- `OrderDate`  
- `QuantityOrdered`  

**Date Table** *(for Power BI time intelligence)*
- `Date`  
- `Day of Week`  
- `Month`  
- `Quarter`  
- `Year`  

**Relationships**
- Customers (1) → Orders (Many)  
- Products (1) → Orders (Many)  
- Date (1) → Orders (Many)  

---

## 🛠️ SQL Scripts  

### 🔹 Create Database and Tables
```sql
CREATE DATABASE AthleteZone;
USE AthleteZone;

CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY AUTO_INCREMENT,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Email_Address VARCHAR(50),
    JoinDate DATE
);

CREATE TABLE Products (
    ProductID INT PRIMARY KEY AUTO_INCREMENT,
    Name VARCHAR(50),
    Price INT,
    Stock_Quantity INT,
    CustomerID INT,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);

CREATE TABLE Orders (
    OrderID INT AUTO_INCREMENT PRIMARY KEY,
    CustomerID INT,
    ProductID INT,
    OrderDate DATE,
    QuantityOrdered INT,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID),
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
);
INSERT INTO Customers (FirstName, LastName, Email_Address, JoinDate)
VALUES
('James', 'Robert', 'james.robert2@gmail.com', '2021-12-12'),
('Nikky', 'Abbah', 'nikky.abah@gmail.com', '2019-08-31'),
('Liza', 'Jakson', 'lizajackson@gmail,com', '2017-04-29');

INSERT INTO Products (Name, Price, Stock_Quantity, customerID)
VALUES
('Cleanser', 2000, 30, 1),
('Face Towel', 350, 70, 2),
('Body Cream', 3000, 57, 3);

INSERT INTO Orders (CustomerID, ProductID, OrderDate, QuantityOrdered)
VALUES
(1, 1, '2024-04-10', 12),
(2, 3, '2024-04-15', 55),
(3, 2, '2024-04-18', 14);
UPDATE Customers
SET Email_Address = 'james.robert02@gmail.com'
WHERE CustomerID = 1;

UPDATE Products SET Name = 'Basket Ball' WHERE ProductID = 1;
UPDATE Products SET Name = 'Running Shoes' WHERE ProductID = 2;
UPDATE Products SET Name = 'Goalkeeper Gloves' WHERE ProductID = 3;

UPDATE Products SET Price = 1000 WHERE ProductID = 2;
🔍 Findings
Total Revenue: £203K from 3 orders

Top Selling Product: Goalkeeper Gloves

Customer Join Trends: Steady growth across 2017, 2019, and 2021

Inventory Check: Running Shoes had the highest stock level

Data Cleaning: Fixed customer email and renamed products for clarity

📌 Conclusion
The AthleteZone E-commerce project demonstrates how SQL and Power BI can work together to deliver:

Accurate customer insights

Clear sales tracking

Efficient inventory monitoring

Future Improvements

Add more customer demographics (age, region)

Include return/refund data

Build predictive sales models

⚙️ Tools Used
MySQL – Database creation & queries

Power BI – Interactive dashboards

DAX & Power Query – Data cleaning and analysis

ER Modeling – Database schema design

👩‍💻 Created by Balikisu Ajoke Oniyide
