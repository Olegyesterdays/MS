# Практическое задание Online Store Transactions

Рассмотрим упрощенную схему базы данных для интернет-магазина со следующими таблицами:  

Customers (CustomerID, FirstName, LastName, Email)  
Products (ProductID, ProductName, Price)  
Orders (OrderID, CustomerID, OrderDate, TotalAmount)  
OrderItems (OrderItemID, OrderID, ProductID, Quantity, Subtotal)  

Ваша задача —написать транзакции SQL для реализации следующих сценариев:
### Сценарий 1:
Напишите транзакцию, имитирующую размещение заказа. В заказе должны быть указаны:
1. Новая запись о заказе в таблице Orders.
2. Позиции заказа добавлены в таблицу OrderItems с соответствующими количествами и промежуточными итогами.
3. Обновите общую сумму в таблице «Заказы» на основе суммы промежуточных итогов по позициям заказа.
### Сценарий 2:
Напишите транзакцию, которая обновляет адрес электронной почты клиента в таблице «Клиенты». Убедитесь, что обновление является атомарным и не вызывает несоответствий.
### Сценарий 3:
Напишите транзакцию, которая добавляет новый продукт в таблицу Products. Убедитесь, что добавление продукта является атомарным и не оставляет базу данных в inconsistent состоянии.
### Сзоздаём базу данных
```text
CREATE TABLE IF NOT EXISTS Customers (
    CustomerID SERIAL PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Email VARCHAR(50)
);

CREATE TABLE IF NOT EXISTS Products (
    ProductID SERIAL PRIMARY KEY,
    ProductName VARCHAR(50),
    Price DECIMAL
);

CREATE TABLE IF NOT EXISTS Orders (
    OrderID SERIAL PRIMARY KEY,
    CustomerID INT REFERENCES Customers(CustomerID),
    OrderDate TIMESTAMP,
    TotalAmount DECIMAL
);

CREATE TABLE IF NOT EXISTS OrderItems (
    OrderItemID SERIAL PRIMARY KEY,
    OrderID INT REFERENCES Orders(OrderID),
    ProductID INT REFERENCES Products(ProductID),
    Quantity INT,
    Subtotal DECIMAL
);
```
### Сценарий 1: Размещение заказа
```text
BEGIN TRANSACTION;

INSERT INTO Orders (CustomerID, OrderDate, TotalAmount)
VALUES (@CustomerID, GETDATE(), 0);

DECLARE @OrderID INT;
SET @OrderID = SCOPE_IDENTITY();

INSERT INTO OrderItems (OrderID, ProductID, Quantity, Subtotal)
VALUES
    (@OrderID, @ProductID1, @Quantity1, @Subtotal1),
    (@OrderID, @ProductID2, @Quantity2, @Subtotal2),

UPDATE Orders
SET TotalAmount = (
    SELECT SUM(Subtotal)
    FROM OrderItems
    WHERE OrderID = @OrderID
)
WHERE OrderID = @OrderID;

COMMIT TRANSACTION;
```
### Сценарий 2: Обновление адреса электронной почты клиента
```text
BEGIN TRANSACTION;

UPDATE Customers
SET Email = @NewEmail
WHERE CustomerID = @CustomerIDToUpdate;

COMMIT TRANSACTION;
```
### Сценарий 3: Добавление нового продукта
```text
BEGIN TRANSACTION;

INSERT INTO Products (ProductName, Price)
VALUES (@ProductName, @Price);

COMMIT TRANSACTION;
```
