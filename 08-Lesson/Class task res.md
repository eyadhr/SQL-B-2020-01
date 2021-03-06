# Class task res

```sql
USE mydb;

CREATE TABLE Customer(
	customer_id int primary key,
    cust_name nvarchar(20) not null,
    city nvarchar(20),
    grade float,
    salesman_id int
);

insert into Customer(customer_id,cust_name,city,grade,salesman_id)
	   value(3002, 'Nick Rimando','New York' ,'100','5001'),
			(3007, 'Brad Davis','New York' ,'200','5001'),
            (3005, 'Graham Zusi','California' ,'200','5002'),
            (3008, 'Julian Green','London','300','5002'),
            (3004, 'Fabian Johnson','Paris' ,'300','5006'),
            (3009, 'Geoff Cameron', 'Berlin' ,'100','5003'),
            (3003, 'Jozy Altidor', 'Moscow' ,'200','5007'),
            (3001, 'Brad Guzan', 'London' ,'','5005');

SELECT * FROM Customer;


CREATE TABLE Orders(
	ord_no int primary key,
    purch_amt float not null,
    ord_date date,
    customer_id int,
    salesman_id int
);


INSERT INTO Orders(ord_no,purch_amt,ord_date,customer_id,salesman_id)
VALUES (70001,150.5,2012-10-05,3005,5002),
	   (70009,270.65,2012-09-10,3001,5005),
       (70002,65.26,2012-10-05,3002,5001),
	   (70004,110.5,2012-08-17,3009,5003),
       (70007,948.5,2012-09-10,3005,5002),
	   (70005,2400.6,2012-07-27,3007,5001),
       (70008,5760,2012-09-10,3002,5001),
	   (70010,1983.43,2012-10-10,3004,5006),
       (70003,2480.4,2012-10-10,3009,5003),
	   (70012,250.45,2012-06-27,3008,5002),
       (70011,75.29,2012-08-17,3003,5007),
	   (70013,3045.6,2012-04-25,3002,5001);

```

```sql
-- 1. Write a SQL statement which selects the highest grade for each of the cities of the customers.

SELECT city, Max(grade)
FROM Customer
GROUP BY city;

-- 2. Write a SQL statement to find the highest purchase amount ordered by the each customer with their ID and highest purchase amount.

SELECT customer_id, MAX(purch_amt)
FROM Orders
GROUP BY customer_id;

USE mydb;

-- 3. Write a SQL statement to find the highest purchase amount ordered by the each customer on a particular date with their ID, order date and highest purchase amount.

SELECT customer_id, ord_date, MAX(purch_amt)
FROM Orders
GROUP BY customer_id, ord_date;

-- 4. Write a SQL statement to find the highest purchase amount on a date '2012-08-17' for each salesman with their ID.

SELECT customer_id, MAX(purch_amt)
FROM Orders
WHERE ord_date = '2012-08-17'
GROUP BY salesman_id;

-- 5. Write a SQL statement to find the highest purchase amount with their ID and order date, for only those customers who have highest purchase amount in a day is more than 2000.

SELECT customer_id, ord_date, MAX(purch_amt)
FROM Orders
GROUP BY customer_id, ord_date
HAVING MAX(purch_amt) > 2000.00;

-- 6. Write a SQL statement to find the highest purchase amount with their ID and order date, for those customers who have a higher purchase amount in a day is within the range 2000 and 6000.

SELECT customer_id, ord_date, MAX(purch_amt)
FROM Orders
GROUP BY customer_id, ord_date
HAVING MAX(purch_amt) BETWEEN 2000 AND 6000;

-- 7. Write a SQL statement to find the highest purchase amount with their ID and order date, for only those customers who have a higher purchase amount in a day is within the list 2000, 3000, 5760 and 6000.

SELECT customer_id, ord_date, MAX(purch_amt)
FROM Orders
GROUP BY customer_id, ord_date
HAVING MAX(purch_amt) IN(2000, 3000, 5760, 6000);

-- 8. Write a SQL statement to find the highest purchase amount with their ID, for only those customers whose ID is within the range 3002 and 3007.

SELECT customer_id, MAX(purch_amt)
FROM Orders
WHERE customer_id BETWEEN 3002 AND 3007
GROUP BY customer_id;
USE mydb;

-- 9. Write a SQL statement to display customer details (ID and only highest purchase amount) whose IDs are within the range 3002 and 3007 and highest purchase amount is more than 1000.

SELECT customer_id, MAX(purch_amt)
FROM Orders
WHERE customer_id BETWEEN 3002 AND 3007
GROUP BY customer_id
HAVING max(purch_amt) > 1000;

-- 10. Write a SQL statement to find the highest purchase amount with their ID, for only those salesmen whose ID is within the range 5003 and 5008.

SELECT salesman_id, MAX(purch_amt)
FROM Orders
GROUP BY customer_id
HAVING salesman_id BETWEEN 5003 AND 5008;

```
