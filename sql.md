# SQL 101 - Learning the Basics
##### SQL & Database General Questions

1. What is Sql ?
* It stands for Structured Query Language . 
* It is the standard programming language used to communicate with database
* We use it to ask for data the query, insert new records ,update exiting inforation or delete data from a database

2. What databases other than PostgreSQL use SQL? 
* MySQL
* Microsoft SQL Server
* Oracale Database 
* SQLite 

Part 1: Setting Up the database using postgresSql 

step 1 ; install the sodtware in your computer

```bash
# 1. Update your system's package list
sudo apt update

# 2. Install PostgreSQL and its extra utilities
sudo apt install postgresql postgresql-contrib -y
```

Step 2 ; Start and Enable the Postgres Service

```bash

# Start the server engine right now
sudo systemctl start postgresql

# Ensure the database turns on automatically whenever you boot up your computer
sudo systemctl enable postgresql
```
Step 3; to verify it successfully running 

```bash
sudo systemctl status postgresql
```
Step 4; log into the postgres console 

```bash
sudo -i -u postgres
```
Step 5; Launch the interactive postgres terminal 

```bash
psql
```


 # CREATING THE SYSTEM 

* This holds all our information .

## Step 1 ; CREATE DATABASE

Environment for the data school_system 

```bash
CREATE DATABASE school_system;
```

## Step 2 ; Switch to the new database environment to create the tables 

```bash
\c school_system
```
Explain command;

1. /c - used to connect database named school_system .Hence, it intsructs the terminal to disconnect from your current database and open a new session and the target database we want to access is the school_system 

## Step 3 ; Inside the database (environment) we need specific structures that hold our data .

a) STRUCTURE THAT HOLDS THE LIST OF NAMES 

```bash
CREATE TABLE students (
    student_id SERIAL PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50)
);
```
Explaining the command ; 

1. Serial ; It tels the database to automatically number each students in systematic order eg 1,2,3,4,5

2. Primary key ; the student_id is the unique identifier hence , no two students can share the same ID 

3. VARCHAR(50); (variable Character) ; VARCHAR(n) the n repesents the maximum number of characters or bytes are allowed in that column it can store letters, numbers and special characters .

## Step 4 ; Inserting data into our tables

Students Table ;

```bash
INSERT INTO students (first_name, last_name) VALUES 
('Purity', 'Nkirote'),
('Brianna', 'Makena'),
('Zion', 'Gitonga'),
('Kenan', 'Ndungu'),
('Grace', 'Magoma'),
('Arlene', 'Khakai');
```
VISUAL REPRESENTATION AS IN SPREADSHEET ;

```bash
 student_id | first_name | last_name 
------------+------------+-----------
          1 | Purity     | Nkirote
          2 | Brianna    | Makena
          3 | Zion       | Gitonga
          4 | Kenan      | Ndungu
          5 | Grace      | Magoma
          6 | Arlene     | Khakai
(6 rows)
```

## Step 5 ; Grades Table for relationship
 
Grades Table ;

```bash
CREATE TABLE grades (
    student_id INT,
    subject VARCHAR(50),
    score INT
);
```

Insert content into the grades table ;

```bash
INSERT INTO grades (student_id, subject, score) VALUES 
(1, 'Math', 95),
(2, 'Math', 88),
(3, 'Science', 91),
(99, 'History', 85);
```
VISUAL REPRESENTATION 

```bash
 score 
-------
    95
    88
    91
    85
(4 rows)
```
## Step 6 ; Using select and from in our data 

* SELECT ; Tells Postgres which columns you want to look at in the data table 

* FROM ; Tells Postgres which table those column live in 

Analogy ; opening a large notebooke FROM students and highlighting only the first column hence SELECT first_name from the table students .

Examples ; 


```bash
SELECT first_name FROM students;
```
Expected Output ;

```bash
 first_name 
------------
 Purity
 Brianna
 Zion
 Kenan
 Grace
 Arlene
(6 rows)
```
To view all columns at once

