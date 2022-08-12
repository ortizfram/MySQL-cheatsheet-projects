
# MySQL_cheatsheet my sql commands
Here the scripts that where used for examples 👇 (most of them from first folder)

## 👉 Project: Design a store database https://gist.github.com/ortizfram/115771fba59c3a0e5afc40fa0fb59aa9

https://bit.ly/3rvtqdO

###### 💁commented code is like this ⤵️
` --` SELECT * FROM customers
-------------------------------------------
# *️⃣ CREATING a table and INSERTING data:

CREATE TABLE groceries (id INTEGER PRIMARY KEY, name TEXT, quantity INTEGER );

INSERT INTO groceries VALUES (1, "Bananas", 4);

INSERT INTO groceries VALUES (2, "Peanut Butter", 1);

INSERT INTO groceries VALUES (3, "Dark chocolate bars", 2);

SELECT * FROM groceries;

![screenshot-www khanacademy org-2022 08 11-10_13_01](https://user-images.githubusercontent.com/51888893/184141430-57fdb433-7ab5-4167-b24b-02c636e0b7ac.png)
--------------------------------------------
# *️⃣  Querying table:

CREATE TABLE groceries (id INTEGER PRIMARY KEY, name TEXT, quantity INTEGER, aisle INTEGER);


INSERT INTO groceries VALUES (1, "Bananas", 4, 7);

INSERT INTO groceries VALUES(2, "Peanut Butter", 1, 2);

INSERT INTO groceries VALUES(3, "Dark Chocolate Bars", 2, 2);

INSERT INTO groceries VALUES(4, "Ice cream", 1, 12);

INSERT INTO groceries VALUES(5, "Cherries", 6, 2);

INSERT INTO groceries VALUES(6, "Chocolate syrup", 1, 4);


SELECT * FROM groceries WHERE aisle > 5 ORDER BY aisle;

SELECT name FROM groceries;

❗ "giving just names"

![image](https://user-images.githubusercontent.com/51888893/184144221-c3413c79-7a7e-4738-86cc-80af0b1183c6.png)

## 🟡 WHERE & ORDER BY

SELECT * FROM groceries WHERE aisle > 5 aisle ORDER BY aisle

![image](https://user-images.githubusercontent.com/51888893/184146728-56d56602-ad5c-448a-b88f-c694ec6773f8.png)

--------------------------------------------
# *️⃣ Agregating D: 
## 🟡SUM,MAX,AVG--GROUP BY

❗ `SUM/MAX(column)`, instead of Orderby we `GROUP BY` & we select the column we groupby cuse if not , we dont see it ordered

💁 sum the time it will take to finish all tasks

CREATE TABLE todo_list (id INTEGER PRIMARY KEY, item TEXT, minutes INTEGER);

INSERT INTO todo_list VALUES (1, "Wash the dishes", 15);

INSERT INTO todo_list VALUES (2, "vacuuming", 20);

INSERT INTO todo_list VALUES (3, "Learn some stuff on KA", 30);

INSERT INTO todo_list VALUES (4, "finishing lesson", 50);


SELECT SUM(minutes) FROM todo_list


![image](https://user-images.githubusercontent.com/51888893/184161561-10a9aa50-9b78-4cb0-baf5-c704b93ef933.png)

--------------------------------------------
# *️⃣ Complex queries:
## 🟡AND, OR

💁 We've created a table with songs, and in this challenge, you'll use queries to decide what songs to sing. 

CREATE TABLE songs (
    id INTEGER PRIMARY KEY,
    title TEXT,
    artist TEXT,
    mood TEXT,
    duration INTEGER,
    released INTEGER);
    
INSERT INTO songs (title, artist, mood, duration, released)
    VALUES ("Bohemian Rhapsody", "Queen", "epic", 60, 1975);
    
INSERT INTO songs (title, artist, mood, duration, released)
    VALUES ("Let it go", "Idina Menzel", "epic", 227, 2013);
    
INSERT INTO songs (title, artist, mood, duration, released)
    VALUES ("I will survive", "Gloria Gaynor", "epic", 198, 1978);
    
INSERT INTO songs (title, artist, mood, duration, released)
    VALUES ("Twist and Shout", "The Beatles", "happy", 152, 1963);
    
INSERT INTO songs (title, artist, mood, duration, released)
    VALUES ("La Bamba", "Ritchie Valens", "happy", 166, 1958);
    
INSERT INTO songs (title, artist, mood, duration, released)
    VALUES ("I will always love you", "Whitney Houston", "epic", 273, 1992);
    
INSERT INTO songs (title, artist, mood, duration, released)
    VALUES ("Sweet Caroline", "Neil Diamond", "happy", 201, 1969);
    
INSERT INTO songs (title, artist, mood, duration, released)
    VALUES ("Call me maybe", "Carly Rae Jepsen", "happy", 193, 2011);
    

SELECT title FROM songs;

 ❗  'epic' mood or a release date after 1990.*/

 SELECT title FROM songs WHERE mood = "epic" OR released > 1990;

❗  'epic', and released after 1990, and less than 4 minutes long.

 SELECT title FROM songs WHERE mood = "epic" AND released > 1990 AND duration < 240;
 
 ![image](https://user-images.githubusercontent.com/51888893/184189840-8326d6bc-a5ed-438f-989c-d0db65d8dbe7.png)

-------------------------------------------
# *️⃣ Querying IN Subqueries : 
## 🟡 IN, NOT IN
CREATE TABLE exercise_logs
    (id INTEGER PRIMARY KEY AUTOINCREMENT,
    type TEXT,
    minutes INTEGER, 
    calories INTEGER,
    heart_rate INTEGER);

INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("biking", 30, 100, 110);

INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("biking", 10, 30, 105);

INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("dancing", 15, 200, 120);

INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("tree climbing", 30, 70, 90);

INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("tree climbing", 25, 72, 80);

INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("rowing", 30, 70, 90);

INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("hiking", 60, 80, 85);

❗ WHERE `column_name` `IN` `("values", "values2")`

💁exercises outside home , inside home

SELECT * FROM exercise_logs WHERE type IN ("biking", "hiking", "tree climbing", "rowing")

## 🟡 SUBQUERIES
💁 new list of doctor's favourites exercises & why

CREATE TABLE drs_favorites

    (id INTEGER PRIMARY KEY,
    
    type TEXT,
    
    reason TEXT);

INSERT INTO drs_favorites(type, reason) VALUES ("biking", "Improves endurance and flexibility.");

INSERT INTO drs_favorites(type, reason) VALUES ("hiking", "Increases cardiovascular health.");

SELECT type FROM drs_favorites;

💁 to mantain the table update with doctors election of favourites

❗ `subquery`

SELECT * FROM exercise_logs WHERE type IN (SELECT type FROM drs_favorites);

![image](https://user-images.githubusercontent.com/51888893/184194871-5c7b56e5-f3d4-4a37-9225-1618a7ceb6e4.png)

-------------------------------------------
# *️⃣ Restricting grouped results:
	(CREATE TABLE exercise_logs

    (id INTEGER PRIMARY KEY AUTOINCREMENT,
    type TEXT,
    minutes INTEGER, 
    calories INTEGER,
    heart_rate INTEGER);
    
	INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("biking", 30, 115, 110);
	INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("biking", 10, 45, 105);
	INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("dancing", 15, 200, 120);
	INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("dancing", 15, 165, 120);
	INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("tree climbing", 30, 70, 90);
	INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("tree climbing", 25, 72, 80);
	INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("rowing", 30, 70, 90);
	INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("hiking", 60, 80, 85);

	SELECT * FROM exercise_logs;


## 🟡 AS ,HAVING

❗ when we use `HAVING`, we're apliying conditions to the `grouped values` not individual values in individual rows

💁 AVG calories `AS` avg_calories & `having` avg total > 70

	SELECT type, AVG(calories) AS avg_calories FROM exercise_logs
	    GROUP BY type
	    HAVING avg_calories > 70
💁 choosing activities i've done more than 2 times :

❗ `COUNT(*)` all columns where the exercise is repeated 

	SELECT type FROM exercise_logs GROUP BY type HAVING COUNT(*) >= 2;
-------------------------------------------
# # 🟢 SELECT

all or
column
```
SELECT *
SELECT customer_id, fisrt_name
```
- FUNTIONS



🤙 EXAMPLE

🧮 calculate discount w user_points

 `AS var_name`
```
SELECT first_name, points, (points * 10) + 100 AS 'discount factor'
FROM customers
```
aritmatic expression (+,-,/,*,% (reminder of the division))

---------------------------------------
# # 🟢  FROM, WHERE, AND, OR, NOT

- `FROM`

table  (clause words)
```
FROM customers 
```

- `WHERE`
ℹ️ (date values are always represented between  ' ' )
```
WHERE customer_id = 1
WHERE points > 300
WHERE state = 'VA'
WHERE birth_date > '1990-01-01'
```

🤙 EXAMPLE

```
SELECT *
FROM orders
WHERE order_date >= '2019-01-01' 
```


- MULTIPLE CONDITIONS `AND`, `OR`


🤙 EXAMPLE

🧮 birth date gratter than 2019, AND +1000 points

🧮 OR = 1 of 2 conditions AND state = 'virginia'
```
SELECT *
FROM customers
WHERE birth_date >= '1990-01-01' AND points > 1000

SELECT *
FROM customers
WHERE birth_date >= '2019-01-01' 
(OR points > 1000 AND state = 'VA')
```
- `NOT`
```
SELECT *
FROM customers
WHERE NOT (birth_date >= '1990-01-01' AND points > 1000)
```
🤙 EXAMPLE

🧮 get items FOR ORDER #6, WHERE total price greater than 30

```
SELECT * 
from order_items
WHERE order_id = 6 AND unit_price * quantity > 30
```

-------------------------------------
# # 🟢 OPERATORS // NOT, IN, BETWEEN, LIKE, REGEXP, IS NULL

- `IN`, `NOT IN` operator

ℹ️ same as OR but you can write all values together like this :

🤙 EXAMPLE
```
SELECT *
FROM customers
WHERE  state IN ('VA', 'FL', 'GA')
```


- `BETWEEN`

ℹ️ same as <=, >=

🤙 EXAMPLE

```
SELECT *
FROM customers
WHERE points BETWEEN 1000 AND 3000


SELECT *
FROM customers
WHERE birth_date BETWEEN '1-1-1990' AND '2000-1-1'
```

- `LIKE` 

🤙 EXAMPLE

ℹ️ you put the **%** to declare what you re looking for 

🥐 LIKE 'b%' = STARTs w B

🥐 LIKE '%b%' = has a B ANYWhERE

🥐 LIKE '%b' = ENDs w B


🥐 LIKE '_y' = SECOND CHAR equals Y

🧮 when string starts like **b%**:... 

```
SELECT *
FROM customers
WHERE last_name LIKE 'b%'

SELECT *
FROM customers
WHERE last_name LIKE '%b%'

SELECT *
FROM customers
WHERE last_name LIKE '%b'


```
- `REGEXP`

ℹ️ same as LIKE 

🥐 REGEXP '^field' = phrase STARTs w field...

🤙EXAMPLE 🧮 starts w : my , or contains: SE
```
SELECT *
FROM customers
WHERE last_name REGEXP '^my|se'
```

🥐 REGEXP 'field$' = phrase ENDs w ...field

🤙EXAMPLE 🧮 last name ends w :   ey OR on 
```
SELECT *
FROM customers
WHERE last_name REGEXP 'ey$|on$'
```

🥐 REGEXP 'field|Mac' = phrases HAS fiel OR mac ⭐ you can combine them 


🥐 REGEXP '[ae]d' = HAS an A/E BEFORE D

🥐 REGEXP 'd[ae]' = HAS an D after a/e

🤙EXAMPLE 🧮 contains :b  , followed by : r or u
```
SELECT *
FROM customers
WHERE last_name REGEXP 'b[ru]'
```
🥐 REGEXP '[a-d]r' = HAS A--to--D AFTER R

- `IS NULL`  ℹ️ where column is empty

🤙EXAMPLE 🧮 orders that were not shipped
```
SELECT *
FROM orders
WHERE shipped_date IS NULL
```
--------------------------------------
# # 🟢 ORDER BY clause ℹ️ for sorting data for columns

🥐 ORDER BY first_name DESC = descending
```
ORDER BY first_name
```
🤙EXAMPLE 🧮 sort by state descendent,  and if repeated, sort by name
```
SELECT *
FROM customers
ORDER BY state DESC, first_name
```
🤙EXAMPLE 🧮 calculate total_price Where order id = 2 ⭐
```
SELECT *, quantity * unit_price AS total_price
FROM order_items
WHERE order_id = 2
ORDER BY total_price DESC
```

-------------------------------------------
# # 🟢 LIMIT clause 

```
SELECT *
FROM customers
LIMIT 3
```
🥐 LIMIT 6, 3 = offset

🤙EXAMPLE 🧮 dont show first 6, and then show 3 

should be showing 7-9
```
SELECT *
FROM customers
LIMIT 6, 3
```

🤙EXAMPLE🧮 get top 3 loyal customers (more points)
```
SELECT *
FROM customers
ORDER BY points DESC
LIMIT 3

```
-------------------------------------------
# # 🟢 INNER JOINS 
ℹ️ 👁️ if you have same column  in multiple tables, you have to prefix them with the table_name.column

ℹ️ 👁️ ALIAS : is like this > FROM orders o, so nxt time you write it you use **o** for orders

🤙EXAMPLE🧮what im joining is the last 3 columns to order's table that its limited just to order_id
```
SELECT order_id, first_name, last_name,  c.customer_id
FROM orders o
JOIN customers c
	ON o.customer_id =  c.customer_id
```
❓ON o.customer_id =  c.customer_id 👇

this  means we're saying that the foreing key in those 2 tables, will be the same in this NEW TABLE

🤙EXAMPLE🧮 join orders w products , for each order return pr id and name, followed by quantity and unit price from order item table
```
SELECT order_id, p.product_id, quantity, oi.unit_price
FROM order_items oi
JOIN products p ON 
	oi.product_id = p.product_id
```
-------------------------------------------
# # 🟢 JOINING ACROSS DATABASES 
🤙EXAMPLE🧮 combining columns from databases


```
SELECT *
FROM order_items oi
JOIN sql_inventory.products p
	ON oi.product_id = p.product_id
```
-------------------------------------------
# # 🟢 SELF JOINS
🤙EXAMPLE🧮 write the manager's name for every employer 

```
USE  sql_hr;

SELECT 
    e.employee_id,
    e.first_name,
    m.first_name AS manager 
FROM employees e
JOIN employees m 
	ON e.reports_to = m.employee_id 
```
-------------------------------------------
# # 🟢 MULTIPLE JOINS
🧮here we re joining 3 tables 

👇 JOIN customers c

❓in o.customer_id i want -> c.customer_id

ℹ️ 👁️ here we saying that foreign keys of both tables are the same 

👇 JOIN order_statuses os 

❓in o.status i want -> os.order_status_id
```
USE  sql_store;

SELECT 
    o.order_id, 
    o.order_date,
    c.first_name,
    c.last_name,
    os.name AS status
FROM orders o
JOIN customers c
	ON o.customer_id = c.customer_id
JOIN order_statuses os
	ON o.status = os.order_status_id
```
🤙EXAMPLE 🧮 join clients and join payment method to payment
```
USE  sql_invoicing;

SELECT 
	p.date,
    p.invoice_id,
    p.amount,
    c.name,
    pm.name
FROM payments p
JOIN clients c
	ON p.client_id = c.client_id
    -- it says foreing keys are the same
JOIN payment_methods pm
	ON p.payment_method = pm.payment_method_id
	-- we change the number for the payment name

```
❓ ON p.client_id = c.client_id 

ℹ️ 👁️ here we saying that foreign keys of both tables are the same 
-------------------------------------------
# # 🟢 COMPOUND JOINS 
```
USE sql_store;

SELECT *
FROM order_items oi
JOIN order_item_notes oin
	ON oi.order_id = oin.order_Id
    AND oi.product_id = oin.product_id
    
```
-------------------------------------------
# # 🟢 ⭐a IMPLICIT JOIN SYNTAX
⭐ 🧮 slecting and joining everything in **FROM**, you change the **ON** with **WHERE** 👇
```
USE sql_store;
SELECT *
FROM orders o, customers c
-- select & join in FROM
WHERE o.customer_id = c.customer_id
-- change the ON with WHERE
```
❓ the original for this will be 👇

```
SELECT *
FROM orders o 
JOIN customers c
	ON o.cusmer_id = c.customer_id
```
-------------------------------------------
# # 🟢 OUTER JOINS// LEFT JOIN, OUTER J MULTiPLE, SELF OUTER J, 
🧰`LEFT JOIN`

🤙EXAMPLE 🧮 all results are shown wether is empty or not 
```
USE sql_store;
SELECT p.product_id, p.name, oi.quantity
FROM products p
LEFT JOIN order_items oi
	ON p.product_id = oi.product_id
```
🧰 `outer join multiple tables`

🤙EXAMPLE |  🧮we join all orders to customers, and then join shipper id, then oin shipper name
```
USE sql_store;
SELECT 
	c.customer_id,
    c.first_name,
    o.order_id,
    sh.name AS shipper
FROM customers c
LEFT JOIN orders o
	ON c.customer_id = o.customer_id
LEFT JOIN shippers sh
	ON o.shipper_id = sh.shipper_id
ORDER BY c.customer_id
```
🤙EXAMPLE 2 ⭐| 🧮orders, JOIN customers, view all shippers, JOIN status 
```
USE sql_store;

SELECT 
	o.order_date,
    o.order_id,
    c.first_name,
    sh.name AS shipper,
    -- to add sh column
    os.name AS status
FROM orders o 
JOIN customers c 
	ON o.customer_id = c.customer_id
    -- SYNC tables
LEFT JOIN shippers sh 
	ON o.shipper_id = sh.shipper_id
    -- SYNC tables ,left join to sshow all
JOIN order_statuses os
	ON o.status = os.order_status_id
```
🧰 `SELF OUTER JOIN`

🤙EX🧮 here we have employees and 1 of them is the manager so to see him in the list you should uuse LEFT JOIN

```
USE sql_hr;

SELECT 
	e.employee_id,
    e.first_name,
    m.first_name AS manager
FROM employees e
LEFT JOIN employees m
	ON e.reports_to = m.employee_id
ORDER BY manager
```
-------------------------------------------
# # 🟢 ⭐ USING clause 

🧰 `USING ()`

👁️ it only works if the name of column it's exactly the same 

ℹ️ it simplifys joining tables

original 👇
```
USE sql_store;

SELECT*
FROM order_items oi
JOIN order_item_notes oin
	ON oi.order_id = oin.order_Id
    AND oi.product_id = oin.product_id
```
SIMPLIFIED W `USING`
```
USE sql_store;

SELECT*
FROM order_items oi
JOIN order_item_notes oin
	USING (order_Id, product_id)
    -- coma is an AND
```

🤙EX 🧮 complete using boths ON and USING 
```
USE sql_invoicing;

SELECT 
	p.date,
	c.name AS client,
    p.amount,
    pm.name AS payment_method
    -- here we bring the column we want
FROM payments p
JOIN clients c USING (client_id)
JOIN payment_methods pm
	ON p.payment_method = pm.payment_method_id
    -- here we put column id  to link them
```
-------------------------------------------
# # 🔴 Union

ℹ️ here you combing rows from querys

👁️when UNION, number of columns should be equal otherwise you get an error

💁 we select a new STRING that is not an actual column and assign it to a name 

🤙EX 1 ⭐|`UNION`🧮 union w `<>=` conditions for point 'gold', 'bronze', 'silver' 
```
USE sql_store;

SELECT
	c.customer_id,
	first_name,
    c.points,
    'bronze' AS type
FROM customers c
WHERE points < 2000
UNION
SELECT
	c.customer_id,
	first_name,
    c.points,
    'silver' AS type
FROM customers c
WHERE points BETWEEN 2000 AND 3000
UNION
SELECT
	c.customer_id,
	first_name,
    c.points,
    'gold' AS type
FROM customers c
WHERE points > 3000
ORDER BY first_name

	

```

🤙EX 2 | `UNION`🧮 you combine order statuses as 'actual' year and 'archieved'
```
USE sql_store;

SELECT 
	order_id,
    order_date,
    'active' AS status
FROM orders
WHERE order_date >= '2019-01-01'
--
UNION
--
SELECT 
	order_id,
    order_date,
    'archieved' AS status
FROM orders
WHERE order_date < '2019-01-01'

	

```
-----------------------------------------------------
# # 🔵 INSERT a row into table 
ℹ️ `DEFAULT` = to generate an automatical ID that's not the same as others

-----------------------------------------------------
# # 🟢 INSERT MULTIPLES ROWS

🤙EX 🧮 inseting 3 products ...
```
INSERT INTO products (name, quantity_stock, unit_price)
VALUES ('product1', 10, 1.95),
	   ('product2', 12, 4.9),
       ('product3', 166, 1.95)
```
# # 🟢 INSERT HIERARCHICAL ROWS

ℹ️`SELECT LAST_INSERT_ID()` = function  
```
-- funtion
INSERT INTO order_items
VALUES
		(last_insert_id(), 1, 1 , 2.95),
		(LAST_INSERT_ID(),2,1,3.00)
```
--------------------------------------------------
# # 🟢 COPY TABLE , INSERTING IN TABLE W FILTERS
👁️ when creating a cipy like this , SQL ignores `Primary Key` & `AI(auto incrment prop)`
```
-- funtion
INSERT INTO order_items
VALUES
		(last_insert_id(), 1, 1 , 2.95),
		(LAST_INSERT_ID(),2,1,3.00)
```
💁 `TRUNCATE TABLE config command` to delete everything from table

🤙EX 🧮 inserting orders placed before 2019 into orders_archieved that is a copy of orders table 
```
INSERT INTO orders_archieved 
SELECT * 
    
FROM orders
WHERE order_date < '2019-01-01'
```
⭐🧮 creating a copy of records in invoices table, and put them in new table called invoices_archieved, and in cllient id we want client name (so join clients table ) using this as a subquery in the create statement. and only copy invioces that have a payment
```
USE sql_invoicing;

CREATE TABLE invoices_archieved AS
SELECT 
	i.invoice_id,
    i.number,
    c.name AS client,
    i.invoice_total,
    i.payment_total,
    i.invoice_date,
    i.payment_date,
    i.due_date
FROM invoices i 
JOIN clients c
	USING (client_id)
WHERE payment_date IS NOT NULL

```

-----------------------------------------------------------------------
# # 🟢 UPDATE SINGLE ROW
 `UPDATE` = table 
 
 `SET` = here we specify new value for 1 or more columns
 
 `WHERE` = here we specify the record or records that need to be udated
 ```
 USE sql_invoicing;

UPDATE invoices
SET 
	payment_total = 10,
    payment_date = '2019-03-01'
WHERE invoice_id = 1

 ```
# # 🟢 UPDATE MULTIPLE ROWS
 ℹ️ in th WHERE clause insted of = we use IN to specify more than 1 row
 
 🧮 +50 points to customers born before 1990
 ```
 USE sql_store;

UPDATE customers
SET 
	points = points + 50
WHERE birth_date < '1990-01-01'
 ```
 # # 🟢 UPDATE w subquerys
 🧮update all clients located in NY or CA
 ```
 USE sql_invoicing;
UPDATE invoices
SET 
	payment_total = invoice_total * 0.5,
	payment_date = due_date
WHERE client_id = 
			(SELECT client_id
			FROM clients
			WHERE state IN ('NY','CA'))
 ```
```
USE sql_invoicing;
UPDATE invoices
SET 
	payment_total = invoice_total * 0.5,
    payment_date = due_date
WHERE payment_date IS NULL
```
 🧮 update orders commets where points more than 3000 points 
```
USE sql_store;

UPDATE orders
SET comments = 'Gold customer'
WHERE customer_id IN 
				(SELECT customer_id
				FROM customers c
				WHERE points > 3000)
```
--------------------------------------------------------------------------------------------------
# # 🔴DELETING ROWS 
```
USE sql_invoicing;

DELETE FROM invoices
WHERE 	client_id = 	
			(SELECT *
            FROM clients
            WHERE name = 'Myworks')
```
-------------------------------------------------------------------------------------------------
# # 🔵RESTORING DATA BASES
- `file`, `open SQL Script`

- 
