
# MySQL_commands
my sql commands

# # ..data Bases

`create database nameX;`  **|create a dataBase**

`show databases;` **|shows all dataBases**

------------------------------------------

`use dataBaseName;` **|to use x dataBase**

-------------------------------------------
# # ..table

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
# #...Insert Data in tables

`insert into tableName`

`1st ()` **~in which column**

`2nd ()` **~things to add**

```
insert into animales (tipo, estado) VALUES('franco','feliz');
```
------------------------------------
# #... Modified table

`ALTER TABLE tableName MODIFY COLUMN columnName TypeofColumn FUNCTION `

```
ALTER TABLE animales MODIFY COLUMN id int auto_increment;
```

--------------------------------------
# #... List registers

`select * FROM tableName;` **|consult all elements  inside table**

```
SELECT * from animales;
```

`where` **|select just 1 of the list**

```
SELECT * FROM animales WHERE id = 1; 
```

`where  columnName = 'feliz';`

```
SELECT * FROM animales WHERE estado = 'feliz';
```
