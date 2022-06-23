
# MySQL_cheatsheet my sql commands
Here the scripts that where used for examples 👇 (most of them from first folder)

https://bit.ly/3rvtqdO

###### 💁commented code is like this ⤵️
` --` SELECT * FROM customers

## 1 Use dataBase
database
```
USE database_name;
```
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

🤙EX 1 | `UNION`🧮 you combine order statuses as 'actual' year and 'archieved'
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