```bash
SELECT * FROM students;
```
Expected Output ; 

```bash
 student_id | first_name | last_name 
------------+------------+-----------
          1 | Purity     | Nkirote
          2 | Brianna    | Makena
          3 | Zion       | Gitonga
          4 | Kenan      | Ndungu
          5 | Grace      | Magoma
          6 | Arlene     | Khakai
(6 rows)
```

* Alone SELECT also acts like a calculator or a printing tool ;

### Example 1 ; As a calculator 

```bash
SELECT 50 + 25;
```
### Example 2 ; To see the current time 

```bash
SELECT NOW();
```
### Example 3 ; To print plain text 

```bash
SELECT 'Hello Purity';
```

* FROM is a dependeant modifer hence it cant be used alone 

## Step 7 ; The use of WHERE ;

* WHERE , it is a filtering tool . Hence , it filters data on your tables 

### Example 1 ; Using   WHERE to filter names 

* To scan a table and return only the specific rows that match a precise word or text 

```bash
SELECT first_name, last_name FROM students 
WHERE last_name = 'Gitonga';
```
Expected Output ; 
```bash
 first_name | last_name 
------------+-----------
 Zion       | Gitonga
(1 row)
```

### Example 2 ; Using WHERE with numbers 

* You can use mathematical symbols like greater than (>), less than (<), or equals (=) to filter numeric records. Let's find students who scored above a 90 in their classes.

```bash
SELECT student_id, score FROM grades 
WHERE score > 90;
```
Expected Output ;


```bash
 student_id | score 
------------+-------
          1 |    95
          3 |    91
(2 rows)
```

### Example 3 ; Combining filters using AND 

* You can string multiple rules together inside a single WHERE statement to create narrow, exact lookups.

```bash
SELECT * FROM grades 
WHERE score > 90 AND subject = 'Math';
```
* This code looks for a grade where the score is high AND the subject is Math alone 

Expected Output ; 


```bash
 student_id | subject | score 
------------+---------+-------
          1 | Math    |    95
(1 row)
```

## Step 8 ; Use of LIMIT 

* LIMIT restricts the maximum number of rows returned on your screen. If you have millions of rows, running a plain query will crash your computer. LIMIT cuts the list short at a number you choose.

### Example 1 ; Basic Limit

```bash
SELECT * FROM students LIMIT 3;
```
Expected Output ; 

```bash
 student_id | first_name | last_name 
------------+------------+-----------
          1 | Purity     | Nkirote
          2 | Brianna    | Makena
          3 | Zion       | Gitonga
(3 rows)
```
### Example 2 ; Combining WHERE and LIMIT together 

```bash
SELECT score FROM grades WHERE score > 85 LIMIT 1;
```
* Let's look inside the grades table, find scores higher than 85, but restrict the output to just the first single result. 

Expected Output ; 

```bash
 score 
-------
    95
(1 row)
```
# RELATIONSHIP PHASE 

## Step 9. Use of JOIN 

* It is also known as INNER JOIN 

* It looks at both tables and only returns a row if the student_id exists perfectly in both the students table and the grades table.Hence , proves the relationship between both tables 

### Example 1 ; INNER JOIN 

```bash
SELECT students.first_name, grades.subject, grades.score
FROM students
INNER JOIN grades ON students.student_id = grades.student_id;
```

Explain the command ;

1. student.first_name - Looks inside the students table and pull out the first name the (.) , is a connector that means look inisde 

2. grades.score - Looks inside the grades table and pulls put the score columns 


Expected Output ; 

```bash
 first_name | subject | score 
------------+---------+-------
 Purity     | Math    |    95
 Brianna    | Math    |    88
 Zion       | Science |    91
(3 rows)
```

## Step 10. Use of LEFT JOIN

* Left" refers to the first table you mention in your code (students). A LEFT JOIN says: "Give me every single student from my left table, no matter what. If they have a grade in the right table, show it. If they don't, just leave it blank (NULL)."

### Example 1; LEFT JOIN 

