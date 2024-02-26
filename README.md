create procedure
Get_Order_with_Customers
as begin select
o.orderID,
o.CustomerID,
c.CompanyName,
o.orderDate,
o.ShippedDate
from
Orders o
inner join 
Customers c on
o.CustomerID = c.CustomerID;
END
