
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
## 🟢 SELECT

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
# # 🟢  FROM, WHERE, AND, OR, NOT, IN

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

- `IN`, `NOT IN` operator

ℹ️ same as OR but you can write all values together like this :

🧮 EXAMPLE
```
SELECT *
FROM customers
WHERE  state IN ('VA', 'FL', 'GA')
```

--------------------------------------
# # 🟢 ORDER BY
clause
```
ORDER BY first_name
```
-------------------------------------



-------------------------------------------
# # ..CREATE TABLE

`varchar`  **~char lenght**

`create table nameTable`  **|create x table** (in () you put column names)

```
create table animales(

id  int, 

tipo varchar(255),

estado varchar(255),

PRIMARY KEY(id)


); 
```

![image](https://user-images.githubusercontent.com/51888893/168340629-8e7cb71b-618d-420c-98ba-c9b1cdffd34c.png)


--------------------------------------
# #...INSERT Data in tables

![image](https://user-images.githubusercontent.com/51888893/168631669-6e28cbf4-a29c-4e69-8eba-ce9ef29af9e3.png)

```
insert into product (name, created_by, marca)
values
	('ipad',1,'apple'),
    ('iphone',1,'apple'),
    ('watch',2,'apple'),
    ('macbook',1,'apple'),
    ('imac',3,'apple'),
    ('ipad mini',2,'apple');
```

`insert into tableName`

`1st ()` **~in which column**

`2nd ()` **~things to add**

```
insert into animales (tipo, estado) VALUES('franco','feliz');
```

------------------------------------
# #... MODIFY table

`ALTER TABLE tableName MODIFY COLUMN columnName TypeofColumn FUNCTION `

```
ALTER TABLE animales MODIFY COLUMN id int auto_increment;
```

--------------------------------------
# #... SELECT List registers 

`select * FROM tableName;` **|consult all elements  inside table**

```
SELECT * from animales;
```
///**--GROUP BY**

`count(id)`

```
select count(id), marca FROM product group by marca;
```

how many products had created every user??

```
select count(p.id), u.name from product p left JOIN  user u on u.id = p.created_by group by p.created_by;

```

`limit` **|just first from list**

```
select * from user limit 1;
```

`WHERE VALUE <>= X`
```
select * from user where edad > 15;
```

`where` **|select just 1 of the list**

```
SELECT * FROM animales WHERE id = 1; 
```

`where  columnValue = 'feliz';` **|search 4 values**

```
SELECT * FROM animales WHERE estado = 'feliz';
```

`AND` **|search 4 2 or more values together**

```
SELECT * FROM animales WHERE estado = 'feliz' AND tipo = 'franco' ;
```

`OR` **|one of 2 conditions**

`!=` **|where is not x value** (where email != laly@gmail.com) = gives everything is not that

```
select * from user where email != 'layla@gmail.com'
```

///**--REPLACE COLUMN NAMES**

`select` **|show**

`as` (select column1, column2  AS newNameColumn2 FROM xTable)

```
select id, name AS nombre from user;
```



///**--LIKE**

(emai lLKE) `%gmail`  **|has to FINISH with ONLY gmail**

(email LIKE) `%gmail%` **|SIMILARS could finish with gmail.com**

(value) `LIKE  %gmail%;`

```
select * from user where email LIKE '%gmail%';
```

`between` EX = (WHERE age Between 3 AND 5)

```
select * from user where age between 3 and 5;
```

///**--ORDER by value**

`desc` **|descendent**

`asc` **|ascendent**

```
select * from user ORDER BY age ASC
```

///**--MAX MIN**

`max(value) as assingnedColumnName from user`

```
select max(age) as mayor from user;
```

------------------------------------------------
# #...UPDATE registers

`UPDATE / SET / WHERE`

```
UPDATE animales  SET estado= 'triste' WHERE id = 3;
```

`would give ERROR, u should put ID`

```
UPDATE animales SET estado = 'triste' WHERE tipo = 'jose';
```

----------------------------------------------
# #...DELETE registers

`delete where value = x` **|delete where certain value**

```
DELETE FROM animales WHERE estado ='feliz';
```
![image](https://user-images.githubusercontent.com/51888893/168608640-9a960409-e332-4061-8802-68bfcecfb296.png)

```
DELETE FROM animales WHERE id = 3;
```
------------------------------------------------
# #...JOIN tables MIX

open new Query tab , create new table **to use foreign keys** and join tables

`created-by` **|refers JOINED from table name**

`foreign key` **|primary key from extern table that it`s id**

![image](https://user-images.githubusercontent.com/51888893/168628879-fb91c301-de97-44e6-a576-d117884f42f4.png)

```
 created_by int not null
```

```
foreign key (created_by) references user(id)
```

///**--LEFT JOIN** SHOW ONLY IF TABLE1 HAS CREATED SOMETHING IN TABLE2

`u = alias for user table`

`p = alias for product table`

`created_by` has table 1 User id **|search id from table 1 and joins created_by from table 2**

*ignore ()

select (all column values) FROM (table alias) LEFT JOIN (table alias) `on` table1.xColumn `=` table2.xColumn

```
select u.id, u.email, p.name from user u LEFT JOIN product p ON u.id = p.created_by;
```

`RIGHT JOIN` takes product table as principal

`INNER JOIN` shows if value bttween them exists

`CROSSED JOIN` gives all possibilities (could be giant)

--------------------------------------------------
# #...RENAME table

```
rename table products to product;
```

--------------------------------------------------
# #...DELETE TABLES

```
drop table tableName;
```
------------------------------------------------
# #...CORDINALITY

`1n - 1n` 

![image](https://user-images.githubusercontent.com/51888893/168694317-1b1c2445-ad9d-4542-99c5-4ef371fda0bc.png)

`middle table => 1n - n1` **~would be like order DETAIL** (bananas x4, salame x2, etc...)

![image](https://user-images.githubusercontent.com/51888893/168694612-51bc26f0-e16c-4a33-bd61-acac25190fb9.png)

