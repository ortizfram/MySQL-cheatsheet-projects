
# SQL_cheatsheet_exercises
## 👉 Project: Design a store database https://gist.github.com/ortizfram/115771fba59c3a0e5afc40fa0fb59aa9
## 👉 Project: Data dig Marvels Queries https://gist.github.com/ortizfram/0193243ed8376f61548720a9635dc57f
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


## 🟡 AS ,HAVING, COUNT, AVG

❗ when we use `HAVING`, we're apliying conditions to the `grouped values` not individual values in individual rows

💁 AVG calories `AS` avg_calories & `having` avg total > 70

	SELECT type, AVG(calories) AS avg_calories FROM exercise_logs
	    GROUP BY type
	    HAVING avg_calories > 70
💁 choosing activities i've done more than 2 times :

❗ `COUNT(*)` all columns where the exercise is repeated 

	SELECT type FROM exercise_logs GROUP BY type HAVING COUNT(*) >= 2;
-------------------------------------------

	CREATE TABLE books (
	    id INTEGER PRIMARY KEY AUTOINCREMENT,
	    author TEXT,
	    title TEXT,
	    words INTEGER);

	INSERT INTO books (author, title, words)
	    VALUES ("J.K. Rowling", "Harry Potter and the Philosopher's Stone", 79944);
	INSERT INTO books (author, title, words)
	    VALUES ("J.K. Rowling", "Harry Potter and the Chamber of Secrets", 85141);
	INSERT INTO books (author, title, words)
	    VALUES ("J.K. Rowling", "Harry Potter and the Prisoner of Azkaban", 107253);
	INSERT INTO books (author, title, words)
	    VALUES ("J.K. Rowling", "Harry Potter and the Goblet of Fire", 190637);
	INSERT INTO books (author, title, words)
	    VALUES ("J.K. Rowling", "Harry Potter and the Order of the Phoenix", 257045);
	INSERT INTO books (author, title, words)
	    VALUES ("J.K. Rowling", "Harry Potter and the Half-Blood Prince", 168923);
	INSERT INTO books (author, title, words)
	    VALUES ("J.K. Rowling", "Harry Potter and the Deathly Hallows", 197651);
	INSERT INTO books (author, title, words)
	    VALUES ("Stephenie Meyer", "Twilight", 118501);
	INSERT INTO books (author, title, words)
	    VALUES ("Stephenie Meyer", "New Moon", 132807);
	INSERT INTO books (author, title, words)
	    VALUES ("Stephenie Meyer", "Eclipse", 147930);
	INSERT INTO books (author, title, words)
	    VALUES ("Stephenie Meyer", "Breaking Dawn", 192196);
	INSERT INTO books (author, title, words)
	    VALUES ("J.R.R. Tolkien", "The Hobbit", 95022);
	INSERT INTO books (author, title, words)
	    VALUES ("J.R.R. Tolkien", "Fellowship of the Ring", 177227);
	INSERT INTO books (author, title, words)
	    VALUES ("J.R.R. Tolkien", "Two Towers", 143436);
	INSERT INTO books (author, title, words)
	    VALUES ("J.R.R. Tolkien", "Return of the King", 134462);
	
💁 Author with total_words > 1.000.000 & avg_words > 150.000 per book

❗ `SUM(words)` AS total_words   `HAVING` total_words > 1000000;

❗ `AVG(words)` AS avg_words  `HAVING` avg_words > 150000
    

	SELECT author, SUM(words) AS total_words 
	    FROM books GROUP BY author
	    HAVING total_words > 1000000;

	SELECT author, AVG(words) AS avg_words
	    FROM books GROUP BY author
	    HAVING avg_words > 150000
-------------------------------------------
# *️⃣ Results with CASE:
	CREATE TABLE exercise_logs
	    (id INTEGER PRIMARY KEY AUTOINCREMENT,
	    type TEXT,
	    minutes INTEGER, 
	    calories INTEGER,
	    heart_rate INTEGER);

	INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("biking", 30, 100, 110);
	INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("biking", 10, 30, 105);
	INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("dancing", 15, 200, 120);
	INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("dancing", 15, 165, 120);
	INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("tree climbing", 30, 70, 90);
	INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("tree climbing", 25, 72, 80);
	INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("rowing", 30, 70, 90);
	INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("hiking", 60, 80, 85);

	SELECT * FROM exercise_logs;
## 🟡 CASE,WHEN->THEN,ELSE,END
❗ `CASE` is used `like an IF`, `THEN` is `:`, `END as` `'column_name'`, `FROM` `table`;

💁 which of the exercises takes `heart_rate` above max= (220-age), above target(90% of max), within target(50% of max), below t

	SELECT type, heart_rate,
	    CASE 
		WHEN heart_rate > 220-30 THEN "above max"
		WHEN heart_rate > ROUND(0.90 * (220-30)) THEN "above target"
		WHEN heart_rate > ROUND(0.50 * (220-30)) THEN "within target"
		ELSE "below target"
	    END as "hr_zone"
	FROM exercise_logs;
