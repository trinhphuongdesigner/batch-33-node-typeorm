CREATE PROCEDURE usp_Products_GetByDiscount
  @MinDiscount DECIMAL(18, 2)
AS
BEGIN
  SELECT * FROM Products AS P
  WHERE (P.Discount = @MinDiscount)
END

«««««««««««««««««««««««««  »»»»»»»»»»»»»»»»»»»»»»»»»

CREATE PROCEDURE usp_Orders_GetAll
AS
BEGIN
  SELECT * FROM Orders AS O
END

«««««««««««««««««««««««««  »»»»»»»»»»»»»»»»»»»»»»»»»

CREATE OR ALTER PROCEDURE usp_Orders_GetAll
AS
BEGIN
  SELECT
    O.*,
    (SELECT C.* FROM Customers AS C WHERE C.Id = O.customerId FOR JSON PATH, WITHOUT_ARRAY_WRAPPER) AS Customer
    (SELECT E.* FROM Employees AS E WHERE E.Id = O.employeeId FOR JSON PATH, WITHOUT_ARRAY_WRAPPER) AS Employee
  FROM Orders AS O;
END

«««««««««««««««««««««««««  »»»»»»»»»»»»»»»»»»»»»»»»»

CREATE PROCEDURE usp_Customers_GetByYearOfBirth
  @Year INT = 1990
AS
BEGIN
  SELECT * FROM Customers AS C
  WHERE YEAR(C.Birthday) = @Year
END