```bash
SELECT students.first_name, grades.subject, grades.score
FROM students
LEFT JOIN grades ON students.student_id = grades.student_id;
```
Expected Output ; 

```bash
 first_name | subject | score 
------------+---------+-------
 Purity     | Math    |    95
 Brianna    | Math    |    88
 Zion       | Science |    91
 Kenan      | [null]  | [null]
 Grace      | [null]  | [null]
 Arlene     | [null]  | [null]
(6 rows)
```
## Step 11 ; OUTER JOIN 

* It is written as FULL OUTER JOIN 

* It returns absolutely everything from both tables. If a student has no grade, it shows the student with blank grades. If a grade has no student (like our ghost ID 99), it shows the grade with a blank name.

### Example 1 ; 

```bash
SELECT students.first_name, grades.subject, grades.score
FROM students
FULL OUTER JOIN grades ON students.student_id = grades.student_id;
```
Expected Output 

```bash
 first_name | subject | score 
------------+---------+-------
 Purity     | Math    |    95
 Brianna    | Math    |    88
 Zion       | Science |    91
 Kenan      | [null]  | [null]
 Grace      | [null]  | [null]
 Arlene     | [null]  | [null]
 [null]     | History |    85
(7 rows)
```

## Step 12. Use of VIEW

* Now that we are writing these multi-line JOIN statements, it can become exhausting to re-type them every single time you want to see the combined spreadsheet. Hence , we use VIEW

* A VIEW is a saved, reusable shortcut query. It acts exactly like a regular table on your screen, but it doesn't store any new data itself. It just remembers your favorite JOIN query so you can run it in a single short line.

### Example 1 ; Use of VIEW in INNER JOIN 


```bash
CREATE VIEW student_report_card AS 
SELECT students.first_name, grades.subject, grades.score
FROM students
INNER JOIN grades ON students.student_id = grades.student_id;
```
* Here we have created a view where it saves your multi-line query codes inside its memory 

To verify ; 
* Now, instead of typing that massive 4-line join query again, you can read from your new shortcut just like it's a normal table

```bash
SELECT * FROM student_report_card;
```
Explain the command statement ; 

1.  CREATE VIEW student_report_card AS ..., the three dots ... are just a placeholder meaning "paste your long query code" .Hence creates a new saved shortcut folder and names it sudent_report_card so insead of using the inner join command we use (SELECT * FROM student_report_card;)


Expected Output ; 

```bash
 first_name | subject | score 
------------+---------+-------
 Purity     | Math    |    95
 Brianna    | Math    |    88
 Zion       | Science |    91
(3 rows)
```

### Example 2 ; Use of VIEW in LEFT JOIN 

```bash
CREATE VIEW master_attendance_view AS 
SELECT students.first_name, grades.subject, grades.score
FROM students
LEFT JOIN grades ON students.student_id = grades.student_id;
```
* This saves your flexible LEFT JOIN query under the shortcut name master_attendance_view.

To verify ; 

```bash
SELECT * FROM master_attendance_view;
```
Expected Output ; 

```bash
first_name | subject | score 
------------+---------+-------
 Purity     | Math    |    95
 Brianna    | Math    |    88
 Zion       | Science |    91
 Grace      |         |      
 Arlene     |         |      
 Kenan      |         |      
(6 rows)
```
### Example 3 ; Use of VIEW in OUTER JOIN

```bash
CREATE VIEW all_data_view AS 
SELECT students.first_name, grades.subject, grades.score
FROM students
FULL OUTER JOIN grades ON students.student_id = grades.student_id;
```
* This tells Postgres to save your inclusive FULL OUTER JOIN recipe under the shortcut name all_data_view.

To verify ; 

```bash
SELECT * FROM all_data_view;
```
Expected Output ; 

```bash
 first_name | subject | score 
------------+---------+-------
 Purity     | Math    |    95
 Brianna    | Math    |    88
 Zion       | Science |    91
 Kenan      | [null]  | [null]
 Grace      | [null]  | [null]
 Arlene     | [null]  | [null]
 [null]     | History |    85
(7 rows)
```
# SAFTEY PHASE 

