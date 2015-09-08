_1 => "Get me a list of all of our products with above average sales". Send me the number of items in this list._

SELECT inventory.prod_id, products.title, products.price, inventory.sales
FROM inventory
JOIN products
ON inventory.prod_id = products.prod_id
WHERE inventory.sales > (SELECT AVG(sales) FROM inventory)

_2 => Based on the first list, tell me the top 3 selling titles._

SELECT inventory.prod_id, products.title, products.price, inventory.sales
FROM inventory
JOIN products
ON inventory.prod_id = products.prod_id
WHERE inventory.sales > (SELECT AVG(sales) FROM inventory)
ORDER BY inventory.sales DESC
LIMIT 3

_3 => Get me a list of how many orders have been placed by Sam Williams. How many total orders Have been placed?_

SELECT orders.orderid, orders.orderdate, orders.totalamount
FROM orders
JOIN customers
ON orders.customerid = (SELECT customers.customerid FROM customers WHERE customers.firstname = 'Sam' AND customers.lastname = 'Williams')
** BROKEN - multiple Sam Williams **

When was Sam Williams most active ?

(When did he place his orders) ?

_4 => What are the two cheapest PINOCCHIO movies? (PINOCCHIO is the second part of the title of many of our movies)._

send me the names and prices of the two cheapest PINOCCHIO movies

SELECT products.prod_id, products.title, products.price
FROM products
WHERE products.title SIMILAR TO '%PINOCCHIO%'
ORDER BY products.price ASC
LIMIT 2

send me the PINOCCHIO query so I can re-use it later

_5 => Add an auto-incrementing 'id' column to the "reorder" table, then populate that table with two or three lines of data. Remember that when you add rows to an auto-incrementing table, you don't have to include 'id' as one of the columns to populate. It should do it for you. In postgres, SERIAL is the equivalent to auto-increment. (Hint: syntax for this is back on Unit01.md)

Question: if you delete the final record of an auto-incrementing table, and that final record's auto-incremented value (id) was 9, what will be the the value of the next record inserted into the table? In other words, delete 9, and what will the next record be?_

ALTER TABLE reorder ADD COLUMN id SERIAL;
UPDATE reorder SET id = DEFAULT;
ALTER TABLE reorder ADD PRIMARY KEY (id);

INSERT INTO reorder values(1, '2015/01/01', 3, '2015/05/05', 8, '2015/06/06');
INSERT INTO reorder values(2, '2015/02/02', 6, '2015/06/06', 3, '2015/07/06');
INSERT INTO reorder values(3, '2014/08/08', 2, '2015/05/05', 1, '2016/04/04');

send me the answer to this question

Email all of your answers IN ONE EMAIL to complete this assignment.