![image](https://user-images.githubusercontent.com/51888893/184364406-095610fa-9d4c-4682-800d-5809e50d80e0.png)


💁 count them: 

	SELECT COUNT(*),
	    CASE 
		WHEN heart_rate > 220-30 THEN "above max"
		WHEN heart_rate > ROUND(0.90 * (220-30)) THEN "above target"
		WHEN heart_rate > ROUND(0.50 * (220-30)) THEN "within target"
		ELSE "below target"
	    END as "hr_zone"
	FROM exercise_logs
	GROUP BY hr_zone;
	
![image](https://user-images.githubusercontent.com/51888893/184364327-4722b4f0-9c64-4055-a9ac-77cb466c88ff.png)

-------------------------------------------
Challenge: Gradebook

	CREATE TABLE student_grades (
	    id INTEGER PRIMARY KEY AUTOINCREMENT,
	    name TEXT,
	    number_grade INTEGER,
	    fraction_completed REAL);

	INSERT INTO student_grades (name, number_grade, fraction_completed)
	    VALUES ("Winston", 90, 0.805);
	INSERT INTO student_grades (name, number_grade, fraction_completed)
	    VALUES ("Winnefer", 95, 0.901);
	INSERT INTO student_grades (name, number_grade, fraction_completed)
	    VALUES ("Winsteen", 85, 0.906);
	INSERT INTO student_grades (name, number_grade, fraction_completed)
	    VALUES ("Wincifer", 66, 0.7054);
	INSERT INTO student_grades (name, number_grade, fraction_completed)
	    VALUES ("Winster", 76, 0.5013);
	INSERT INTO student_grades (name, number_grade, fraction_completed)
	    VALUES ("Winstonia", 82, 0.9045);
💁 /*Select all of the rows, and display the name, number_grade, and percent_completed, 
which you can compute by multiplying and rounding the fraction_completed column.*/

	SELECT name,number_grade,
	ROUND(fraction_completed*100) AS percent_completed
	FROM student_grades;
	
![image](https://user-images.githubusercontent.com/51888893/184371251-47eb1969-8df2-40d5-b0c6-b32c82643ea8.png)

💁  how many students have earned which letter_grade. You can output the letter_grade by using CASE with the number_grade column, outputting 
'A' for grades > 90, ,'B' for grades > 80, 'C' for grades > 70, and 'F' otherwise. 
Then you can use COUNT with GROUP BY to show the number of students with each of those grades.

	SELECT COUNT(*),
	    CASE
		WHEN number_grade > 90 THEN "A"
		WHEN number_grade > 80 THEN "B"
		WHEN number_grade > 70 THEN "C"
		ELSE "F"
	    END AS "letter_grade"
	FROM student_grades
	GROUP BY letter_grade;
	
![image](https://user-images.githubusercontent.com/51888893/184371204-7641e8f6-8ba2-4c27-aceb-84e94d075a40.png)


-------------------------------------------
# *️⃣Splitting data into related tables:
	CREATE TABLE students (id INTEGER PRIMARY KEY,
	    first_name TEXT,
	    last_name TEXT,
	    email TEXT,
	    phone TEXT,
	    birthdate TEXT);

	INSERT INTO students (first_name, last_name, email, phone, birthdate)
	    VALUES ("Peter", "Rabbit", "peter@rabbit.com", "555-6666", "2002-06-24");
	INSERT INTO students (first_name, last_name, email, phone, birthdate)
	    VALUES ("Alice", "Wonderland", "alice@wonderland.com", "555-4444", "2002-07-04");

	CREATE TABLE student_grades (id INTEGER PRIMARY KEY,
	    student_id INTEGER,
	    test TEXT,
	    grade INTEGER);

	INSERT INTO student_grades (student_id, test, grade)
	    VALUES (1, "Nutrition", 95);
	INSERT INTO student_grades (student_id, test, grade)
	    VALUES (2, "Nutrition", 92);
	INSERT INTO student_grades (student_id, test, grade)
	    VALUES (1, "Chemistry", 85);
	INSERT INTO student_grades (student_id, test, grade)
	    VALUES (2, "Chemistry", 95);
## 🟡CROSS JOIN,INNER JOIN,EXPLICIT INNER JOIN
❗cross join: simplest & least usefull matches everything w eveeything

	SELECT * FROM student_grades, students;
❗Inner JOin: (implicit)

	SELECT * FROM student_grades, students
    		WHERE student_grades.student_id = students.id;
❗ ⭐ EXPLICIT INNER JOIN: **JOIN** **ON**, starting just from 1 table, & specify what columns are beeing match on top, you JOIN them from the ID

	SELECT persons.name, hobbies.name FROM persons
	    JOIN hobbies
	    ON persons.id = hobbies.person_id;
	    
## 🟡LEFT OUTER JOIN:
Student's Projects>>>>

	CREATE TABLE students (id INTEGER PRIMARY KEY,
	    first_name TEXT,
	    last_name TEXT,
	    email TEXT,
	    phone TEXT,
	    birthdate TEXT);

	INSERT INTO students (first_name, last_name, email, phone, birthdate)
	    VALUES ("Peter", "Rabbit", "peter@rabbit.com", "555-6666", "2002-06-24");
	INSERT INTO students (first_name, last_name, email, phone, birthdate)
	    VALUES ("Alice", "Wonderland", "alice@wonderland.com", "555-4444", "2002-07-04");

	CREATE TABLE student_grades (id INTEGER PRIMARY KEY,
	    student_id INTEGER,
	    test TEXT,
	    grade INTEGER);

	INSERT INTO student_grades (student_id, test, grade)
	    VALUES (1, "Nutrition", 95);
	INSERT INTO student_grades (student_id, test, grade)
	    VALUES (2, "Nutrition", 92);
	INSERT INTO student_grades (student_id, test, grade)
	    VALUES (1, "Chemistry", 85);
	INSERT INTO student_grades (student_id, test, grade)
	    VALUES (2, "Chemistry", 95);

	CREATE TABLE student_projects (id INTEGER PRIMARY KEY,
	    student_id INTEGER,
	    title TEXT);

	INSERT INTO student_projects (student_id, title)
	    VALUES (1, "Carrotapault");
❗ OUTER: even if they don't have a project they'd appear in the list  

	SELECT students.first_name, students.last_name, student_projects.title
	    FROM students
	    LEFT OUTER JOIN student_projects
	    ON students.id = student_projects.student_id;
	    
![image](https://user-images.githubusercontent.com/51888893/184643675-1b26a9f6-38aa-492e-b7cf-5e403757010e.png)

--------------------------------------------------------
Challenge: Customer's orders >>>>>

	CREATE TABLE customers (
	    id INTEGER PRIMARY KEY AUTOINCREMENT,
	    name TEXT,
	    email TEXT);

	INSERT INTO customers (name, email) VALUES ("Doctor Who", "doctorwho@timelords.com");
	INSERT INTO customers (name, email) VALUES ("Harry Potter", "harry@potter.com");
	INSERT INTO customers (name, email) VALUES ("Captain Awesome", "captain@awesome.com");

	CREATE TABLE orders (
	    id INTEGER PRIMARY KEY AUTOINCREMENT,
	    customer_id INTEGER,
	    item TEXT,
	    price REAL);

	INSERT INTO orders (customer_id, item, price)
	    VALUES (1, "Sonic Screwdriver", 1000.00);
	INSERT INTO orders (customer_id, item, price)
	    VALUES (2, "High Quality Broomstick", 40.00);
	INSERT INTO orders (customer_id, item, price)
	    VALUES (1, "TARDIS", 1000000.00);

💁  one row per each customer, with their name, email, and total amount of money they've spent on orders. Sort the rows according to the total money spent, from the most spent to the least spent.


	SELECT customers.name, customers.email, 
	SUM(orders.price) AS "total"
	FROM customers
	LEFT OUTER JOIN orders
	ON customers.id = orders.customer_id
	GROUP BY customers.id
	ORDER BY orders.price DESC;
	
![image](https://user-images.githubusercontent.com/51888893/184655628-65685de6-48aa-45f8-a0dd-4380180ecf99.png)

## 🟡SELF-JOINS:
buddies for projects >>>>

	CREATE TABLE students (id INTEGER PRIMARY KEY AUTOINCREMENT,
	    first_name TEXT,
	    last_name TEXT,
	    email TEXT,
	    phone TEXT,
	    birthdate TEXT,
	    buddy_id INTEGER);

	INSERT INTO students 
	    VALUES (1, "Peter", "Rabbit", "peter@rabbit.com", "555-6666", "2002-06-24", 2);
	INSERT INTO students 
	    VALUES (2, "Alice", "Wonderland", "alice@wonderland.com", "555-4444", "2002-07-04", 1);
	INSERT INTO students 
	    VALUES (3, "Aladdin", "Lampland", "aladdin@lampland.com", "555-3333", "2001-05-10", 4);
	INSERT INTO students 
	    VALUES (4, "Simba", "Kingston", "simba@kingston.com", "555-1111", "2001-12-24", 3);
❗ you can do it by givving `alias` name to the `same table` & joining `ON` with `alias.id`

	SELECT students.first_name, students.last_name, buddies.email AS buddy_email
	    FROM students
	    JOIN students buddies
	    ON students.buddy_id = buddies.id;
	    
![image](https://user-images.githubusercontent.com/51888893/184658562-c288ae67-e512-4109-9f8a-6991674e667c.png)