## Step 13 . Use of BEGIN 

* Open up a temporary safety bubble. Any data modifications I type next are just a test. Do not lock them permanently onto the computer's hard drive yet!"

* The terminal moves from school_system=# to school_system=*#.

* The asteric is Postgres signaling the safety mode has been activated 

### Example 1 ; Use of SAVEPOINT and COMMIT

* Now that we are inside the bubble, let's test how to safely edit data. We will change Purity's last name from "Nkirote" to "Honor Student", but we will drop a safety anchor flag along the way.
(A) . SAVEPOINT 

* It is used to isolate and undo specific mistakes inside a long transaction without having to cancel all your other successful work.

```bash
SAVEPOINT before_change;
```
* SAVEPOINT places a digital bookmark in your timeline. If you make a massive mistake on the next step, you can type a command to undo your work back to this exact second without destroying everything else.

(B) . Run the data 

```bash
UPDATE students SET last_name = 'Honor Student' WHERE student_id = 1;
```
* This changes Purity's last name. Let's look at the table inside our bubble by running: SELECT * FROM students LIMIT 1;. You will see her last name says "Honor Student".

(C) . Save Changes Permanently (commit) 

```bash
COMMIT;
```
* This bursts the safety bubble and locks your changes into the hard drive permanently.

* What you will see: Your prompt changes back to a clean school_system=# (the asterisk disappears) and the word COMMIT is printed.

To verify ; 

```bash
SELECT * FROM students WHERE student_id = 1;
```

Expected Output ; 

```bash
 student_id | first_name |   last_name   
------------+------------+---------------
          1 | Purity     | Honor Student
(1 row)
```

(D) . Make a massive mistake 
Step 1; Open the saftey bubble 

```bash
BEGIN;
```
Step 2 ; Make an edit

```bash
UPDATE students SET first_name = 'SQL Maestro' WHERE student_id = 1;
```
Step 3. Drop the checkpoint Flag SAVEPOINT 

```bash
SAVEPOINT name_changed_successfully;
```
Step 4. Make the mistake 

* Delete Zion Gitonga from the Database . 

```bash
DELETE FROM students WHERE student_id = 3;
```
To verify his deleted ; 

```bash
SELECT * FROM students;
```
Step 4 . To go back to the exact time you deleted the name ;

```bash
ROLLBACK TO name_changed_successfully;
```
Step 5. To verify his back

```bash
SELECT * FROM students;
```
# DESTRUCTION PHASE

## Step 14. Use of TRUNCATE TABLE 

* TRUNCATE is used when you want to instantly clear out all the rows of data inside a table, but you want to keep the blank table structure itself so you can reuse it later. It is like taking an eraser to a whiteboard—the writing vanishes, but the board stays on the wall.

### Example 1 ; Wipe out the grades table 

```bash
TRUNCATE TABLE grades;
```
Expected Output ; 

```bash
TRUNCATE TABLE
```
To verify ; 

```bash
SELECT * FROM grades;
```
### Example 2 ; Wipe out students table ; 

```bash
TRUNCATE TABLE students;
```

```bash
SELECT * FROM students;
```
## Step 15. Use of DROP TABLE 

* DROP is much more aggressive than truncate. It does not just erase the data; it destroys the table itself completely out of existence. It is like ripping the whiteboard off the wall and throwing it in the trash.

* Let's completely delete both the grades and students tables. Type these two commands one by one

### Example 1 ; Delete the students table and grades table 

```bash
DROP TABLE grades CASCADE;
DROP TABLE students CASCADE;
```
### Example 2 ; Delete the Database (DROP DATABASE)

```bash
\c postgres
```
### Example 3 ; Erase the whole school system out of existance 

```bash
DROP DATABASE school_system;
```
NB ; If you delete once name use this 

```bash
NSERT INTO students (student_id, first_name, last_name) 
VALUES (3, 'Zion', 'Gitonga');
```
