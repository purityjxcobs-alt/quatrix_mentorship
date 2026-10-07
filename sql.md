# SQL 101 - Learning the Basics
## SQL & Database General Questions

### 1. What is Sql ?

* It stands for Structured Query Language . 

* It is the standard programming language used to communicate with database

* We use it to ask for data the query, insert new records ,update exiting 
  inforation or delete data from a database

### 2. What databases other than PostgreSQL use SQL? 

* MySQL

* Microsoft SQL Server

* Oracale Database 

* SQLite 

### 3. What is a table 

* A structured collection of data organized into vertical columns and   
  horizontal rows.

### 4. What is a row?

* A single, horizontal line in a table that hold records 

### 5. What is a column 

* A vertical entities that conatins the fields of which the records are 
  placed 

### 6. How do you comment out an SQL line so that it is ignored by the SQL engine?

#### * Single-Line Comments: Type -- (two dashes). Everything after these dashes on that specific line will be ignored.


```bash
-- This entire line is ignored
SELECT * FROM users; -- This comment is at the end of a line
```
#### * Multi-Line Comments: Enclose the text between /* and */. This is useful for ignoring blocks of text across multiple lines.

```bash
/* This is a 
   multi-line comment */
SELECT * FROM orders;
```


# SQL Keywords (Specific to PostgreSQL)

1. CREATE DATABASE
2. CREATE TABLE 
3. SELECT
4. FROM
5. WHERE 
6. LIMIT
7. JOIN
8. LEFT JOIN
9. OUTER JOIN
10. VIEW 
11. BEGIN
12.  = 9999;
DELETE 1
traccar=# SELECT id, name, uniqueid, category FROM tc_devices WHERE id = 9999;
 id | name | uniqueid | category 
----+------+----------+----------
(0 rows)

traccar=# RESET ROLE;
RESET
traccar=# SELECT current_user
;
 current_user 
--------------
SAVEPOINT 
13. COMMIT
14. START TRANSACTION
15. TRUNCATE TABLE 
16. DROP TABLE 
17. DROP DATABASE
18. CREATE 
19. DROP 


## Part 1: Setting Up the database using postgresSql 

### Step 1 : Install the Software in your computer

```bash
sudo apt update
sudo apt install postgresql postgresql-contrib -y
```

### Step 2 : Start and Enable the Postgres Service

```bash
sudo systemctl start postgresql
sudo systemctl enable postgresql
```
### Step 3 : To verify it is successfully running 

```bash
sudo systemctl status postgresql
```
### Step 4 : Log into the postgres console 

```bash
sudo -i -u postgres
```
### Step 5 : Launch the interactive postgres terminal 

```bash
psql
```

# DEMONSTRATING SQL KEYWORDS

# 1. CREATING THE SYSTEM 

* This holds all our information .

## Step 1 : CREATE DATABASE KEYWORD

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

# 2. CREATE TABLE KEYWORD

## Step 3 : Inside the database (environment) we need specific structures that hold our data .

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

## Step 5 : Grades Table for relationship
 
Grades Table ;

```bash
CREATE TABLE grades (
    student_id INT,
    subject VARCHAR(50),
    score INT
);
```

* Insert content into the grades table ;

```bash
INSERT INTO grades (student_id, subject, score) VALUES 
(1, 'Math', 95),
(2, 'Math', 88),
(3, 'Science', 91),
(99, 'History', 85);
```
Expected Output ;

```bash
 score 
-------
    95
    88
    91
    85
(4 rows)
```
# 3. SELECT AND FROM KEYWORD

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

# 4. WHERE KEYWORD

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

# 5. LIMIT KEYWORD 

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

# 9. JOIN KEYWORD

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

# 10. LEFT JOIN KEYWORD

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

# 11. OUTER JOIN KEYWORD

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
# 12. VIEW KEYWORD

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

# 13. BEGIN KEYWORD 

## Step 13 . Use of BEGIN 

* Open up a temporary safety bubble. Any data modifications I type next are just a test. Do not lock them permanently onto the computer's hard drive yet!"

* The terminal moves from school_system=# to school_system=*#.

* The asteric is Postgres signaling the safety mode has been activated 

# 14. SAVEPOINT AND COMMIT KEYWORD 

### Example 1 ; Use of SAVEPOINT and COMMIT

* Now that we are inside the bubble, let's test how to safely edit data. We 
  will change Purity's last name from "Nkirote" to "Honor Student", but we will drop a safety anchor flag along the way.
  (A) . SAVEPOINT 

* It is used to isolate and undo specific mistakes inside a long transaction  
  without having to cancel all your other successful work.

```bash
SAVEPOINT before_change;
```

* SAVEPOINT places a digital bookmark in your timeline. If you make a massive 
  mistake on the next step, you can type a command to undo your work back to this exact second without destroying everything else.

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
### Step 1; Open the saftey bubble 

```bash
BEGIN;
```
### Step 2 ; Make an edit

```bash
UPDATE students SET first_name = 'SQL Maestro' WHERE student_id = 1;
```
### Step 3. Drop the checkpoint Flag SAVEPOINT 

```bash
SAVEPOINT name_changed_successfully;
```
### Step 4. Make amistake 

* Delete Zion Gitonga from the Database . 

```bash
DELETE FROM students WHERE student_id = 3;
```
* To verify his deleted ; 

```bash
SELECT * FROM students;
```
### Step 4 . To go back to the exact time you deleted the name ;

```bash
ROLLBACK TO name_changed_successfully;
```
### Step 5. To verify his back

```bash
SELECT * FROM students;
```
# DESTRUCTION PHASE

# TRUNCATE TABLE KEYWORD

## Step 14. Use of TRUNCATE TABLE 

* TRUNCATE is used when you want to instantly clear out all the rows of data 
  inside a table, but you want to keep the blank table structure itself so you can reuse it later. It is like taking an eraser to a whiteboard—the writing vanishes, but the board stays on the wall.

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
# 15. DROP TABLE KEYWORD

## Step 15. Use of DROP TABLE 

* DROP is much more aggressive than truncate. It does not just erase the data; it destroys the table itself completely out of existence. It is like ripping the whiteboard off the wall and throwing it in the trash.

* Let's completely delete both the grades and students tables. Type these two commands one by one

### Example 1 ; Delete the students table and grades table 

```bash
DROP TABLE grades CASCADE;
DROP TABLE students CASCADE;
```
# 16. DROP DATABASE 

### Example 2 ; Delete the Database (DROP DATABASE)

```bash
\c postgres
```
### Example 3 ; Erase the whole school system out of existance 

```bash
DROP DATABASE school_system;
```

* NB ; If you delete once name use this 

```bash
NSERT INTO students (student_id, first_name, last_name) 
VALUES (3, 'Zion', 'Gitonga');
```

# Create a Database, Table and Insert Records

In our system the ./util/generate_exam_data.

We have a table like this ;

```bash
             List of relations
Schema |      Name       | Type  |  Owner
--------+-----------------+-------+---------
public | county          | table | kkiragu
public | school          | table | kkiragu
public | student         | table | kkiragu
public | student_subject | table | kkiragu
public | subject         | table | kkiragu
(5 rows)
```
#### To navigate from one table to another to see the contents

1. county table 

```bash
SELECT * FROM county;
```
2.  school table 

```bash
SELECT * FROM school;
```
3. student table 

```bash
SELECT * FROM student;
```
4. student_subject 

```bash
SELECT * FROM student_subject;
```
5. subject 

```bash
SELECT * FROM subject;
```
6. to see all the tables content at once we use 

```bash
SELECT * FROM county LIMIT 3;
SELECT * FROM school LIMIT 3;
SELECT * FROM student LIMIT 3;
SELECT * FROM subject LIMIT 3;
SELECT * FROM student_subject LIMIT 3;
```
### EXPECTED OUTPUT 

```bash
 id |  name   
----+---------
  1 | Mombasa
  2 | Kwale
  3 | Kilifi
(3 rows)

 id | county_id |         name         
----+-----------+----------------------
  1 |         1 | Mombasa - National
  2 |         1 | Mombasa - Provincial
  3 |         1 | Mombasa - District
(3 rows)

  id  |      name      |    phone     | county_id | school_id |        email         
------+----------------+--------------+-----------+-----------+----------------------
 1001 | Amber C Atieno | 0720-729-029 |        32 |        26 | acatieno@hotmail.com
 1002 | Amber C Chacha | 0770-778-412 |        32 |       168 | acchacha@hotmail.com
 1003 | Amber C Idris  | 0738-490-302 |        43 |        85 | acidris@yahoo.com
(3 rows)

 id |    name     
----+-------------
  1 | Mathematics
  2 | English
  3 | Swahili
(3 rows)

 student_id | subject_id |  score  
------------+------------+---------
       1001 |          1 | 80.4028
       1001 |          2 | 90.1712
       1001 |          3 | 74.7042
(3 rows)
```

## Query Questions

### 1 . Display students named Alice.


* From the students table .

```bash
SELECT * FROM student WHERE name LIKE 'Alice%';
```
Explain the command ;

1. 'Alice%'- The percentage sif=gn is a wildcard character used with he LIKE 
    ator in SQL . It acts a placeholder that matches any sequence of characters including no characters at all . hence, it finds any students whose name start with alice followed by anything else eg ; Alice C Kimani .

### 2 How many students are from Mombasa (count_id=1) county?

To see all the counties 

```bash
SELECT * FROM county;
```
To see those students in Mombasa 

```bash
SELECT COUNT(*) FROM student WHERE county_id = 1;
```
Expected Output ; 

```bash
 count 
-------
    47
(1 row)
```
To display the contents of the output ; 

```bash
SELECT * FROM student WHERE county_id = 1;
```
### 3. How many students are from each of the counties?

* Getting the count for each county 

```bash
SELECT county_id, COUNT(*) as student_count FROM student GROUP BY county_id;
```
Explaining the command ; 
1. county-id is the table targeted

2. COUNT(*) Tells the database to count all the number of rows

3. as student_count - it specifies what we are counting without it , it just mentions count 

4. GROUP BY county_id - It tells the database to split the students into separate groups based on theor county and count each group individually 

Expected Output ; 

```bash
 county_id | student_count 
-----------+---------------
        42 |            44
        29 |            44
         4 |            53
        34 |            36
        41 |            57
        46 |            51
        40 |            56
        43 |            42
        32 |            53
         7 |            32
         9 |            46
        10 |            49
        35 |            49
        45 |            58
        38 |            55
        15 |            59
         6 |            48
        26 |            38
        12 |            62
        39 |            42
        24 |            50
        19 |            59
        36 |            57
        25 |            72
```

* Hence , county_id 42 has 44 students registered

### 4. Write a query that averages the scores of each student.

* Using the student_subject table 

```bash
SELECT student_id, ROUND(CAST(float8(AVG(score)) as numeric),4) as ave_score FROM student_subject GROUP BY student_id;
```
Explaining the command;

1. FROM student_subject: This tells the database to look inside your student_subject table where all the individual exam marks are stored.

2. GROUP BY student_id: This splits the rows into bundles. If a student took 5 subjects, all 5 of their score rows are bundled together into one group for that specific student.

3. AVG(score): This is the actual math. It adds up all the scores in a student's bundle and divides by the number of subjects they took to find the average.

4. float8(...): This ensures the data is treated as a double-precision decimal number.

5. CAST(... as numeric): PostgreSQL cannot directly round standard computer decimals (float8) to a specific number of decimal places. We must change (or "cast") the data type into a precise mathematical numeric type first.

6. ROUND(..., 4): Now that the number is a numeric type, this function rounds the average score so it shows exactly 4 digits after the decimal point (e.g., 74.3333).

7. as ave_score: This gives the final calculated column a clean, readable header name: ave_score.

Expected Output ;

```bash
student_id | ave_score 
------------+-----------
       2850 |   73.4476
       1798 |   62.1486
       1489 |   57.0946
       2335 |   66.1066
       1269 |   69.6290
       1560 |   65.3539
       2574 |   87.0797
       1898 |   97.5609
       2425 |   65.8818
       2080 |   62.8101
       2614 |   61.4030
       2520 |   60.7080
       2128 |   80.7992
       2466 |   59.7167
       2196 |   61.3705
       1750 |   92.8995
       1136 |   55.9914
       1831 |   81.1776
       1003 |   90.8078
       1331 |   63.3173
       2784 |   70.4704
       1552 |   59.9305
       1589 |   66.8528
       1493 |   91.1662
```

To see display the student_id 


```bash
SELECT * FROM student_subject LIMIT 5;
```
Expected Output ; 

```bash
student_id | subject_id |  score  
------------+------------+---------
       1001 |          1 | 80.4028
       1001 |          2 | 90.1712
       1001 |          3 | 74.7042
       1001 |          4 |  80.237
       1001 |          5 | 75.9394
(5 rows)
```

To display one student alone 

```bash
SELECT student_id, ROUND(CAST(float8(AVG(score)) as numeric),4) as ave_score FROM student_subject WHERE student_id = 1001 GROUP BY student_id;
```
Expected Output ; 

```bash
 student_id | ave_score 
------------+-----------
       1001 |   80.5191
(1 row)
```

### 5. Do a select query where you show the . after the middle initial eg. Amber C Kimani should be displayed as Amber C. Kimani etc.

To display the name initial format first ;

```bash
SELECT name FROM student LIMIT 10;
```
Expected Output ; 

```bash
     name       
-----------------
 Amber C Atieno
 Amber C Chacha
 Amber C Idris
 Amber C Kamau
 Amber C Kimani
 Amber C Kiptoo
 Amber C Maribe
 Amber C Maxx
 Amber C Mulanga
 Amber C Mwangi
(10 rows)
```
Now replacing with a period (.)

```bash
SELECT name, REGEXP_REPLACE(name, ' ([A-Z]) ', ' \1. ') AS formatted_name FROM student;
```
Explaining the command ;

1. REGEXP_REPLACE function. This function looks for a pattern where a single uppercase letter sits between two spaces, and adds a period to it.

2. ' ([A-Z]) ': This searches for a pattern containing a space, followed by any single capital letter from A to Z, followed by another space.

3. ' \1. ': The \1 grabs whatever letter was found in that spot, and adds a period right next to it, keeping the spaces intact.

Expected Output ; 


```bash
      name         |    formatted_name     
----------------------+-----------------------
 Amber C Atieno       | Amber C. Atieno
 Amber C Chacha       | Amber C. Chacha
 Amber C Idris        | Amber C. Idris
 Amber C Kamau        | Amber C. Kamau
 Amber C Kimani       | Amber C. Kimani
 Amber C Kiptoo       | Amber C. Kiptoo
 Amber C Maribe       | Amber C. Maribe
 Amber C Maxx         | Amber C. Maxx
 Amber C Mulanga      | Amber C. Mulanga
 Amber C Mwangi       | Amber C. Mwangi
 Amber C Nuru         | Amber C. Nuru
 Amber C Otieno       | Amber C. Otieno
 Amber C Ouma         | Amber C. Ouma
 Amber C Ratemo       | Amber C. Ratemo
 Amber C Wambugu      | Amber C. Wambugu
 Amber C Wanyonyi     | Amber C. Wanyonyi
 Amber C Yegon        | Amber C. Yegon
 Amber C Yebo         | Amber C. Yebo
 Amber K Atieno       | Amber K. Atieno
 Amber K Chacha       | Amber K. Chacha
 Amber K Idris        | Amber K. Idris
 Amber K Kamau        | Amber K. Kamau
```
### 6. Generate a select query that will show potential usernames for each student by combining first letter of first name, middle initial and lastname and last 4 digits of their phone number. eg.

Student with the following details: 

```bash
Amber C. Atieno 0783-627-886
```
Should generate such username

```bash
acatieno7886
```

QUERY USED 

* Displaying the initial  data 

```bash
SELECT name, phone FROM student LIMIT 10;
```
Expected Output ;

```bash
     name       |    phone     
-----------------+--------------
 Amber C Atieno  | 0720-729-029
 Amber C Chacha  | 0770-778-412
 Amber C Idris   | 0738-490-302
 Amber C Kamau   | 0795-796-371
 Amber C Kimani  | 0736-274-645
 Amber C Kiptoo  | 0741-981-287
 Amber C Maribe  | 0755-032-110
 Amber C Maxx    | 0730-247-011
 Amber C Mulanga | 0768-786-093
 Amber C Mwangi  | 0715-365-498
(10 rows)
```

* Adding username to the initial data 

Format we are following ; 

```bash
SELECT name, phone, LOWER(...) AS username FROM student;
```

```bash
SELECT name, phone, LOWER(
    LEFT(name, 1) || 
    SPLIT_PART(name, ' ', 2) || 
    SPLIT_PART(name, ' ', 3) || 
    RIGHT(REPLACE(phone, '-', ''), 4)
) AS username FROM student;
```

Explain the command ;

1. LOWER(...): Converts the final combined username into lowercase letters.

2. ||: This is the SQL symbol used to glue (concatenate) all these text pieces together.

3. RIGHT(..., 4): Grabs the last 4 digits of that cleaned phone number.

4. REPLACE(phone, '-', ''): Removes the dashes from the phone number so we are left with only numbers.

5. SPLIT_PART(name, ' ', 3): Splits the name by spaces and takes the third part, which is the last name (Atieno).

6. SPLIT_PART(name, ' ', 2): Splits the name by spaces and takes the second part, which is the middle initial (C).

7. LEFT(name, 1): Takes the first letter of the first name (A).


Expected Output ; 

```bash
         name         |    phone     |    username    
----------------------+--------------+----------------
 Amber C Atieno       | 0720-729-029 | acatieno9029
 Amber C Chacha       | 0770-778-412 | acchacha8412
 Amber C Idris        | 0738-490-302 | acidris0302
 Amber C Kamau        | 0795-796-371 | ackamau6371
 Amber C Kimani       | 0736-274-645 | ackimani4645
 Amber C Kiptoo       | 0741-981-287 | ackiptoo1287
 Amber C Maribe       | 0755-032-110 | acmaribe2110
 Amber C Maxx         | 0730-247-011 | acmaxx7011
 Amber C Mulanga      | 0768-786-093 | acmulanga6093
 Amber C Mwangi       | 0715-365-498 | acmwangi5498
 Amber C Nuru         | 0746-366-734 | acnuru6734
 Amber C Otieno       | 0728-213-014 | acotieno3014
 Amber C Ouma         | 0726-241-292 | acouma1292
 Amber C Ratemo       | 0714-481-051 | acratemo1051
 Amber C Wambugu      | 0767-568-323 | acwambugu8323
 Amber C Wanyonyi     | 0759-797-875 | acwanyonyi7875
 Amber C Yegon        | 0780-552-836 | acyegon2836
 Amber C Yebo         | 0751-668-707 | acyebo8707
 Amber K Atieno       | 0774-334-057 | akatieno4057
 Amber K Chacha       | 0719-987-980 | akchacha7980
 Amber K Idris        | 0771-246-224 | akidris6224
 Amber K Kamau        | 0791-084-676 | akkamau4676
```

# SECTION 2

# Queries involving Multiple Tables - utilizing SQL JOINS

### Display students with name Ami with an average score of 90% and above.

```bash
SELECT s.id, s.name, ROUND(CAST(float8(AVG(ss.score)) as numeric), 4) as ave_score 
FROM student s
JOIN student_subject ss ON s.id = ss.student_id
WHERE s.name LIKE 'Ami%'
GROUP BY s.id, s.name
HAVING AVG(ss.score) >= 90;
```
Explaining the command ;

### Line 1: SELECT s.id, s.name, ROUND(CAST(float8(AVG(ss.score)) as numeric), 4) as ave_score

1. s.id and s.name: Displays the student's ID number and full name from the student table.

2. ROUND(CAST(...)): This is the exact same rounding machine we used in Question 4. It calculates the average score for the student and rounds it to exactly 4 decimal places.

3. as ave_score: Gives that calculated column a clean header nickname.

### Line 2: FROM student s

1. The letter s: This is a table alias (a temporary nickname). Instead of typing student.id or student.name on every line, we just use s.

### Line 3: JOIN student_subject ss ON s.id = ss.student_id

1. JOIN student_subject ss: Brings in the grades table and gives it the short nickname ss.

2. ON s.id = ss.student_id: Explains the connection rule to PostgreSQL. It says: "Match rows where the id in the student table matches the student_id inside the grades table."

### Line 4: WHERE s.name LIKE 'Ami%'

1. It instantly throws away all students in the database whose names do not start with "Ami".

### Line 5: GROUP BY s.id, s.name

1. Collects all the individual subject rows for each remaining student and compresses them into a single bundle.

### Line 6: HAVING AVG(ss.score) >= 90;

1. Filters the final compressed bundles based on the math

2. While WHERE filters individual rows, HAVING filters aggregated groups. It looks at the calculated average for each "Ami" bundle and only allows it onto your screen if the average mark is 90 or higher.

Expected Output ;

```bash
id  |     name      | ave_score 
------+---------------+-----------
 1095 | Ami C Kimani  |   92.3541
 1123 | Ami K Wambugu |   93.0531
 1113 | Ami K Kimani  |   90.5584
 1177 | Ami W Wambugu |   93.6313
 1097 | Ami C Maribe  |   94.7201
 1169 | Ami W Maribe  |   90.8770
 1171 | Ami W Mulanga |   92.6217
 1138 | Ami L Otieno  |   92.6344
 1146 | Ami P Chacha  |   90.5688
 1168 | Ami W Kiptoo  |   92.3710
 1157 | Ami P Ouma    |   92.0410
(11 rows)
```

### 2 . What are the averages scores per county

* Three tables are joined together 

1. The county to find the county IDs and names 

2. Students table to find the students pesonal details hence knowing the specific counfty_id of the students

3. student_subject table to find the raw test marks of the students 

```bash
SELECT c.name AS county_name, ROUND(CAST(float8(AVG(ss.score)) as numeric), 4) as ave_score
FROM county c
JOIN student s ON c.id = s.county_id
JOIN student_subject ss ON s.id = ss.student_id
GROUP BY c.id, c.name
ORDER BY ave_score DESC;
```
Explain the command ; 
 
1. JOIN student s ON c.id = s.county_id: Links the county table (c) to the
   student table (s).

2. JOIN student_subject ss ON s.id = ss.student_id: Links those students to
   their scores (ss).

3. GROUP BY c.id, c.name: Groups all scores together by county so we
   calculate one average per county.

4. ORDER BY ave_score DESC(Descending order): Sorts the list from the highest average score to
   the lowest.

Expected Output ;

```bash
county_name | ave_score 
-------------+-----------
 Nyamira     |   78.8988
 Lamu        |   78.2919
 Isiolo      |   78.0714
 Tharaka     |   77.2446
 Mombasa     |   76.8075
 Tana        |   76.7975
 Kisumu      |   76.1957
 Kiambu      |   75.8939
 Trans       |   75.8708
 Wajir       |   75.8257
 Kericho     |   75.7992
 Garissa     |   75.7896
```

### 3. List all students from Turkana county. Display only the following fields: id, name and their school name.

* Here we need to join three tables since they are connected to each other

1. The STUDENT TABLE - to get the students ID and their NAME 

2. The COUNTY TABLE - to filter names from turukana 

3. The SCHOOL TABLE - to find the school the students are in 



```bash
SELECT s.id, s.name, sch.name AS school_name
FROM student s
JOIN county c ON s.county_id = c.id
JOIN school sch ON s.school_id = sch.id
WHERE c.name = 'Turkana';
```
Explaining the command ;

1. JOIN county c ON s.county_id = c.id: Connects the student to their county so we can check for 'Turkana'.

2. JOIN school sch ON s.school_id = sch.id: Connects the student to their school table so we can grab the
   shools actual name field (sch.name)

3. WHERE c.name = 'Turkana': Filters the rows so only students from Turkana appear on your screen.

Expected output ; 

```bash
id  |         name         |      school_name      
------+----------------------+-----------------------
 1026 | Amber K Maxx         | Kericho - Provincial
 1061 | Amber P Maribe       | Kitui - Homeschool
 1073 | Amber W Atieno       | Mandera - Private
 1081 | Amber W Mulanga      | Nyeri - Private
 1101 | Ami C Nuru           | Isiolo - National
 1127 | Ami L Atieno         | Baringo - Private
 1207 | Alice K Mulanga      | Busia - Private
 1235 | Alice P Atieno       | Nandi - District
 1284 | Beth C Ratemo        | Laikipia - Provincial
 1322 | Beth L Wanyonyi      | Kwale - Private
 1342 | Beth P Yebo          | Uasin - Provincial
 1370 | Conrad C Mwangi      | Kirinyaga - District
 1374 | Conrad C Ratemo      | Bungoma - Private
 1400 | Conrad L Kamau       | Bomet - Homeschool
 1429 | Conrad P Wambugu     | Nyeri - Provincial
 1446 | Conrad W Ratemo      | Elgeyo - Homeschool
 1460 | Edward C Mwangi      | Marsabit - Private
 1465 | Edward C Wambugu     | Kiambu - Homeschool
 1546 | Elizabeth C Kiptoo   | Marsabit - District
 1556 | Elizabeth C Wanyonyi | Kwale - Private
 1572 | Elizabeth K Ratemo   | Mandera - Private
 1635 | James C Kimani       | Elgeyo - National
 1645 | James C Wambugu      | Samburu - Homeschool
 1650 | James K Chacha       | Siaya - National
 1689 | James P Kimani       | Baringo - District
 1862 | Joanne L Wanyonyi    | Meru - Homeschool
 1924 | John K Kiptoo        | Machakos - National
 1972 | John P Yebo          | Tana - National
```
### 4. List the top students for each subject in the country, include their county name and school name.


```bash
SELECT ranked.subject_name, ranked.student_name, ranked.score, ranked.school_name, ranked.county_name
FROM (
    SELECT 
        sub.name AS subject_name,
        s.name AS student_name,
        ss.score,
        sch.name AS school_name,
        c.name AS county_name,
        ROW_NUMBER() OVER(PARTITION BY ss.subject_id ORDER BY ss.score DESC) as rank
    FROM student_subject ss
    JOIN student s ON ss.student_id = s.id
    JOIN subject sub ON ss.subject_id = sub.id
    JOIN school sch ON s.school_id = sch.id
    JOIN county c ON s.county_id = c.id
) ranked
WHERE ranked.rank = 1;
```

Expected Output ; 


```bash
subject_name |    student_name    |  score  |     school_name     | county_name 
--------------+--------------------+---------+---------------------+-------------
 Mathematics  | Joanne K Kiptoo    | 99.8083 | Nairobi - Private   | Nyamira
 English      | Joan K Kiptoo      | 99.9693 | Laikipia - District | Taita
 Swahili      | Martin P Otieno    | 99.9584 | Meru - District     | Laikipia
 Biology      | Elizabeth W Kimani | 99.9791 | Nakuru - Homeschool | Lamu
 Chemistry    | Beth L Wanyonyi    | 99.9964 | Kwale - Private     | Turkana
 Physics      | Joanne K Ratemo    | 99.8492 | Migori - District   | Kisii
 Geography    | Okello W Yegon     | 99.9702 | Lamu - Private      | Samburu
 History      | Yannis P Maxx      | 99.8125 | Narok - District    | Samburu
 Agriculture  | Johnson L Wanyonyi | 99.9131 | Kwale - Homeschool  | Nandi
(9 rows)
```
### 5. List the top 10 students in the country. Use the average score of all their subjects. Include a field that shows their ranks ie 1 to 10. Additionally, list the county and school name.

```bash
SELECT 
    RANK() OVER(ORDER BY AVG(ss.score) DESC) as student_rank,
    s.name AS student_name, 
    ROUND(CAST(float8(AVG(ss.score)) as numeric), 4) as ave_score,
    c.name AS county_name, 
    sch.name AS school_name
FROM student s
JOIN student_subject ss ON s.id = ss.student_id
JOIN county c ON s.county_id = c.id
JOIN school sch ON s.school_id = sch.id
GROUP BY s.id, s.name, c.name, sch.name
ORDER BY ave_score DESC
LIMIT 10;
```
Expected output ;

```bash
 student_rank |   student_name    | ave_score | county_name |     school_name      
--------------+-------------------+-----------+-------------+----------------------
            1 | Joanne W Wanyonyi |   97.5609 | Bomet       | Elgeyo - National
            2 | Joanne C Yegon    |   96.6643 | Meru        | Tana - District
            3 | John C Maribe     |   96.3209 | Machakos    | Migori - Private
            4 | Yannis L Ratemo   |   96.0123 | Lamu        | Nyamira - Provincial
            5 | Alice W Kiptoo    |   95.9981 | Migori      | Kilifi - Homeschool
            6 | Mary C Atieno     |   95.9980 | Nyamira     | Nyeri - Private
            7 | James L Mwangi    |   95.9386 | Meru        | Bungoma - National
            8 | Beth K Wanyonyi   |   95.8104 | Isiolo      | Kericho - Provincial
            9 | Liz P Yegon       |   95.7570 | Wajir       | Turkana - National
           10 | Edward C Otieno   |   95.7250 | Busia       | Kirinyaga - National
(10 rows)
```
### 5b . List a column with the county name and another county as well 

```bash
SELECT 
    s.id, 
    s.name, 
    c.name AS county_name,
    sch.name AS school_name 
FROM student s 
JOIN county c ON s.county_id = c.id 
JOIN school sch ON s.school_id = sch.id 
WHERE c.name IN ('Turkana', 'Lamu');
```
Expected Output ; 
```bash
id  |         name         | county_name |      school_name       
------+----------------------+-------------+------------------------
 1026 | Amber K Maxx         | Turkana     | Kericho - Provincial
 1061 | Amber P Maribe       | Turkana     | Kitui - Homeschool
 1062 | Amber P Maxx         | Lamu        | Nyamira - National
 1073 | Amber W Atieno       | Turkana     | Mandera - Private
 1081 | Amber W Mulanga      | Turkana     | Nyeri - Private
 1093 | Ami C Idris          | Lamu        | Tharaka - Provincial
 1101 | Ami C Nuru           | Turkana     | Isiolo - National
 1127 | Ami L Atieno         | Turkana     | Baringo - Private
 1170 | Ami W Maxx           | Lamu        | Kericho - Private
 1173 | Ami W Nuru           | Lamu        | Isiolo - National
 1174 | Ami W Otieno         | Lamu        | Embu - Provincial
 1206 | Alice K Maxx         | Lamu        | Nyandarua - Provincial
 1207 | Alice K Mulanga      | Turkana     | Busia - Private
 1214 | Alice K Wanyonyi     | Lamu        | Elgeyo - National
 1218 | Alice L Chacha       | Lamu        | Busia - Homeschool
 1221 | Alice L Kimani       | Lamu        | Samburu - National
 1235 | Alice P Atieno       | Turkana     | Nandi - District
 1284 | Beth C Ratemo        | Turkana     | Laikipia - Provincial
 1322 | Beth L Wanyonyi      | Turkana     | Kwale - Private
 1324 | Beth L Yebo          | Lamu        | Samburu - Homeschool
 1342 | Beth P Yebo          | Turkana     | Uasin - Provincial
 1351 | Beth W Mulanga       | Lamu        | Kirinyaga - Homeschool
 1370 | Conrad C Mwangi      | Turkana     | Kirinyaga - District
 1374 | Conrad C Ratemo      | Turkana     | Bungoma - Private
 1400 | Conrad L Kamau       | Turkana     | Bomet - Homeschool
 1429 | Conrad P Wambugu     | Turkana     | Nyeri - Provincial
 1444 | Conrad W Otieno      | Lamu        | Embu - Homeschool
 1446 | Conrad W Ratemo      | Turkana     | Elgeyo - Homeschool
 1457 | Edward C Maribe      | Lamu        | Kericho - District
 1460 | Edward C Mwangi      | Turkana     | Marsabit - Private
 1465 | Edward C Wambugu     | Turkana     | Kiambu - Homeschool
 1475 | Edward K Maribe      | Lamu        | Garissa - District
 1490 | Edward L Kamau       | Lamu        | Kericho - Provincial
 1546 | Elizabeth C Kiptoo   | Turkana     | Marsabit - District
 1556 | Elizabeth C Wanyonyi | Turkana     | Kwale - Private
 1572 | Elizabeth K Ratemo   | Turkana     | Mandera - Private
 1617 | Elizabeth W Kimani   | Lamu        | Nakuru - Homeschool
 1624 | Elizabeth W Otieno   | Lamu        | Meru - Homeschool
 1635 | James C Kimani       | Turkana     | Elgeyo - National
 1645 | James C Wambugu      | Turkana     | Samburu - Homeschool
 1650 | James K Chacha       | Turkana     | Siaya - National
 1651 | James K Idris        | Lamu        | Laikipia - National
 1688 | James P Kamau        | Lamu        | Nyamira - National
 1689 | James P Kimani       | Turkana     | Baringo - District
 1703 | James W Atieno       | Lamu        | Kajiado - Homeschool
 1738 | Joan C Yebo          | Lamu        | Bungoma - National
 1746 | Joan K Maxx          | Lamu        | Machakos - District
 1853 | Joanne L Maribe      | Lamu        | Kakamega - National
 1862 | Joanne L Wanyonyi    | Turkana     | Meru - Homeschool
 1917 | John C Yegon         | Lamu        | Nyeri - Homeschool
```

### 6. List the top schools (school name, total number of students in each school and county name) based on type/category ie top school:

* Homeschool

* National

* Provincial

* District

* Private

* #### To know the categories are named in the school table 

```bash
\d school
```
Expected output ; 

```bash
                    Table "public.school"
  Column   |          Type          | Collation | Nullable | Default 
-----------+------------------------+-----------+----------+---------
 id        | integer                |           | not null | 
 county_id | integer                |           |          | 
 name      | character varying(255) |           |          | 
Indexes:
    "school_pkey" PRIMARY KEY, btree (id)
Foreign-key constraints:
    "school_county_id_fkey" FOREIGN KEY (county_id) REFERENCES county(id)
Referenced by:
    TABLE "student" CONSTRAINT "student_school_id_fkey" FOREIGN KEY (school_id) REFERENCES school(id)
```

```bash
 SELECT 
    sch.name AS school_name,
    COUNT(s.id) AS total_students,
    c.name AS county_name,
    CASE 
        WHEN sch.name ILIKE '%Homeschool%' THEN 'Homeschool'
        WHEN sch.name ILIKE '%National%' THEN 'National'
        WHEN sch.name ILIKE '%Provincial%' THEN 'Provincial'
        WHEN sch.name ILIKE '%District%' THEN 'District'
        WHEN sch.name ILIKE '%Private%' THEN 'Private'
        ELSE 'Other'
    END AS school_category
FROM school sch
JOIN student s ON sch.id = s.school_id
JOIN county c ON sch.county_id = c.id
GROUP BY sch.id, sch.name, c.name
ORDER BY school_category, total_students DESC;
```
Explain the Output ; 

1. ILIKE: This is a case-insensitive search. It matches keywords regardless of whether they are uppercase or lowercase (e.g., %National% will match "National High", "national academy", or "NATIONAL SCHOOL").


Expected Output ; 

```bash
school_name       | total_students | county_name | school_category 
------------------------+----------------+-------------+-----------------
 Kisumu - District      |             19 | Kisumu      | District
 Busia - District       |             18 | Busia       | District
 Bungoma - District     |             16 | Bungoma     | District
 Meru - District        |             16 | Meru        | District
 Wajir - District       |             16 | Wajir       | District
 Machakos - District    |             15 | Machakos    | District
 Bomet - District       |             14 | Bomet       | District
 Lamu - District        |             14 | Lamu        | District
 Murang'a - District    |             14 | Murang'a    | District
 Kakamega - District    |             13 | Kakamega    | District
 Marsabit - District    |             13 | Marsabit    | District
 Kiambu - District      |             12 | Kiambu      | District
 Siaya - District       |             12 | Siaya       | District
 Isiolo - District      |             12 | Isiolo      | District
 Homa - District        |             12 | Homa        | District
 Baringo - District     |             12 | Baringo     | District
 Garissa - District     |             11 | Garissa     | District
 Nakuru - District      |             11 | Nakuru      | District
 Mombasa - District     |             11 | Mombasa     | District
 Migori - District      |             11 | Migori      | District
```

### 7. Similar to above query, list the top student from each school type.

```bash
SELECT school_top.school_name, school_top.student_name, school_top.ave_score
FROM (
    SELECT 
        sch.name AS school_name,
        s.name AS student_name,
        ROUND(CAST(float8(AVG(ss.score)) as numeric), 4) as ave_score,
        ROW_NUMBER() OVER(PARTITION BY s.school_id ORDER BY AVG(ss.score) DESC) as rank
    FROM student s
    JOIN student_subject ss ON s.id = ss.student_id
    JOIN school sch ON s.school_id = sch.id
    GROUP BY sch.id, sch.name, s.id, s.name
) school_top
WHERE school_top.rank = 1
ORDER BY school_top.school_name;
```
Expected Output ; 

```bash
  school_name       |    student_name     | ave_score 
------------------------+---------------------+-----------
 Baringo - District     | Mary L Kamau        |   93.4816
 Baringo - Homeschool   | Yannis K Mulanga    |   94.1873
 Baringo - National     | Conrad K Kiptoo     |   91.1722
 Baringo - Private      | Johnson L Chacha    |   85.9539
 Baringo - Provincial   | Ami W Wambugu       |   93.6313
 Bomet - District       | John W Kimani       |   90.6886
 Bomet - Homeschool     | Conrad L Kamau      |   93.3883
 Bomet - National       | Elizabeth W Kamau   |   92.7977
 Bomet - Private        | John K Yegon        |   92.2995
 Bomet - Provincial     | James P Nuru        |   92.2629
 Bungoma - District     | Liz K Atieno        |   94.4172
 Bungoma - Homeschool   | Martin W Mwangi     |   90.8181
 Bungoma - National     | James L Mwangi      |   95.9386
 Bungoma - Private      | Liz K Maxx          |   92.5910
 Bungoma - Provincial   | Conrad W Ouma       |   93.7699
 Busia - District       | Ami C Kimani        |   92.3541
 Busia - Homeschool     | Beth W Kamau        |   93.8105
 Busia - National       | Maryanne P Ratemo   |   78.0484
 Busia - Private        | Ami W Kiptoo        |   92.3710
 Busia - Provincial     | Conrad K Atieno     |   95.2727
```

# Update Data Questions

#### * The following involve updating records, tables, or deleting records. Make use of database transactions to be safe.
 
# 1. Delete all records for students with the name Joan and be careful not to delete Joanne

## Step 1 : Display all the students going by the name joan 

```bash
SELECT id, name FROM student WHERE name LIKE 'Joan %' OR name = 'Joan';
```

## Step 2 : Start the Transaction 

```bash
BEGIN;
```

## Step 2 : Delete the name Joan scores first

```bash
DELETE FROM student_subject WHERE student_id IN (SELECT id FROM student WHERE name LIKE 'Joan %' OR name = 'Joan');
```
## Step 3 :  Delete Joan's student profiles next

```bash
DELETE FROM student WHERE name LIKE 'Joan %' OR name = 'Joan';
```
## Step 4 : To verify Joan has been deleted

```bash
SELECT COUNT(*) FROM student WHERE name LIKE 'Joan %' OR name = 'Joan';
```
## Step 5 : Verify we havent deleted Joanne 

```bash
SELECT COUNT(*) FROM student WHERE name LIKE 'Joanne%';
```
# 2. Update all county names to UPPERCASE.


## Step 1 : Check the county names format 

```bash
SELECT * FROM county;
```
## Step 2 : Start a new transaction 

```bash
BEGIN;
```
## Step 3 : Change them to uppercase from lower case

```bash
UPDATE county SET name = UPPER(name);
```
## Step 4 : Verify the changes 

```bash
SELECT name FROM county LIMIT 5;
```
# 4. Update all phone numbers so that they change from format 0707-155-302 to format 254707155302

## Step 1 : To verify the initial phone number format

```bash
SELECT phone FROM student LIMIT 5;
```
## Step 2 : Start the Transaction 

```bash
BEGIN;
```
## Step 3 : Format the original phone number to another formation 

```bash
UPDATE student 
SET phone = '254' || SUBSTRING(REPLACE(phone, '-', '') FROM 2);
```
## Step 4 : To verify the changes 

```bash
SELECT phone FROM student LIMIT 5;
```
# 5. Update records for students from TRANS, THARAKA and WEST counties so that they read TRANS-NZOIA, THARAKA-NITHI and WEST-POKOT respectively.

## Step 1 : To verify the format before the changes 

```bash
SELECT name FROM county WHERE name LIKE 'TRANS%' OR name LIKE 'THARAKA%' OR name LIKE 'WEST%';
```
## Step 2 : Start the transaction

```bash
BEGIN;
```
## Step 3 : Update the county name 

```bash
UPDATE county SET name = 'TRANS-NZOIA' WHERE name = 'TRANS';
UPDATE county SET name = 'THARAKA-NITHI' WHERE name = 'THARAKA';
UPDATE county SET name = 'WEST-POKOT' WHERE name = 'WEST';
```
## Step 4 : Verify the changes 

```bash
SELECT name FROM county WHERE name LIKE 'TRANS%' OR name LIKE 'THARAKA%' OR name LIKE 'WEST%';
```
# 6. Update all students with ALICE .... to ALLISA.

## Step 1 . Verify their is a student called Alice

```bash
SELECT name FROM student WHERE name ILIKE 'Alice%';
```
## Step 2. Start the transaction 

```bash
BEGIN;
```
## Step 3. Update the name from Alice to ALLISA

```bash
UPDATE student 
SET name = REGEXP_REPLACE(name, '^Alice', 'ALLISA', 'i');
```
## Step 4. Verify the changes 

```bash
SELECT name FROM student WHERE name LIKE 'ALLISA%' LIMIT 5;
```
# 7. Write an SQL query where that shows the letter grade using the following scale - If a student's average score is between:

* 95 and 100 then the grade => 'A'

* 90 and 95 then the grade => 'A-'

* 85 and 90 then the grade => 'B+'

* 80 and 85 then the grade => 'B'

* 75 and 80 then the grade => 'B-'

* 70 and 75 then the grade => 'C+'


* 60 and 65 then the grade => 'C-'

* 55 and 60 then the grade => 'D+'

* 50 and 55 then the grade => 'D'

* 49 and below, the grade => 'FAIL'

## Step 1 : The query Structure

```bash
SELECT 
    s.id, 
    s.name, 
    ROUND(CAST(float8(AVG(ss.score)) as numeric), 0) as score,
    CASE 
        WHEN AVG(ss.score) >= 95 AND AVG(ss.score) <= 100 THEN 'A'
        WHEN AVG(ss.score) >= 90 AND AVG(ss.score) < 95   THEN 'A-'
        WHEN AVG(ss.score) >= 85 AND AVG(ss.score) < 90   THEN 'B+'
        WHEN AVG(ss.score) >= 80 AND AVG(ss.score) < 85   THEN 'B'
        WHEN AVG(ss.score) >= 75 AND AVG(ss.score) < 80   THEN 'B-'
        WHEN AVG(ss.score) >= 70 AND AVG(ss.score) < 75   THEN 'C+'
        WHEN AVG(ss.score) >= 65 AND AVG(ss.score) < 70   THEN 'C'
        WHEN AVG(ss.score) >= 60 AND AVG(ss.score) < 65   THEN 'C-'
        WHEN AVG(ss.score) >= 55 AND AVG(ss.score) < 60   THEN 'D+'
        WHEN AVG(ss.score) >= 50 AND AVG(ss.score) < 55   THEN 'D'
        ELSE 'FAIL'
    END AS grade
FROM student s
JOIN student_subject ss ON s.id = ss.student_id
GROUP BY s.id, s.name
ORDER BY s.id ASC;
```

Expected Output ;

```bash
  id  |         name         | score | grade 
------+----------------------+-------+-------
 1001 | Amber C Atieno       |    81 | B
 1002 | Amber C Chacha       |    81 | B
 1003 | Amber C Idris        |    91 | A-
 1004 | Amber C Kamau        |    80 | B-
 1005 | Amber C Kimani       |    86 | B+
 1006 | Amber C Kiptoo       |    62 | C-
 1007 | Amber C Maribe       |    63 | C-
 1008 | Amber C Maxx         |    77 | B-
 1009 | Amber C Mulanga      |    86 | B+
 1010 | Amber C Mwangi       |    82 | B
 1011 | Amber C Nuru         |    92 | A-
 1012 | Amber C Otieno       |    71 | C+
 1013 | Amber C Ouma         |    81 | B
 1014 | Amber C Ratemo       |    56 | D+
 1015 | Amber C Wambugu      |    56 | D+
 1016 | Amber C Wanyonyi     |    82 | B
 1017 | Amber C Yegon        |    76 | B-
 1018 | Amber C Yebo         |    70 | C
 1019 | Amber K Atieno       |    60 | D+
 1020 | Amber K Chacha       |    93 | A-
```

# Securing PostgreSQL Databases

# 1. What type of authentication did we utilize in the above user creation ie given that we have matched the database user to the Linux system username?

* Peer Authentication 

#### Why we use it 

* No Double Passwords: You only log into Linux.

* Automatic Trust: PostgreSQL trusts the Linux kernel identity.

* High Security: No passwords pass over local networks.


* # Peer $ Ident 

| Feature | Peer Authentication | Ident Authentication |
| :--- | :--- | :--- |
| **Network Scope** | Local only (via Unix domain sockets). | Remote or network-based (via TCP/IP). |
| **How it Works** | Database asks the OS for the username of the process making the connection. | Database contacts an external `identd` daemon running on the client machine. |
| **Source of Trust** | Trusted local kernel/operating system. | Trusted remote client machine (vulnerable if client is compromised). |
| **Configuration Entry** | Specified as `peer` in `pg_hba.conf`. | Specified as `ident` in `pg_hba.conf`, usually mapping to an `ident` map file. |
| **Spoofing Risk** | Extremely low (requires root/kernel level exploit on the host). | High (if an attacker controls the client machine, they can fake the ident response). |

* # md5 vs scram-sha-256
Upgrading password encryption from MD5 to SCRAM -SHA-256

  * md5 has been used for years but has some potential security flaws e.g. collision attacks.

  * It is a password  authentication methods 

    * scram-sha-256

* Salted Challenge Response Authentication Mechanism , is a highly secure, modern 
  authentication protocol used to verify user identities over networks without exposing plaintext passwords or vulnerable hashes. It is the default authentication standard for modern systems like PostgreSQL and MongoDB.

## Differences in md5 and scram


| Feature | MD5 Password Method | SCRAM-SHA-256 Method |
| :--- | :--- | :--- |
| **Security Status** | Broken and unsafe |  Ultra-secure standard |
| **Output Size** | 128 bits (32 characters) | 256 bits (64 characters) |
| **Salting** | No salt (Same password = same hash) |  Built-in salt (Same password = unique hash) |
| **Network Safety** | Sends the hash over the wire |  Uses a secure cryptographic handshake |
| **Cracking Risk** | High (Vulnerable to Rainbow Tables) | Zero (Protected against guessing attacks) |

## Step 1 : Edit postgresql

```bash
sudo vi /etc/postgresql/17/main/postgresql.conf
```
Press / to locate the exact line ;

Change it from ; 

```bash
#password_encryption = md5		# md5 or scram-sha-256
```
To ;

```bash
password_encryption = scram-sha-256
```
## Step 2 : Updating The network authentication (pg_hba.conf)

* To aquire this new encryption method when the users try to log in via local network connections . We do this in the host based authentification file pg_hba.conf

```bash
sudo vi /etc/postgresql/17/main/pg_hba.conf
```
press / to get you to the exact line 

Change ; 

```bash
host    all             all             127.0.0.1/32            md5
```

To ;

```bash
host    all             all             127.0.0.1/32            scram-sha-256
```

## Step 3 : Restart Postgresql 

```bash
sudo service postgresql restart
```
* This shuts down the database engine cleanly and starts it back up, forcing it to load your new SCRAM-SHA-256 security rules into memory.

## Step 4 : Verify the Global Encryption 

* We log in to the database and check the status of the global password encryption setting 

* Log in to the Postgresql as the superuser 


```bash
sudo -u postgres psql
```

Once we see ; postgres=# prompt

```bash
SHOW password_encryption;
```
* This explicitly asks the active database engine what encryption method it will apply to any new or updated passwords. It should return scram-sha-256.

Expected Output ; 


```bash
psql (17.10 (Debian 17.10-0+deb13u1))
Type "help" for help.

postgres=# SHOW password_encryption;
 password_encryption 
---------------------
 scram-sha-256
(1 row)
```
## step 5 : Check user roles and encryption 

```bash
SELECT rolpassword, rolname FROM pg_authid;
```

Expected Output ; 


```bash
                                                             rolpassword                                                              |           rolname           
---------------------------------------------------------------------------------------------------------------------------------------+-----------------------------
                                                                                                                                       | postgres
                                                                                                                                       | pg_database_owner
                                                                                                                                       | pg_read_all_data
                                                                                                                                       | pg_write_all_data
                                                                                                                                       | pg_monitor
                                                                                                                                       | pg_read_all_settings
                                                                                                                                       | pg_read_all_stats
                                                                                                                                       | pg_stat_scan_tables
                                                                                                                                       | pg_read_server_files
                                                                                                                                       | pg_write_server_files
                                                                                                                                       | pg_execute_server_program
                                                                                                                                       | pg_signal_backend
                                                                                                                                       | pg_checkpoint
                                                                                                                                       | pg_maintain
                                                                                                                                       | pg_use_reserved_connections
                                                                                                                                       | pg_create_subscription
 SCRAM-SHA-256$4096:AIS2GlB4MK75Ko3cjG7Shw==$4hh2b8rdATAPQFqqSmFVBYs73yaQeF+i3GsOCen6eOQ=:RBBeZ19/MWEMygZjBbiFAv/XRKYjORv9I0BdPSzFHVQ= | gwekesa
 SCRAM-SHA-256$4096:wtj6sSoUnBLYzS0+jTSUJw==$9XtjIhyCY1Zl2Kz6lkUP+vFE1kW8l0Ie0oMuaKvuu/8=:Pg7JntySBznwIHAx3qcggMuNQRG92911hHOUPxuxD5s= | pkinoti
(18 rows)
```

* #### This output means that we have successfully upgraded our users accounts to a new security standard .

* #### The system roles have empty passwords , the postgres , pg_database have blank spaces next to them this means they do not have a network password set . They rely fully on the Peer authentication .

* #### 4096 This represents the iteration count. The algorithm runs 4,000+ times to scramble the password, making it incredibly slow and difficult for hackers to guess via brute force.


* # Troubleshooting Permission Denied Errors

* After creating the database user dont automatically mean they can interact with every database or table because they are locked down tightly . Henc , we use GRANT statements t solve permission issues 

## Step 1 : log into the database 

```bash
sudo -u postgres psql
```

## Step 2 : Connect to the Exam Database

```bash
\c exam
```
## Step 3 : Grant the permission 

* Exam database

```bash
GRANT ALL PRIVILEGES ON DATABASE exam TO pkinoti;
```
* Connection privelege to the exam database 

```bash
GRANT CONNECT ON DATABASE exam TO pkinoti;
```
* Privelege for the exam database to ; 

```bash
GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA public TO pkinoti;
```

# Installing and using pgAdmin

* pgAdmin is a helpful tool to easily run queries on the fly similar to psql but can come in handy if you:

## Step 1 : Install pgadmin

```bash
curl -fsS https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo gpg --dearmor -o /usr/share/keyrings/packages-pgadmin-org.gpg
sudo sh -c 'echo "deb [signed-by=/usr/share/keyrings/packages-pgadmin-org.gpg] https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'
sudo apt install pgadmin4
```
## Step 2 : edit the pg_hba.conf

* You might need to edit your local pg_hba.conf file e.g. sudo vi /etc/postgresql/17/main/pg_hba.conf and add the following line (right below the line # IPv4 local connections: line): 

```bash
host    all             all             127.0.0.1/32            trust
```
## Step 3 : Now uninstall and install it again 

```bash
sudo apt-get purge --auto-remove pgadmin4 pgadmin4-desktop pgadmin4-web pgadmin4-server -y
```
* purge: Tells the system to delete not just the application, but all of its configuration files too.

* --auto-remove: Cleans up leftover background software packages that were only installed to support pgAdmin

* -y: Automatically answers "yes" to confirmation prompts.

## Step 4 :  Delete left-over directories

```bash
sudo rm -rf /var/lib/pgadmin /var/log/pgadmin /etc/pgadmin
```

* /var/lib/pgadmin & /var/log/pgadmin: Removes the old configuration databases and event log files.

## Step 5 : Download the official GPG security key

* The left side downloads the security key from the internet, and the right side converts and saves it securely onto your computer.

```bash
curl -fsS https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo gpg --dearmor -o /usr/share/keyrings/packages-pgadmin-org.gpg
```
Explain the command ; 

* Downloading the Public Key

curl -fsS https://www.pgadmin.org/static/packages_pgadmin_org.pub

1. curl: A command-line tool used to transfer data to or from a network server (essentially a terminal-based web browser).

2. f (Fail silently): If the website is down or the link is broken, this prevents the terminal from outputting a messy HTML error page.

3. -s (Silent mode): Hides the download progress bar, keeping your terminal screen completely clean.

4. -S (Show error): If the download fails completely, this forces curl to show a single line explaining why 

5. https://www.pgadmin.org/...: The official web address where pgAdmin hosts their public cryptographic security key.

* The Connector (The Pipe)

1. | (Pipe) It takes the text output from the first command (curl) and injects it directly as the input for the second command (gpg).

* Converting and Saving the Key

sudo gpg --dearmor -o /usr/share/keyrings/packages-pgadmin-org.gpg

1. sudo: Grants root (administrative) permissions 

2. gpg: GNU Privacy Guard. This is the built-in encryption engine Linux uses to verify digital signatures

3. --dearmor: The key downloaded from the website is written in plain text format 

4. o (Output): Tells the command where to save the newly converted binary file.

5. /usr/share/keyrings/packages-pgadmin-org.gpg: The exact secure folder path where Linux stores trusted security keys


## Step 6 : Create the repository list file and update

* Downloaded address to your system records and refresh your application logs

* It uses sh -c to run them all with administrative power (sudo)

* uses echo to write a text configuration

* uses && to trigger a system update.


```bash
sudo sh -c 'echo "deb [signed-by=/usr/share/keyrings/packages-pgadmin-org.gpg] https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'
```

Explain the command :

1. sudo: Grants root (administrative) privileges

2. sh -c: Opens a temporary background shell processor to execute the long string of commands wrapped inside the single quotes '

* echo "deb [signed-by=/usr/share/keyrings/packages-pgadmin-org.gpg] https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" 

1. echo: A basic terminal command that prints out whatever text comes after it.

2. deb: Tells your system that this download source hosts pre-compiled, ready-to-install Linux packages.

3. [signed-by=...]: A security rule forcing Linux to use that specific GPG security key to verify the pgAdmin packages before installing them.

4. https://ftp.postgresql.org...: The official web server URL where the pgAdmin software files are stored.

5. $(lsb_release -cs): A dynamic variable. When executed, your terminal replaces this text with your exact Linux version codename (for example: bookworm) This ensures your computer pulls software designed specifically for your operating system version.

* Creating the Source List File

1. The "redirection" operator > . Instead of printing the echo text onto your screen, this arrow forces the text directly into a file.

2. /etc/apt/sources.list.d/pgadmin4.list: The exact folder and file path where Linux stores third-party software download addresses.

* The Safety Chain and Index Refresh - && apt update

1. &&: A logical operator meaning "AND". It tells the terminal: "Only run the next command if the first part finished successfully without any errors."

2. apt update: Refreshes your local software catalog. Now that you have added the new address file, this command tells your machine to scan that specific pgAdmin URL and download a fresh list of available packages, making pgadmin4 ready to install.

## Step 7 : Install the pgAdmin package

```bash
sudo apt install pgadmin4 -y
```

* pgadmin4: This acts as a combined bundle package that automatically reinstalls both the standalone desktop window interface and the web server components.


## Step 8 : Initialize the web server interface

* configure your browser login settings 

```bash
sudo /usr/pgadmin4/bin/setup-web.sh
```
* This runs the official setup script which builds a new underlying storage database, prompts you for a clean login email/password, and automatically wires up the Apache HTTP web server redirect link.

What has been done in short ; 

1. Removed Old Files: Completely erased the previous pgAdmin 4 software packages and their background configuration records from your system.

2. Downloaded Security Key: Fetched the official pgAdmin public encryption key (packages-pgadmin-org.pub) directly from their server.

3. ecured the Key: Converted that plain-text security key into a binary format and saved it into your system’s trusted keyring folder.

4. Registered the Repository: Created a new dedicated software source file (pgadmin4.list) so your computer knows the exact web address to find pgAdmin.

5. Updated System Index: Refreshed your local package manager catalog (apt update) to recognize the newly added pgAdmin download path.

6. Reinstalled pgAdmin: Successfully deployed a fresh instance of the full pgadmin4 desktop and web bundle onto your machine.

7. Configured Web Server: Initialized the web application, created a new administrative login (purity.jxcobs@gmail.com), and successfully restarted the Apache web server on your browser port.


# Creating a PostgreSql Database 

## Step 1 : Access your initial traccar 

```bash
ssh pkinoti@test.traccar.quatrixglobal.com
```
## Step 2 : Access the postgres 

```bash
sudo -u postgres psql
```
## Step 3 :  Create Your Account

```bash
CREATE ROLE pkinoti WITH LOGIN SUPERUSER PASSWORD 'kinoti1234';
```
## Step 4 : Verify the Account

```bash
\du
```
## Step 5 : Exit the shell 

```bash
\q
```
# Accessing a Remote Database (Traccar)

* You will need to access the test.traccar database for the following questions. We will access the test.traccar database using ssh tunneling as outlined below: Create an ssh tunnel to test.traccar server

## Step 1 : Setting up the SSH Tunnel

```bash
ssh -f -o ExitOnForwardFailure=yes -L 63334:localhost:5432 yourusername@test.traccar.quatrixglobal.com sleep 30
```

* ### The Traccar database server is remote and secure. It does not allow direct connections from the internet to its database port (5432) to prevent hacking attempts. However, it does allow secure SSH connections.


* ### By running this command, we create a secure, encrypted "tunnel" (like a private pipeline) between your local computer and the remote server. We are telling your computer: "Take anything I send to my local port 63333, securely send it through SSH, and drop it directly into the remote server's database port 5432 as if I were sitting right at the server."

* ### The sleep 30 at the end keeps the tunnel open for 30 seconds to give you time to connect. Once you connect, the tunnel will stay alive as long as your connection is active.

## Step 2 : Connecting to the Traccar Database

* ### Now that the tunnel is open, we need to log into the actual PostgreSQL database server using the psql command-line utility

* ### We are telling psql:

* Connect to the database named traccar (-d traccar)

* Look for it on our own machine (-h localhost

* Use our new, open tunnel gateway port (-p 63334)

* Log in as your database user account (-U pkinoti)

```bash
psql -d traccar -h localhost -p 63334 -U pkinoti
```

## Step 3 : Connect the remote traccar to the pgadmin 

* In pgadmin4 : 

1. right-click on Servers at the very top of your left panel and select Create Server

2. In the General tab:

* Name: Type Remote Traccar Test 

3. In the Connection tab:

* Host name/address: localhost - the tunnel brings the remote database to my local machine

* Port: 63334 (matching your -L 63334 flag)

* Username: pkinoti 

* Password: Enter your database password. (kinoti1234)

* Click save 

* ### Once connected, look under your new server's Databases ➡️ traccar ➡️ Schemas ➡️ public ➡️ Tables folder to see all the device and position tables.

## Step 4 : Open the Query Tool

* On the task bar there is the psql tool 

B) . On the new server tree on the left.

* Right-click on the traccar database name

* Select Query Tool from the context menu. A large text editor tab will open on the right side of your screen where you can write and execute your SQL code.

# Creating a New server (yours) in pgadmin 

## Step 1: Create a New Server
 
1. Open **pgAdmin**.
2. Right-click **Servers**.
3. Select **Register → Server...**
 
---
 
## Step 2: Configure the Connection
 
Navigate to the **Connection** tab and enter the following information.
 
| Field | Value |
|-------|-------|
| Host name / address | `localhost` or `127.0.0.1` | use 127.0.0.1
| Port | `5432` |
| Maintenance database | `postgres` *(or your target database)* |
| Username | `postgres` *(or your PostgreSQL user)* |
| Password | *Your PostgreSQL password* |
 
> **Note:** Even though the database is hosted remotely, the host should remain `localhost` because pgAdmin connects through the SSH tunnel.
 
---
 
# Step 3: Configure the SSH Tunnel
 
Open the **SSH Tunnel** tab and configure the following:
 
| Field | Value |
|-------|-------|
| Use SSH tunneling | ✅ Enabled |
| Tunnel host | `test.traccar.quatrixglobal.com` |
| Tunnel port | `22` |
| Username | `pkinoti` |
| Authentication | Password **or** Identity File (SSH Key) | "kinoti1234"
 
### Option 1: Password Authentication
 
Provide:
 
- SSH Username
- SSH Password
 
### Option 2: SSH Key Authentication (Recommended)
 
Provide:
 
- SSH Username
- Path to your private key (e.g. `~/.ssh/id_rsa`)
 
If your key is encrypted, provide the passphrase when prompted.
 
# What we used in the ssh ;

* Access the .ssh file in your pc and select your public key and select the file to pgadmin4

 
# Step 4: Save the Connection
 
1. Click **Save**.
2. pgAdmin will establish the SSH tunnel automatically.
3. If the connection is successful, the remote PostgreSQL server will appear under **Servers**

# Run the Report Queries

# Question 1 . All devices and their corresponding groups using one query.


```bash
SELECT 
    d.id AS device_id,
    d.name AS device_name,
    d.uniqueid,
    g.name AS group_name
FROM tc_devices d
LEFT JOIN tc_groups g ON d.groupid = g.id;
```
Expected Output ; 

```bash
device_id |       device_name        |         uniqueid         | group_name 
-----------+--------------------------+--------------------------+------------
      1902 | KAY485M                  | 355139085072210          | Truck
      1904 | KBA480Q                  | 355139085738547          | Truck
      1851 | 0                        | 254112225128             | Motorcycle
      1852 | BIKE-25239168            | 254710555089             | Bicycle
      1748 | KCE948J                  | 353701094216971          | Truck
      1475 | KBK771X                  | 353701094237704          | Truck
      1907 | KBL795K                  | 355139085833660          | Truck
      1580 | KBZ059Q                  | 353701094236649          | Truck
      1011 | KMER787R                 | 254724071640             | Motorcycle
       790 | KMGB216P                 | 254115730334             | Motorcycle
      1935 | KDW936Z                  | 355139085833611          | Truck
      1260 | KMGH853Z                 | 254711761390             | Motorcycle
       891 | KMFX289E                 | 254701620278             | Motorcycle
      1778 | KDG052D                  | 353701094225881          | Truck
      1906 | KBJ532W                  | 355139085834809          | Truck
      1930 | KDM357V                  | 355139085843032          | Truck
       782 | KMDY364B                 | 254727257595             | Motorcycle
      1874 | KMFW326T                 | 254720210335             | Motorcycle
       784 | KMFX211R                 | 254757959740             | Bicycle
      1946 | X-KCX053S                | X-353701094217672        | Truck
       104 | KMFF747Y                 | 254712608767             | Motorcycle
      1663 | KCC627M                  | 353701094231434          | Truck
      1942 | X-KCL032A                | X-353701094237845        | Truck
       677 | KMFK886A                 | 254715964467             | Motorcycle
      1457 | KAJ531V                  | 353701094234206          | Truck
      1384 | KMGE973L                 | 254723544404             | Motorcycle
       461 | KMFS728L                 | 254720827885             | Motorcycle
      1948 | X-KDL078W                | X-353701094216534        | Truck
       485 | BIKE035B                 | 254723021212             | Bicycle
       714 | KMCN322M                 | 254701866380             | Motorcycle
       493 | KMFZ160P                 | 254704148603             | Motorcycle
      1585 | KDC049G                  | 353701094218399          | Truck
      1446 | KAE628U                  | 353701094220221          | Truck
      1463 | KAU635F                  | 353701094216690          | Truck
       697 | KMDQ087Q                 | 254728624207             | Motorcycle
        77 | KMFC794L                 | 254707424001             | Motorcycle
      1412 | KBS476T                  | 353701094230774          | Truck
       238 | KMEY472A                 | 254728508778             | Motorcycle
       437 | KMEB352Z                 | 254724496529             | Motorcycle
      1410 | KBK871X                  | 353701094230824          | Truck
        27 | KMFP148U                 | 254717574849             | Motorcycle
      1787 | KAT695H                  | 353701094219579          | Truck
         9 | KMFP728Z                 | 254717734327             | Motorcycle
       566 | KMEA570A                 | 254797282970             | Motorcycle
      1423 | KCG651X                  | 353701094216914          | Truck
       141 | KDC001A                  | 254723841328             | Pickup
      1938 | X-KCC666Z                | X-353701094221377        | Truck
      1660 | KCN267N                  | 353701094229263          | Truck
      1941 | X-KCK912T                | X-353701094217243        | Truck
      1364 | KMGG044H                 | 254702416627             | Motorcycle
      1713 | KCJ298F                  | 353701094217896          | Truck
```

# Question 2 : All position data for the last 1 day should including vehicle and the group

```bash
SELECT 
    p.id AS position_id,
    p.devicetime,
    p.latitude,
    p.longitude,
    p.speed,
    d.name AS vehicle_name,
    g.name AS group_name
FROM tc_positions p
JOIN tc_devices d ON p.deviceid = d.id
LEFT JOIN tc_groups g ON d.groupid = g.id
WHERE p.devicetime >= NOW() - INTERVAL '1 day';
```

Expected Output ; 

```bash
position_id |       devicetime        |        latitude         |     longitude      |         speed          | vehicle_name | group_name 
-------------+-------------------------+-------------------------+--------------------+------------------------+--------------+------------
   153044874 | 2026-08-06 10:18:07.781 |              -1.3256783 |         36.8610117 |    0.07875250279903412 | KMEG358X     | Motorcycle
   153046288 | 2026-08-06 11:40:14.941 |     -1.1920716666666666 | 36.997233333333334 |              31.317506 | KDB237E      | Truck
   153046289 | 2026-08-06 11:40:15.802 |               -0.980235 |  36.58296222222222 |              15.118796 | KDT668G      | Truck
   153046290 | 2026-08-06 11:40:21.233 |     -1.2659416666666667 | 36.904133333333334 |     24.838022000000002 | KDA089J      | Truck
   153046291 | 2026-08-06 11:40:21.65  |     -1.3064533333333332 | 36.841681111111114 |              20.518366 | KDE183U      | Van
   153046292 | 2026-08-06 11:40:22.339 |     -1.0593044444444446 |  37.17892888888889 |              16.738667 | KCD632S      | Truck
   153046293 | 2026-08-06 11:40:22.558 |     -1.3061355555555556 |  36.88200277777778 |              11.339097 | KBL795K      | Truck
   153046303 | 2026-08-06 11:40:46.004 |     -0.9789116666666666 | 36.581473333333335 |     14.038882000000001 | KDT668G      | Truck
   153046304 | 2026-08-06 11:40:46.627 |      -1.307223888888889 |  36.84296666666667 |               9.179269 | KDE183U      | Van
   153046305 | 2026-08-06 11:40:46.653 |     -1.0586572222222221 | 37.180863888888894 |              21.058323 | KCD632S      | Truck
   153046331 | 2026-08-06 11:41:26.281 |     -1.0570555555555556 |  37.18562333333333 |              29.157678 | KCD632S      | Truck
   153046332 | 2026-08-06 11:41:29.105 |               -1.280505 |  36.90140888888889 |      5.399570000000001 | KCM312R      | Truck
   153046333 | 2026-08-06 11:41:29.22  |     -1.3016916666666667 | 36.884910000000005 |              23.758108 | KBL795K      | Truck
   153046334 | 2026-08-06 11:41:30.126 |     -1.3090555555555554 |           36.84546 |              16.738667 | KDE183U      | Van
   153046335 | 2026-08-06 11:41:31.194 |     -1.2625149999999998 |  36.90727555555555 |     12.419011000000001 | KDA089J      | Truck
   153046336 | 2026-08-06 11:41:35.019 |     -1.1846583333333334 | 36.993404444444444 |              22.678194 | KDB237E      | Truck
   153046337 | 2026-08-06 11:41:36.145 |     -1.0566322222222222 | 37.186883333333334 |     28.077764000000002 | KCD632S      | Truck
   153046338 | 2026-08-06 11:41:37.023 |     -0.9754433333333333 | 36.578586666666666 |              25.917936 | KDT668G      | Truck
   153046339 | 2026-08-06 11:41:39.102 |               -1.280755 |  36.90155333333334 |      5.399570000000001 | KCM312R      | Truck
   153046340 | 2026-08-06 11:41:39.148 |                 -1.3008 | 36.885465555555555 |              20.518366 | KBL795K      | Truck
   153046341 | 2026-08-06 11:41:42.715 |     -1.2620600000000002 |  36.90783777777778 |     16.198710000000002 | KDA089J      | Truck
   153046342 | 2026-08-06 11:41:45.055 |     -1.1840366666666666 | 36.992424444444445 |              25.917936 | KDB237E      | Truck
   153046343 | 2026-08-06 11:41:45.719 |     -1.0562166666666666 |  37.18811722222222 |              27.537807 | KCD632S      | Truck
   153046344 | 2026-08-06 11:41:45.981 |     -0.9748133333333334 |  36.57756444444445 |              24.298065 | KDT668G      | Truck
   153046345 | 2026-08-06 11:41:47.835 |     -1.3001861111111113 |  36.88578166666667 |     16.198710000000002 | KBL795K:
```

# Question 3 . All devices that are not motorcycles and not trucks

```bash
SELECT id, name, uniqueid, category 
FROM tc_devices 
WHERE UPPER(category) NOT IN ('MOTORCYCLE', 'TRUCK') 
   OR category IS NULL;
```

```bash
 id  |           name           |         uniqueid         | category 
------+--------------------------+--------------------------+----------
 1852 | BIKE-25239168            | 254710555089             | Bicycle
  784 | KMFX211R                 | 254757959740             | bicycle
  485 | BIKE035B                 | 254723021212             | bicycle
  141 | KDC001A                  | 254723841328             | pickup
 1622 | KAW049Y                  | 353701094244239          | pickup
  268 | BIKE023B                 | 254748050383             | bicycle
 1853 | EBIKE-36624308           | 254728388813             | Bicycle
 1336 | E-BIKE03                 | 254742233505             | bicycle
 1205 | Bike-08                  | 254723627262             | bicycle
  354 | BIKE033B                 | 254113276466             | bicycle
  290 | BIKE029B                 | 254112128091             | bicycle
  131 | KMMB051B                 | 254726396506             | bicycle
 1167 | E-BIKE01                 | 254790392219             | bicycle
 1403 | 6532ae2652b2164c0d39862d | 6532ae2652b2164c0d39862d | 
  751 | Bike001                  | 254792310498             | bicycle
 1388 | KCA996Q                  | 353701094227465          | van
 1903 | KAY812Z                  | 353701094240963          | van
 1925 | KDE183U                  | 355139085737937          | van
 1534 | KDK127A                  | 353701094217144          | pickup
  543 | KMFX130X                 | 254790360627             | bicycle
 1360 | E-BIKE02                 | 254769393830             | bicycle
  334 | BIKE014B                 | 254723150111             | bicycle
  213 | BIKE011B                 | 254758740753             | bicycle
 1810 | KCX324P                  | 353701094229420          | van
 1323 | Ebee-E-Bike-39717169     | 254799083977             | bicycle
 1775 | KAP695T                  | 353701094234024          | van
  619 | BIKE1987                 | 254727261484             | bicycle
  205 | BIKE003B                 | 254757921593             | bicycle
  312 | BIKE0323A                | 254700356710             | bicycle
 1688 | KDJ978N                  | 353701094234172          | van
 1614 | KCJ273D                  | 353701094218456          | van
 1218 | Ebike-05                 | 254701000967             | bicycle
  295 | BIKE031B                 | 254707058072             | bicycle
 1161 | Ebee-E-Bike-37744883     | 254748780404             | bicycle
 1132 | KDL153M                  | 254746885358             | pickup
```

# Give Access to Other Users to exam Database

* #### Create a user account/role for a fellow mentee (if you're a remote Quatrix mentee, the admin will suggest a fellow mentee's names). The following should apply:

1. Ensure they can access the database using Ident Authentication meaning they should also have a regular Linux system user account on your local PC.

2. Give them read only access to the exam database.

## Step 1 : Loging in to the server

```bash
ssh pkinoti@test.traccar.quatrixglobal.com
```
## Step 2 : Interactive session with the database 

```bash
sudo -u postgres psql
```
## Step 3 : To display all users 

```bash
\du
```
## Step 4 : Accessing the Ident Authentification 

```bash
sudo nano /etc/postgresql/16/main/pg_hba.conf
```
Edit ; The peer to ident


```bash
local   traccar         amumbi                                  peer
```

To ; 


```bash
local   traccar         amumbi                                  ident
```

1. Press Ctrl + O then Enter to save.

2. Press Ctrl + X to exit back to the command line.

## Step 5 : Reload the server 

```bash
sudo systemctl reload postgresql
```

## Step 6 : Log into the databse again 

```bash
sudo -u postgres psql -d traccar
```

## Step 7 : Grant one user privileges 

* Display the current users 

```bash
\du
```
## Step 8 : Grant the permission to the user amumbi 

```bash
GRANT CONNECT ON DATABASE traccar TO ann;
```
* She can connect to the database and look at it 

## Step 9 : 

```bash
GRANT USAGE ON SCHEMA public TO ann;
```
* She can see the folder structures contained in the specific tables 

## Step 10 :

```bash
GRANT SELECT ON ALL TABLES IN SCHEMA public TO ann;
```
* She can only have the reading -only access 

## Step 11 ; To verify what she can see

* Verify the tables exists ; 


```bash
\dt
```
* To verify the privilege application 

```bash
SELECT table_name, privilege_type 
FROM information_schema.role_table_grants 
WHERE grantee = 'amumbi' 
ORDER BY table_name;
```
Expected Output ;

```bash
    table_name       | privilege_type 
------------------------+----------------
 databasechangelog      | SELECT
 databasechangeloglock  | SELECT
 tc_actions             | SELECT
 tc_attributes          | SELECT
 tc_calendars           | SELECT
 tc_commands            | SELECT
 tc_commands_queue      | SELECT
 tc_device_attribute    | SELECT
 tc_device_command      | SELECT
 tc_device_device       | SELECT
 tc_device_driver       | SELECT
 tc_device_geofence     | SELECT
 tc_device_maintenance  | SELECT
 tc_device_notification | SELECT
 tc_device_order        | SELECT
 tc_device_report       | SELECT
 tc_devices             | SELECT
 tc_drivers             | SELECT
 tc_events              | SELECT
 tc_geofences           | SELECT
 tc_group_attribute     | SELECT
 tc_group_command       | SELECT
 tc_group_driver        | SELECT
 tc_group_geofence      | SELECT
 tc_group_maintenance   | SELECT
 tc_group_notification  | SELECT
 tc_group_order         | SELECT
 tc_group_report        | SELECT
 tc_groups              | SELECT
 tc_keystore            | SELECT
 tc_maintenances        | SELECT
 tc_notifications       | SELECT
 tc_orders              | SELECT
 tc_positions           | SELECT
 tc_reports             | SELECT
 tc_revoked_tokens      | SELECT
 tc_servers             | SELECT
 tc_statistics          | SELECT
 tc_user_attribute      | SELECT
 tc_user_calendar       | SELECT
 tc_user_command        | SELECT
 tc_user_device         | SELECT
 tc_user_driver         | SELECT
 tc_user_geofence       | SELECT
 tc_user_group          | SELECT
 tc_user_maintenance    | SELECT
 tc_user_notification   | SELECT
 tc_user_order          | SELECT
 tc_user_report         | SELECT
```
## If we want the user to have the other priveleges

## Step 1 : Creating the role

```bash
CREATE ROLE purity WITH LOGIN;
```
## Step 2 : Granting access to the user in the database

```bash
GRANT CONNECT ON DATABASE traccar TO purity;
```
## Step 3 : Switch to the traccar

```bash
\c traccar
```
## Step 4 : Connecting the user to the schema

```bash
GRANT USAGE ON SCHEMA public TO purity;
```
## Step 5 : Giving her privileges

```bash
GRANT INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA public TO purity;
```
*To verify :

```bash
SELECT table_name, privilege_type 
FROM information_schema.role_table_grants 
WHERE grantee = 'amumbi' 
ORDER BY table_name;
```
## To remove the privileges 

* Strips the ability to create , change , or remove data records

```bash
REVOKE INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA public FROM purity;
```

* Cleans up any accidental administrative background permissions 

```bash
REVOKE ALL PRIVILEGES ON DATABASE traccar FROM purity;
```

# How to make a user a super user in your Local PC

## Step 1 : We alter the role 

```bash
ALTER ROLE purity WITH SUPERUSER;
```
## Step 2 : To prove it worked 

```bash
\du
```
## Step 3 : To strip back the superuser power

```bash
ALTER ROLE purity WITH NOSUPERUSER;
```
# Differences in the attributes 

* To switch to the other user , you use SET ROLE username;

* SELECT current_user; – Shows the new user you switched to.

* SELECT session_user; – Shows the original user who first authenticated.

* \conninfo – Will still show the original user because the physical connection details haven't changed.

# QUESTION 1 : Testing the CREATE ROLE Attribute

```bash
SET ROLE purity;
```
## Step 1 : Check which user youre on

```bash
SELECT current_user;
```

## Step 2 : Try creating roles in the user purity 

```bash
CREATE ROLE test_user WITH LOGIN;
```

Expected Output : 

```bash
ERROR:  permission denied to create role
DETAIL:  Only roles with the CREATEROLE attribute may create roles.
```
## Step 3 : Granting CREATEROLE to see the change

* ### Switch back to your admin account so you have the authority to alter roles:

```bash
RESET ROLE;
```
* ### Check which user we are using at the moment 

```bash
SELECT current_user;
```

## Step 4 : Grant her the specific attribute

```bash
ALTER ROLE purity WITH CREATEROLE;
```
## Step 5 : Change to purity user to check if the priviledge has been added

```bash
SET ROLE purity;
```
## Step 6 : To test it again 

```bash
CREATE ROLE test_user WITH LOGIN;
```
## Step 7 : What can the new user do with th new privilege 

1. ###  Delete a user ;

* ### Check which user we are in ; 

```bash
SELECT current_user;
```
* ### Delete the user we want to delete with our new user who has privileges

```bash
DROP ROLE ann;
```
* ### We cant use this because PostesSql enforces strict ownership over roles . even though purity has the create role attribute a role cannot drop another role unless it explicitly has thr ADMIN option 

## Step 7b) Reset back to the Postgres Superuser

```bash
RESET ROLE;
```
* ### Check the current user 

```bash
SELECT current_user;
```
* ### Grant Admin Option on ann to purity 

```bash
GRANT ann TO purity WITH ADMIN OPTION;
```
* ### Reassing the ownership of ann's database to purity from the superuser 

```bash
SELECT current_user;
```
```bash
REASSIGN OWNED BY ann TO purity;
```
* ### Drop ann as user purity 

```bash
SET ROLE purity;
```
* ### Confirm the user 

```bash
SELECT current_user;
```
* ### Verify the deletion 

```bash
\du
```
* ### Drop user ann as user purity 

```bash
DROP ROLE ann;
```
* ### Verify the new user

```bash
\du
```
# Question 2 : Attribute Create DB 

## Step 1: Verify purity Lacks CREATEDB Privilege

```bash
\du purity
```
Expected Output ; 

```bash
     List of roles
 Role name | Attributes  
-----------+-------------
 purity    | Create role
```

## Step 2: Grant Database Creation Privilege

* ### Change to the superuser account to grant the privelege to purity 

```bash
RESET ROLE;
```
* ### Check the current user 

```bash
SELECT current_user;
```
* ### Alter the create DB role to purity 

```bash
ALTER ROLE purity WITH CREATEDB;
```

## Step 3 : Switch to the purity User

```bash
SET ROLE purity;
```
* ### Verify the added attribute 

```bash
\du purity
```

## Step 4 : Create a New Database as purity

```bash
CREATE DATABASE purity_test_db;
```
* ### To verify the new database

```bash
\l
```
Expected output ;


```bash
                                                      List of databases
      Name      |  Owner   | Encoding | Locale Provider | Collate |  Ctype  | ICU Locale | ICU Rules |   Access privileges   
----------------+----------+----------+-----------------+---------+---------+------------+-----------+-----------------------
 postgres       | postgres | UTF8     | libc            | C.UTF-8 | C.UTF-8 |            |           | 
 purity_test_db | purity   | UTF8     | libc            | C.UTF-8 | C.UTF-8 |            |           | 
 template0      | postgres | UTF8     | libc            | C.UTF-8 | C.UTF-8 |            |           | =c/postgres          +
                |          |          |                 |         |         |            |           | postgres=CTc/postgres
 template1      | postgres | UTF8     | libc            | C.UTF-8 | C.UTF-8 |            |           | =c/postgres          +
                |          |          |                 |         |         |            |           | postgres=CTc/postgres
 traccar        | postgres | UTF8     | libc            | C.UTF-8 | C.UTF-8 |            |           | =Tc/postgres         +
                |          |          |                 |         |         |            |           | postgres=CTc/postgres+
                |          |          |                 |         |         |            |           | kkiragu=c/postgres   +
                |          |          |                 |         |         |            |           | ywanjiku=c/postgres  +
                |          |          |                 |         |         |            |           | eirungu=c/postgres   +
                |          |          |                 |         |         |            |           | jkipkorir=c/postgres +
                |          |          |                 |         |         |            |           | tajode=c/postgres    +
                |          |          |                 |         |         |            |           | kkiarie=c/postgres   +
                |          |          |                 |         |         |            |           | amumbi=c/postgres    +
                |          |          |                 |         |         |            |           | purity=c/postgres
(5 rows)

```

* ### Hence , a database is a giant container on your server , inside it , we can create tables to hold the actual data . 

## Step 5 : How to use the new database

* ### Connect to the new database 

```bash
\c purity_test_db
```
* ### Create tables inide it 

```bash
CREATE TABLE employees (id SERIAL PRIMARY KEY, name VARCHAR(50));
```
* ### Insert Data into the table 

```bash
INSERT INTO employees (name) VALUES ('Purity'), ('Ann');
```

* ### Verify our data 

```bash
SELECT * FROM employees;
```
* ### To delete all data and keep the empty table 

```bash
TRUNCATE TABLE employees;
```
* ### Delete the Table completely

```bash
DROP TABLE employees;
```

# The attribute SUPERUSER

* ### A Superuser has absolute control over the entire database server, bypassing all security checks and permission restrictions. Because this is the highest level of authority, we must switch back to your original postgres superuser account to grant it.

## Step 1 : Revert to the postgres Superuser

```bash
RESET ROLE;
```
## Step 2: Grant Superuser Attribute to purity

```bash
ALTER ROLE purity WITH SUPERUSER;
```
* ### Verify the new attribute added 

```bash
\du purity
```

## Step 3 : Switch back to purity and utilize the attribute 

```bash
SET ROLE purity;
```
## Step 4 : Access all the tables in the traccar database

```bash
\dt
```
## Step 5 : Select one table 

```bash
\dt tc_devices
```
## Step 6 : Read Data from tc_devices

```bash
SELECT id, name, uniqueid, category FROM tc_devices LIMIT 5;
```
## Step 7 : Insert a New Row into tc_devices

```bash
INSERT INTO tc_devices (id, name, uniqueid, category) VALUES (9999, 'TEST-BIKE', '9999999999', 'bicycle');
```
* ### Insert data in to the row 

```bash
INSERT INTO tc_devices (id, name, uniqueid, category) VALUES (9999, 'TEST-BIKE', '9999999999', 'bicycle');
```
* ### Verify the insertion 

```bash
SELECT id, name, uniqueid, category FROM tc_devices WHERE id = 9999;
```
## Step 8 : Delete the new row

```bash
DELETE FROM tc_devices WHERE id = 9999;
```
* ### Verify the deletion 

```bash
SELECT id, name, uniqueid, category FROM tc_devices WHERE id = 9999;
```

# To strip off all given attributes 

## Step 1 : Switch Back to the postgres Superuser

```bash
RESET ROLE;
```
## Step 2 : Remove all attributes from purity 

```bash
ALTER ROLE purity NOSUPERUSER NOCREATEROLE NOCREATEDB;
```
## Step 3 : Verify the deletion 

```bash
\du purity
```
# Skipped Questions 

## What is the difference between BEGIN and START TRANSACTION?

#### do the exact same thing: they initiate a new transaction block.

### Key diffrences though ;

#### • SQL Standard Compliance: START TRANSACTION is the official SQL standard syntax. BEGIN (or BEGIN TRANSACTION) is an alias adopted by many databases for convenience.

#### • Database Quirks: In some environments, like MySQL, BEGIN can conflict with the BEGIN...END blocks used inside stored procedures. In those cases, using START TRANSACTION is required to avoid syntax errors.


## What is Normalization?

#### is the process of organizing data in a relational database to reduce data redundancy and improve data integrity.


# # SQL Complete Notes — Commands, Concepts, Queries, Practice & Exam Questions

> A full compilation of SQL topics, commands, syntax, queries, practice questions, and exam-style answers.
> Copy this entire file into VS Code or GitHub as your study notes.

---

## Table of Contents

1. [What is SQL?](#1-what-is-sql)
2. [Database Concepts](#2-database-concepts)
3. [Types of SQL Commands](#3-types-of-sql-commands)
4. [Data Types](#4-data-types)
5. [DDL — Data Definition Language](#5-ddl--data-definition-language)
6. [DML — Data Manipulation Language](#6-dml--data-manipulation-language)
7. [DQL — Data Query Language (SELECT)](#7-dql--data-query-language-select)
8. [Filtering with WHERE](#8-filtering-with-where)
9. [Sorting with ORDER BY](#9-sorting-with-order-by)
10. [Limiting Results](#10-limiting-results)
11. [Aggregate Functions](#11-aggregate-functions)
12. [GROUP BY and HAVING](#12-group-by-and-having)
13. [Joins](#13-joins)
14. [Subqueries](#14-subqueries)
15. [Set Operations (UNION, INTERSECT, EXCEPT)](#15-set-operations-union-intersect-except)
16. [String Functions](#16-string-functions)
17. [Date Functions](#17-date-functions)
18. [Numeric Functions](#18-numeric-functions)
19. [CASE Expressions](#19-case-expressions)
20. [Constraints](#20-constraints)
21. [Keys](#21-keys)
22. [Normalization](#22-normalization)
23. [Indexes](#23-indexes)
24. [Views](#24-views)
25. [Transactions (TCL)](#25-transactions-tcl)
26. [DCL — Data Control Language](#26-dcl--data-control-language)
27. [Stored Procedures and Triggers](#27-stored-procedures-and-triggers)
28. [Complete Command Reference (All Commands + Syntax)](#28-complete-command-reference-all-commands--syntax)
29. [Multiple Ways to Get the Same Output](#29-multiple-ways-to-get-the-same-output)
30. [Fill-in-the-Blank Rules](#30-fill-in-the-blank-rules)
31. [Practice Questions & Answers](#31-practice-questions--answers)
32. [Exam-Style Questions](#32-exam-style-questions)
33. [Quick Reference Cheat Sheet](#33-quick-reference-cheat-sheet)

---

## 1. What is SQL?

**SQL (Structured Query Language)** is the standard language for managing and manipulating **relational databases**. It was developed at IBM in the 1970s (originally SEQUEL) and standardized by ANSI and ISO.

**Key points:**

- SQL is a **declarative** language — you say *what* you want, not *how* to get it.
- It works with **relational databases** where data is stored in tables (relations).
- SQL is **case-insensitive** for keywords (`SELECT` = `select`), but table/column names may be case-sensitive depending on the DBMS.
- SQL statements are usually terminated with a **semicolon** `;`.
- It is used by MySQL, PostgreSQL, SQLite, Oracle, SQL Server, MariaDB, and others.

**Q: What does SQL stand for?**
Structured Query Language.

**Q: Who developed SQL and when?**
IBM in the 1970s (originally called SEQUEL).

**Q: Is SQL case-sensitive?**
Keywords are not case-sensitive. Table/column names may be, depending on the DBMS.

**Q: What is a relational database?**
A database that stores data in tables with rows and columns, and defines relationships between tables.

---

## 2. Database Concepts

| Term | Meaning |
|------|---------|
| Database | Organized collection of data |
| Table | A set of rows and columns (a relation) |
| Row / Record / Tuple | One entry in a table |
| Column / Field / Attribute | A property of the entity |
| Primary Key | Unique identifier for each row |
| Foreign Key | Column referencing a primary key in another table |
| Schema | Structure/blueprint of the database |
| DBMS | Database Management System (MySQL, PostgreSQL, etc.) |
| RDBMS | Relational DBMS |
| Query | A request for data |
| Index | Speeds up searching |
| View | A virtual table based on a query |

**Q: What is a primary key?**
A column (or set of columns) that uniquely identifies each row in a table.

**Q: What is a foreign key?**
A column that references the primary key of another table to enforce referential integrity.

**Q: What is a DBMS? Give examples.**
Database Management System — software that manages databases. Examples: MySQL, PostgreSQL, Oracle, SQL Server, SQLite.

**Q: What is the difference between DBMS and RDBMS?**
- DBMS → stores data as files; no relationships enforced.
- RDBMS → stores data in tables; enforces relationships (keys, constraints).

---

## 3. Types of SQL Commands

SQL commands are grouped into five categories:

| Category | Full Form | Purpose | Commands |
|----------|-----------|---------|----------|
| DDL | Data Definition Language | Define/modify structure | `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `RENAME` |
| DML | Data Manipulation Language | Modify data | `INSERT`, `UPDATE`, `DELETE` |
| DQL | Data Query Language | Retrieve data | `SELECT` |
| DCL | Data Control Language | Control access | `GRANT`, `REVOKE` |
| TCL | Transaction Control Language | Manage transactions | `COMMIT`, `ROLLBACK`, `SAVEPOINT` |

**Q: What are the types of SQL commands?**
DDL, DML, DQL, DCL, TCL.

**Q: Which category does `SELECT` belong to?**
DQL (sometimes classified under DML).

**Q: Difference between DDL and DML?**

| DDL | DML |
|-----|-----|
| Defines structure | Modifies data |
| Auto-committed | Can be rolled back |
| `CREATE`, `ALTER`, `DROP` | `INSERT`, `UPDATE`, `DELETE` |

---

## 4. Data Types

Common SQL data types:

| Type | Description | Example |
|------|-------------|---------|
| `INT` / `INTEGER` | Whole numbers | 42 |
| `SMALLINT` | Small integers | 100 |
| `BIGINT` | Large integers | 9999999999 |
| `DECIMAL(p,s)` / `NUMERIC` | Exact decimals | 19.99 |
| `FLOAT` / `REAL` / `DOUBLE` | Approximate decimals | 3.14 |
| `CHAR(n)` | Fixed-length string | 'ABC' |
| `VARCHAR(n)` | Variable-length string | 'Hello' |
| `TEXT` | Long text | paragraph |
| `DATE` | Date only | '2025-01-01' |
| `TIME` | Time only | '14:30:00' |
| `DATETIME` / `TIMESTAMP` | Date + time | '2025-01-01 14:30:00' |
| `BOOLEAN` | True/false | TRUE |
| `BLOB` | Binary data | image |

**Q: Difference between `CHAR` and `VARCHAR`?**

| `CHAR(n)` | `VARCHAR(n)` |
|-----------|--------------|
| Fixed length | Variable length |
| Padded with spaces | No padding |
| Faster for fixed data | Saves space |

**Q: Difference between `DECIMAL` and `FLOAT`?**
`DECIMAL` is exact; `FLOAT` is approximate (floating-point). Use `DECIMAL` for money.

---

## 5. DDL — Data Definition Language

### CREATE

```sql
-- Create database
CREATE DATABASE school;

-- Create table
CREATE TABLE students (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE,
    age INT CHECK (age >= 0),
    enrolled DATE DEFAULT CURRENT_DATE
);

-- Create with foreign key
CREATE TABLE enrollments (
    id INT PRIMARY KEY,
    student_id INT,
    course_id INT,
    FOREIGN KEY (student_id) REFERENCES students(id),
    FOREIGN KEY (course_id) REFERENCES courses(id)
);
```

### ALTER

```sql
ALTER TABLE students ADD COLUMN phone VARCHAR(20);
ALTER TABLE students DROP COLUMN phone;
ALTER TABLE students MODIFY COLUMN name VARCHAR(200);
ALTER TABLE students RENAME TO learners;
ALTER TABLE students ADD CONSTRAINT fk_course FOREIGN KEY (course_id) REFERENCES courses(id);
```

### DROP

```sql
DROP TABLE students;         -- Deletes table + data
DROP DATABASE school;        -- Deletes entire database
```

### TRUNCATE

```sql
TRUNCATE TABLE students;     -- Removes all rows, keeps structure
```

### RENAME

```sql
RENAME TABLE old_name TO new_name;
```

**Q: Difference between `DROP`, `TRUNCATE`, and `DELETE`?**

| DROP | TRUNCATE | DELETE |
|------|----------|--------|
| Removes table structure + data | Removes all rows only | Removes rows based on condition |
| DDL | DDL | DML |
| Cannot rollback | Cannot rollback (usually) | Can rollback |
| No `WHERE` clause | No `WHERE` clause | Supports `WHERE` |
| Fastest | Fast | Slower |

**Q: What does `ALTER TABLE` do?**
Modifies the structure of an existing table (add/drop/rename columns, constraints).

---

## 6. DML — Data Manipulation Language

### INSERT

```sql
-- Single row
INSERT INTO students (id, name, email, age)
VALUES (1, 'Alice', 'alice@example.com', 20);

-- Multiple rows
INSERT INTO students (id, name, email, age) VALUES
(2, 'Bob', 'bob@example.com', 22),
(3, 'Carol', 'carol@example.com', 21);

-- Insert from another table
INSERT INTO students_backup SELECT * FROM students;
```

### UPDATE

```sql
UPDATE students SET age = 21 WHERE id = 1;
UPDATE students SET age = age + 1;                     -- All rows
UPDATE students SET name = 'Al', email = 'al@x.com' WHERE id = 1;
```

### DELETE

```sql
DELETE FROM students WHERE id = 3;
DELETE FROM students;                                   -- All rows
```

**Q: What is the difference between `INSERT INTO` and `INSERT INTO ... SELECT`?**
The first inserts literal values; the second inserts rows from another query/table.

**Q: Do you need a `WHERE` clause with `UPDATE` or `DELETE`?**
No, but without it, **all rows** are affected. Always use `WHERE` unless you intend to modify every row.

---

## 7. DQL — Data Query Language (SELECT)

### Basic SELECT

```sql
SELECT * FROM students;
SELECT name, age FROM students;
```

### Aliases

```sql
SELECT name AS student_name, age AS student_age FROM students;
SELECT s.name, s.age FROM students AS s;
```

### DISTINCT

```sql
SELECT DISTINCT age FROM students;
SELECT DISTINCT city, country FROM customers;
```

### Arithmetic in SELECT

```sql
SELECT name, age, age + 1 AS next_age FROM students;
SELECT price, quantity, price * quantity AS total FROM orders;
```

**Q: What does `SELECT *` mean?**
Selects all columns from the table.

**Q: What does `DISTINCT` do?**
Removes duplicate rows from the result.

**Q: What is an alias?**
A temporary name given to a column or table using `AS`.

---

## 8. Filtering with WHERE

### Comparison operators

| Operator | Meaning |
|----------|---------|
| `=` | Equal |
| `!=` or `<>` | Not equal |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater or equal |
| `<=` | Less or equal |

```sql
SELECT * FROM students WHERE age > 20;
SELECT * FROM students WHERE name = 'Alice';
SELECT * FROM students WHERE age <> 21;
```

### Logical operators

```sql
SELECT * FROM students WHERE age > 20 AND city = 'Nairobi';
SELECT * FROM students WHERE age < 18 OR age > 65;
SELECT * FROM students WHERE NOT city = 'Nairobi';
```

### BETWEEN

```sql
SELECT * FROM students WHERE age BETWEEN 18 AND 25;
```

### IN

```sql
SELECT * FROM students WHERE city IN ('Nairobi', 'Mombasa', 'Kisumu');
```

### LIKE (pattern matching)

| Wildcard | Meaning |
|----------|---------|
| `%` | Zero or more characters |
| `_` | Exactly one character |

```sql
SELECT * FROM students WHERE name LIKE 'A%';        -- Starts with A
SELECT * FROM students WHERE name LIKE '%a';        -- Ends with a
SELECT * FROM students WHERE name LIKE '%li%';      -- Contains li
SELECT * FROM students WHERE name LIKE '_lice';     -- 5 chars ending in lice
```

### IS NULL / IS NOT NULL

```sql
SELECT * FROM students WHERE email IS NULL;
SELECT * FROM students WHERE email IS NOT NULL;
```

**Q: Difference between `=` and `LIKE`?**
`=` matches exactly; `LIKE` allows wildcards (`%`, `_`).

**Q: Difference between `%` and `_` in LIKE?**
`%` matches zero or more characters; `_` matches exactly one character.

**Q: Why can't you use `= NULL`?**
`NULL` is not equal to anything, even itself. Use `IS NULL` or `IS NOT NULL`.

---

## 9. Sorting with ORDER BY

```sql
SELECT * FROM students ORDER BY age;                    -- Ascending (default)
SELECT * FROM students ORDER BY age DESC;               -- Descending
SELECT * FROM students ORDER BY city ASC, age DESC;     -- Multiple columns
SELECT * FROM students ORDER BY 2;                      -- By column position
```

**Q: Default sort order of `ORDER BY`?**
Ascending (`ASC`).

**Q: How do you sort by multiple columns?**
List them separated by commas: `ORDER BY city ASC, age DESC`.

---

## 10. Limiting Results

```sql
-- MySQL / PostgreSQL / SQLite
SELECT * FROM students LIMIT 10;
SELECT * FROM students ORDER BY age DESC LIMIT 5;
SELECT * FROM students LIMIT 10 OFFSET 20;              -- Skip 20, take 10

-- SQL Server / MS Access
SELECT TOP 10 * FROM students;

-- Oracle
SELECT * FROM students WHERE ROWNUM <= 10;
```

**Q: How do you get the top 5 records?**
MySQL: `LIMIT 5`; SQL Server: `TOP 5`; Oracle: `ROWNUM <= 5`.

---

## 11. Aggregate Functions

| Function | Purpose |
|----------|---------|
| `COUNT()` | Count rows |
| `SUM()` | Sum values |
| `AVG()` | Average |
| `MIN()` | Minimum |
| `MAX()` | Maximum |

```sql
SELECT COUNT(*) FROM students;
SELECT COUNT(DISTINCT city) FROM students;
SELECT AVG(age) FROM students;
SELECT SUM(price) FROM orders;
SELECT MIN(age), MAX(age) FROM students;
```

**Q: Difference between `COUNT(*)` and `COUNT(column)`?**
`COUNT(*)` counts all rows; `COUNT(column)` counts non-NULL values in that column.

**Q: Do aggregate functions ignore NULLs?**
Yes — all aggregate functions except `COUNT(*)` ignore NULLs.

---

## 12. GROUP BY and HAVING

### GROUP BY

```sql
SELECT city, COUNT(*) AS num_students
FROM students
GROUP BY city;

SELECT department, AVG(salary)
FROM employees
GROUP BY department;
```

### HAVING

Filters groups **after** aggregation (unlike `WHERE`, which filters rows before).

```sql
SELECT city, COUNT(*) AS num_students
FROM students
GROUP BY city
HAVING COUNT(*) > 5;

SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;
```

**Q: Difference between `WHERE` and `HAVING`?**

| `WHERE` | `HAVING` |
|---------|----------|
| Filters rows before grouping | Filters groups after grouping |
| Cannot use aggregates | Can use aggregates |
| Used with `SELECT` | Used with `GROUP BY` |

**Q: Correct order of SQL clauses?**

```
SELECT → FROM → WHERE → GROUP BY → HAVING → ORDER BY → LIMIT
```

---

## 13. Joins

Combine rows from two or more tables.

### Sample tables

**students**

| id | name | course_id |
|----|------|-----------|
| 1 | Alice | 101 |
| 2 | Bob | 102 |
| 3 | Carol | NULL |

**courses**

| id | title |
|----|-------|
| 101 | Math |
| 102 | Science |
| 103 | History |

### INNER JOIN

Returns rows with matching values in both tables.

```sql
SELECT s.name, c.title
FROM students s
INNER JOIN courses c ON s.course_id = c.id;
```

**Result:** Alice–Math, Bob–Science.

### LEFT JOIN (LEFT OUTER JOIN)

Returns all rows from the left table, matched rows from the right (NULL if no match).

```sql
SELECT s.name, c.title
FROM students s
LEFT JOIN courses c ON s.course_id = c.id;
```

**Result:** Alice–Math, Bob–Science, Carol–NULL.

### RIGHT JOIN (RIGHT OUTER JOIN)

Returns all rows from the right table, matched from the left.

```sql
SELECT s.name, c.title
FROM students s
RIGHT JOIN courses c ON s.course_id = c.id;
```

**Result:** Alice–Math, Bob–Science, NULL–History.

### FULL OUTER JOIN

Returns all rows when there is a match in either table.

```sql
SELECT s.name, c.title
FROM students s
FULL OUTER JOIN courses c ON s.course_id = c.id;
```

(MySQL doesn't support FULL OUTER JOIN directly — emulate with LEFT + UNION + RIGHT.)

### CROSS JOIN

Cartesian product — every row of A × every row of B.

```sql
SELECT s.name, c.title FROM students s CROSS JOIN courses c;
```

### SELF JOIN

Joining a table to itself.

```sql
SELECT e.name AS employee, m.name AS manager
FROM employees e
LEFT JOIN employees m ON e.manager_id = m.id;
```

**Q: Difference between INNER JOIN and LEFT JOIN?**
INNER JOIN returns only matching rows; LEFT JOIN returns all rows from the left table plus matches.

**Q: What is a self join?**
A join where a table is joined with itself.

**Q: What is a cross join?**
A Cartesian product — every row of one table combined with every row of another.

---

## 14. Subqueries

A query inside another query.

### In WHERE

```sql
SELECT name FROM students
WHERE age > (SELECT AVG(age) FROM students);

SELECT name FROM students
WHERE course_id IN (SELECT id FROM courses WHERE title LIKE 'M%');
```

### In FROM

```sql
SELECT AVG(avg_age) FROM (
    SELECT city, AVG(age) AS avg_age
    FROM students
    GROUP BY city
) AS city_avgs;
```

### In SELECT

```sql
SELECT name,
       (SELECT COUNT(*) FROM enrollments e WHERE e.student_id = s.id) AS num_courses
FROM students s;
```

### Correlated subquery

```sql
SELECT name FROM students s
WHERE EXISTS (
    SELECT 1 FROM enrollments e WHERE e.student_id = s.id
);
```

**Q: What is a subquery?**
A query nested inside another query.

**Q: Difference between a subquery and a join?**
Subqueries are often simpler; joins are usually faster for large datasets.

---

## 15. Set Operations (UNION, INTERSECT, EXCEPT)

```sql
-- UNION removes duplicates
SELECT name FROM students
UNION
SELECT name FROM teachers;

-- UNION ALL keeps duplicates
SELECT name FROM students
UNION ALL
SELECT name FROM teachers;

-- INTERSECT — rows in both
SELECT name FROM students
INTERSECT
SELECT name FROM teachers;

-- EXCEPT / MINUS — rows in first but not second
SELECT name FROM students
EXCEPT
SELECT name FROM teachers;
```

| Operator | Meaning |
|----------|---------|
| UNION | Combines, removes duplicates |
| UNION ALL | Combines, keeps duplicates |
| INTERSECT | Rows common to both |
| EXCEPT / MINUS | Rows in first but not second |

**Q: Difference between UNION and UNION ALL?**
`UNION` removes duplicates; `UNION ALL` keeps them (and is faster).

---

## 16. String Functions

| Function | Purpose | Example |
|----------|---------|---------|
| `UPPER(s)` | To uppercase | `UPPER('hi')` → 'HI' |
| `LOWER(s)` | To lowercase | `LOWER('HI')` → 'hi' |
| `LENGTH(s)` / `LEN(s)` | Length | `LENGTH('abc')` → 3 |
| `SUBSTRING(s, start, len)` | Extract part | `SUBSTRING('hello', 1, 3)` → 'hel' |
| `CONCAT(a, b)` | Concatenate | `CONCAT('a','b')` → 'ab' |
| `TRIM(s)` | Remove spaces | `TRIM('  hi  ')` → 'hi' |
| `REPLACE(s, from, to)` | Replace text | `REPLACE('abc','b','X')` → 'aXc' |
| `LEFT(s, n)` | First n chars | `LEFT('hello', 2)` → 'he' |
| `RIGHT(s, n)` | Last n chars | `RIGHT('hello', 2)` → 'lo' |
| `INSTR(s, sub)` | Position of substring | `INSTR('hello','l')` → 3 |

```sql
SELECT UPPER(name) FROM students;
SELECT CONCAT(first_name, ' ', last_name) AS full_name FROM users;
SELECT SUBSTRING(name, 1, 3) FROM students;
```

---

## 17. Date Functions

| Function | Purpose |
|----------|---------|
| `NOW()` / `CURRENT_TIMESTAMP` | Current date and time |
| `CURDATE()` / `CURRENT_DATE` | Current date |
| `CURTIME()` | Current time |
| `YEAR(d)` | Extract year |
| `MONTH(d)` | Extract month |
| `DAY(d)` | Extract day |
| `DATEDIFF(d1, d2)` | Days between dates |
| `DATE_ADD(d, INTERVAL n unit)` | Add to date |
| `DATE_FORMAT(d, format)` | Format date |

```sql
SELECT NOW();
SELECT YEAR(order_date) FROM orders;
SELECT DATEDIFF(NOW(), birth_date) / 365 AS age FROM users;
SELECT * FROM orders WHERE order_date >= '2025-01-01';
```

---

## 18. Numeric Functions

| Function | Purpose |
|----------|---------|
| `ROUND(n, d)` | Round to d decimals |
| `CEIL(n)` / `CEILING(n)` | Round up |
| `FLOOR(n)` | Round down |
| `ABS(n)` | Absolute value |
| `MOD(a, b)` | Remainder |
| `POWER(a, b)` | a^b |
| `SQRT(n)` | Square root |

```sql
SELECT ROUND(3.14159, 2);   -- 3.14
SELECT CEIL(4.2);           -- 5
SELECT FLOOR(4.8);          -- 4
SELECT ABS(-7);             -- 7
SELECT MOD(10, 3);          -- 1
```

---

## 19. CASE Expressions

If/then/else logic in SQL.

```sql
SELECT name, age,
       CASE
           WHEN age < 18 THEN 'Minor'
           WHEN age BETWEEN 18 AND 64 THEN 'Adult'
           ELSE 'Senior'
       END AS age_group
FROM students;
```

```sql
SELECT
    SUM(CASE WHEN gender = 'M' THEN 1 ELSE 0 END) AS males,
    SUM(CASE WHEN gender = 'F' THEN 1 ELSE 0 END) AS females
FROM users;
```

**Q: What is a CASE expression?**
SQL's version of if/then/else — returns different values based on conditions.

---

## 20. Constraints

Rules enforced on columns to maintain data integrity.

| Constraint | Purpose |
|------------|---------|
| `NOT NULL` | Column cannot be empty |
| `UNIQUE` | All values must be distinct |
| `PRIMARY KEY` | Unique + NOT NULL; identifies row |
| `FOREIGN KEY` | References primary key of another table |
| `CHECK` | Values must satisfy a condition |
| `DEFAULT` | Default value if none provided |

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE NOT NULL,
    age INT CHECK (age >= 18),
    status VARCHAR(10) DEFAULT 'active',
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES departments(id)
);
```

**Q: What is the difference between `UNIQUE` and `PRIMARY KEY`?**

| UNIQUE | PRIMARY KEY |
|--------|-------------|
| Can have multiple per table | Only one per table |
| Allows NULL | Does not allow NULL |
| Ensures uniqueness | Ensures uniqueness + NOT NULL |

**Q: What does a `CHECK` constraint do?**
Ensures values satisfy a condition (e.g., `age >= 18`).

---

## 21. Keys

| Key | Meaning |
|-----|---------|
| Primary Key | Uniquely identifies each row |
| Foreign Key | References a primary key in another table |
| Candidate Key | Any column that could be primary key |
| Composite Key | Primary key made of 2+ columns |
| Super Key | Any set of columns that uniquely identify rows |
| Alternate Key | Candidate key not chosen as primary key |

**Q: What is a composite key?**
A primary key made up of two or more columns.

**Q: Difference between a primary key and a candidate key?**
A candidate key is any column that could be primary; the primary key is the one actually chosen.

---

## 22. Normalization

Organizing data to reduce redundancy and improve integrity.

| Normal Form | Rule |
|-------------|------|
| 1NF | Atomic values; no repeating groups |
| 2NF | 1NF + no partial dependencies |
| 3NF | 2NF + no transitive dependencies |
| BCNF | Every determinant is a candidate key |

### 1NF Example

**Before:** `orders(id, customer, products)` — `products` = "apple, banana"
**After:** Split into `orders` and `order_items`.

### 2NF Example

A table `(student_id, course_id, student_name, course_name)` where student_name depends only on student_id → split into students and courses.

### 3NF Example

A table `(student_id, student_name, dept_id, dept_name)` where dept_name depends on dept_id → split into students and departments.

**Q: What is normalization?**
Organizing data into tables to reduce redundancy and prevent anomalies.

**Q: What is 1NF?**
Atomic values in each cell; no repeating groups.

**Q: What is 2NF?**
1NF + no partial dependencies (non-key columns depend on the whole primary key).

**Q: What is 3NF?**
2NF + no transitive dependencies (non-key columns depend only on the primary key).

**Q: What is denormalization?**
Intentionally adding redundancy for performance (opposite of normalization).

---

## 23. Indexes

Speed up queries at the cost of slower writes and more storage.

```sql
CREATE INDEX idx_name ON students(name);
CREATE UNIQUE INDEX idx_email ON students(email);
DROP INDEX idx_name;
```

**Q: What is an index?**
A data structure that speeds up searching in a table.

**Q: What is the downside of indexes?**
They slow down inserts/updates/deletes and consume storage.

**Q: Difference between clustered and non-clustered index?**

| Clustered | Non-Clustered |
|-----------|---------------|
| Physical order of rows | Separate structure |
| One per table | Many per table |
| Fast for range queries | Fast for lookups |

---

## 24. Views

A view is a virtual table based on a query.

```sql
CREATE VIEW student_summary AS
SELECT city, COUNT(*) AS num_students
FROM students
GROUP BY city;

SELECT * FROM student_summary;

CREATE OR REPLACE VIEW v2 AS ...;
DROP VIEW student_summary;
```

**Q: What is a view?**
A saved query that behaves like a table.

**Q: Can you insert into a view?**
Sometimes — only if the view is based on a single table with no aggregates/distinct.

**Q: Advantage of views?**
Simplicity, security (hide columns), abstraction.

---

## 25. Transactions (TCL)

A transaction is a set of operations that succeed or fail as a unit.

### ACID properties

| Property | Meaning |
|----------|---------|
| Atomicity | All or nothing |
| Consistency | Data remains valid |
| Isolation | Transactions don't interfere |
| Durability | Committed data persists |

### Commands

```sql
BEGIN;                            -- or START TRANSACTION
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;                           -- Save changes

ROLLBACK;                         -- Undo changes

SAVEPOINT sp1;
-- ...
ROLLBACK TO sp1;
```

**Q: What are ACID properties?**
Atomicity, Consistency, Isolation, Durability.

**Q: Difference between `COMMIT` and `ROLLBACK`?**
`COMMIT` saves changes permanently; `ROLLBACK` undoes uncommitted changes.

**Q: What is a SAVEPOINT?**
A marker within a transaction you can roll back to.

---

## 26. DCL — Data Control Language

### GRANT

```sql
GRANT SELECT, INSERT ON students TO 'john'@'localhost';
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'%';
```

### REVOKE

```sql
REVOKE INSERT ON students FROM 'john'@'localhost';
REVOKE ALL PRIVILEGES FROM 'john'@'localhost';
```

**Q: Difference between `GRANT` and `REVOKE`?**
`GRANT` gives privileges; `REVOKE` removes them.

---

## 27. Stored Procedures and Triggers

### Stored Procedure

A saved set of SQL statements that can be called.

```sql
DELIMITER //
CREATE PROCEDURE GetStudentsByCity(IN city_name VARCHAR(50))
BEGIN
    SELECT * FROM students WHERE city = city_name;
END //
DELIMITER ;

CALL GetStudentsByCity('Nairobi');
```

### Trigger

Automatically runs when an event (INSERT/UPDATE/DELETE) occurs.

```sql
CREATE TRIGGER after_student_insert
AFTER INSERT ON students
FOR EACH ROW
BEGIN
    INSERT INTO audit_log(action) VALUES ('New student added');
END;
```

**Q: What is a stored procedure?**
A precompiled set of SQL statements stored in the database and callable by name.

**Q: What is a trigger?**
Code that automatically runs on INSERT, UPDATE, or DELETE events.

**Q: Difference between procedure and function?**

| Procedure | Function |
|-----------|----------|
| Called with `CALL` | Called inside a query |
| May not return a value | Must return a value |
| Can modify data | Usually read-only |

---

## 28. Complete Command Reference (All Commands + Syntax)

### DDL

| Command | Syntax |
|---------|--------|
| Create DB | `CREATE DATABASE name;` |
| Drop DB | `DROP DATABASE name;` |
| Create table | `CREATE TABLE name (col type [constraints], ...);` |
| Drop table | `DROP TABLE name;` |
| Truncate | `TRUNCATE TABLE name;` |
| Alter | `ALTER TABLE name ADD/DROP/MODIFY COLUMN ...;` |
| Rename | `RENAME TABLE old TO new;` |

### DML

| Command | Syntax |
|---------|--------|
| Insert | `INSERT INTO t (cols) VALUES (...);` |
| Insert multi | `INSERT INTO t (cols) VALUES (...),(...);` |
| Update | `UPDATE t SET col = val WHERE cond;` |
| Delete | `DELETE FROM t WHERE cond;` |

### DQL

| Clause | Purpose |
|--------|---------|
| `SELECT` | Columns to return |
| `FROM` | Table(s) |
| `WHERE` | Filter rows |
| `GROUP BY` | Group rows |
| `HAVING` | Filter groups |
| `ORDER BY` | Sort |
| `LIMIT` / `TOP` | Limit rows |
| `JOIN` | Combine tables |

### DCL

| Command | Purpose |
|---------|---------|
| `GRANT` | Give privileges |
| `REVOKE` | Remove privileges |

### TCL

| Command | Purpose |
|---------|---------|
| `COMMIT` | Save |
| `ROLLBACK` | Undo |
| `SAVEPOINT` | Marker |
| `SET TRANSACTION` | Set properties |

---

## 29. Multiple Ways to Get the Same Output

### 29.1 Get top 5 by age

```sql
-- MySQL / PostgreSQL
SELECT * FROM students ORDER BY age DESC LIMIT 5;

-- SQL Server
SELECT TOP 5 * FROM students ORDER BY age DESC;

-- Oracle
SELECT * FROM (SELECT * FROM students ORDER BY age DESC) WHERE ROWNUM <= 5;
```

### 29.2 Count students per city (only cities with > 5)

```sql
SELECT city, COUNT(*) AS n
FROM students
GROUP BY city
HAVING COUNT(*) > 5;
```

Alternative with subquery:

```sql
SELECT * FROM (
    SELECT city, COUNT(*) AS n FROM students GROUP BY city
) t WHERE n > 5;
```

### 29.3 Find students older than average

```sql
-- Subquery
SELECT name FROM students WHERE age > (SELECT AVG(age) FROM students);

-- Join with derived table
SELECT s.name
FROM students s
JOIN (SELECT AVG(age) AS avg_age FROM students) a
  ON s.age > a.avg_age;
```

### 29.4 Get all students and their courses (even if no course)

```sql
-- LEFT JOIN
SELECT s.name, c.title
FROM students s
LEFT JOIN courses c ON s.course_id = c.id;

-- NOT EXISTS for those with no course
SELECT s.name FROM students s
WHERE NOT EXISTS (SELECT 1 FROM courses c WHERE c.id = s.course_id);
```

### 29.5 Remove duplicates

```sql
SELECT DISTINCT city FROM students;

SELECT city FROM students GROUP BY city;
```

### 29.6 Upsert (insert or update)

```sql
-- MySQL
INSERT INTO t (id, name) VALUES (1, 'Alice')
ON DUPLICATE KEY UPDATE name = 'Alice';

-- PostgreSQL
INSERT INTO t (id, name) VALUES (1, 'Alice')
ON CONFLICT (id) DO UPDATE SET name = EXCLUDED.name;

-- SQL Server / Oracle
MERGE INTO t USING (SELECT 1 id, 'Alice' name FROM dual) src
ON (t.id = src.id)
WHEN MATCHED THEN UPDATE SET t.name = src.name
WHEN NOT MATCHED THEN INSERT (id, name) VALUES (src.id, src.name);
```

### 29.7 Conditional count

```sql
-- SUM + CASE
SELECT SUM(CASE WHEN gender = 'M' THEN 1 ELSE 0 END) AS males,
       SUM(CASE WHEN gender = 'F' THEN 1 ELSE 0 END) AS females
FROM users;

-- COUNT + FILTER (PostgreSQL)
SELECT COUNT(*) FILTER (WHERE gender = 'M') AS males,
       COUNT(*) FILTER (WHERE gender = 'F') AS females
FROM users;
```

---

## 30. Fill-in-the-Blank Rules

When the question shows part of the command, only write the missing part:

| Question | Answer | NOT |
|----------|--------|-----|
| `SELECT * ___ students;` | `FROM` | `FROM students` |
| `SELECT name FROM students ___ age > 20;` | `WHERE` | `WHERE age > 20` |
| `SELECT city, COUNT(*) FROM students ___ city;` | `GROUP BY` | `GROUP BY city` |
| `SELECT city, COUNT(*) FROM students GROUP BY city ___ COUNT(*) > 5;` | `HAVING` | `HAVING COUNT(*) > 5` |
| `SELECT * FROM students ___ age DESC;` | `ORDER BY` | `ORDER BY age DESC` |
| `SELECT * FROM students ORDER BY age ___ 5;` | `LIMIT` | `LIMIT 5` |
| `SELECT * FROM students s ___ JOIN courses c ON s.course_id = c.id;` | `INNER` | `INNER JOIN courses c ...` |
| `CREATE ___ students (...);` | `TABLE` | `TABLE students` |
| `INSERT ___ students (id, name) VALUES (1, 'Alice');` | `INTO` | `INTO students ...` |
| `UPDATE students ___ age = 21 WHERE id = 1;` | `SET` | `SET age = 21 ...` |
| `DELETE ___ students WHERE id = 3;` | `FROM` | `FROM students ...` |
| `SELECT DISTINCT ___ FROM students;` | `city` | `city FROM students` |

---

## 31. Practice Questions & Answers

### Section A: Basics

**Q1.** What does SQL stand for?
**Answer:** Structured Query Language.

**Q2.** What are the 5 categories of SQL commands?
**Answer:** DDL, DML, DQL, DCL, TCL.

**Q3.** Difference between DBMS and RDBMS?
**Answer:** DBMS stores data as files; RDBMS stores data in tables with enforced relationships.

**Q4.** What is a primary key?
**Answer:** A column (or set of columns) that uniquely identifies each row.

**Q5.** What is a foreign key?
**Answer:** A column referencing the primary key of another table.

**Q6.** Difference between `CHAR` and `VARCHAR`?
**Answer:** `CHAR` is fixed-length (padded); `VARCHAR` is variable-length.

**Q7.** Difference between `DECIMAL` and `FLOAT`?
**Answer:** `DECIMAL` is exact; `FLOAT` is approximate.

### Section B: DDL

**Q8.** Create a table `employees` with `id` (primary key), `name`, `email` (unique), `age`.

**Answer:**

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE,
    age INT CHECK (age >= 18)
);
```

**Q9.** Add a column `phone` to `employees`.

**Answer:** `ALTER TABLE employees ADD COLUMN phone VARCHAR(20);`

**Q10.** Difference between `DROP TABLE` and `TRUNCATE TABLE`?
**Answer:** `DROP` removes the table structure and data; `TRUNCATE` removes only the data.

**Q11.** Difference between `TRUNCATE` and `DELETE`?
**Answer:** `TRUNCATE` is DDL, removes all rows quickly; `DELETE` is DML, can use `WHERE`, can rollback.

### Section C: DML

**Q12.** Insert a new employee `(1, 'Alice', 'alice@example.com', 30)`.

**Answer:**

```sql
INSERT INTO employees (id, name, email, age)
VALUES (1, 'Alice', 'alice@example.com', 30);
```

**Q13.** Update Alice's age to 31.

**Answer:**

```sql
UPDATE employees SET age = 31 WHERE id = 1;
```

**Q14.** Delete employee with id 5.

**Answer:** `DELETE FROM employees WHERE id = 5;`

### Section D: SELECT and Filtering

**Q15.** Select all employees older than 25.

**Answer:** `SELECT * FROM employees WHERE age > 25;`

**Q16.** Select names and emails of employees in 'Nairobi'.

**Answer:** `SELECT name, email FROM employees WHERE city = 'Nairobi';`

**Q17.** Get employees whose age is between 25 and 40.

**Answer:** `SELECT * FROM employees WHERE age BETWEEN 25 AND 40;`

**Q18.** Get employees whose name starts with 'A'.

**Answer:** `SELECT * FROM employees WHERE name LIKE 'A%';`

**Q19.** Get employees whose email is NULL.

**Answer:** `SELECT * FROM employees WHERE email IS NULL;`

**Q20.** Get employees in Nairobi or Mombasa.

**Answer:** `SELECT * FROM employees WHERE city IN ('Nairobi', 'Mombasa');`

### Section E: Sorting and Limiting

**Q21.** Sort employees by age descending.

**Answer:** `SELECT * FROM employees ORDER BY age DESC;`

**Q22.** Get the top 3 highest-paid employees.

**Answer:** `SELECT * FROM employees ORDER BY salary DESC LIMIT 3;`

### Section F: Aggregates and Grouping

**Q23.** Count all employees.

**Answer:** `SELECT COUNT(*) FROM employees;`

**Q24.** Get the average salary per department.

**Answer:**

```sql
SELECT department, AVG(salary) FROM employees GROUP BY department;
```

**Q25.** Show departments with more than 5 employees.

**Answer:**

```sql
SELECT department, COUNT(*) FROM employees
GROUP BY department
HAVING COUNT(*) > 5;
```

**Q26.** Difference between `WHERE` and `HAVING`?
**Answer:** `WHERE` filters rows before grouping; `HAVING` filters groups after aggregation.

### Section G: Joins

**Q27.** Show employees with their department names.

**Answer:**

```sql
SELECT e.name, d.name AS department
FROM employees e
JOIN departments d ON e.dept_id = d.id;
```

**Q28.** Show all employees even if they have no department.

**Answer:** Use `LEFT JOIN`:

```sql
SELECT e.name, d.name
FROM employees e
LEFT JOIN departments d ON e.dept_id = d.id;
```

**Q29.** Difference between INNER JOIN and LEFT JOIN?
**Answer:** INNER returns only matching rows; LEFT returns all rows from the left table plus matches.

**Q30.** What is a self join? Example?
**Answer:** A table joined to itself.

```sql
SELECT e.name AS employee, m.name AS manager
FROM employees e
LEFT JOIN employees m ON e.manager_id = m.id;
```

### Section H: Subqueries

**Q31.** Find employees earning more than the average.

**Answer:**

```sql
SELECT name FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```

**Q32.** Find employees who are not assigned to any project.

**Answer:**

```sql
SELECT name FROM employees e
WHERE NOT EXISTS (SELECT 1 FROM projects p WHERE p.employee_id = e.id);
```

### Section I: Constraints and Keys

**Q33.** Difference between `UNIQUE` and `PRIMARY KEY`?
**Answer:** Primary key is unique + NOT NULL, only one per table; UNIQUE allows NULL and can be multiple.

**Q34.** What is a composite key?
**Answer:** A primary key made of two or more columns.

### Section J: Transactions

**Q35.** What are ACID properties?
**Answer:** Atomicity, Consistency, Isolation, Durability.

**Q36.** Difference between `COMMIT` and `ROLLBACK`?
**Answer:** COMMIT saves changes permanently; ROLLBACK undoes uncommitted changes.

### Section K: Normalization

**Q37.** What is 1NF?
**Answer:** Atomic values, no repeating groups.

**Q38.** What is 2NF?
**Answer:** 1NF + no partial dependencies (non-key columns depend on the full primary key).

**Q39.** What is 3NF?
**Answer:** 2NF + no transitive dependencies (non-key columns depend only on the primary key).

**Q40.** Why normalize?
**Answer:** Reduce redundancy, avoid update/insert/delete anomalies, improve integrity.

---

## 32. Exam-Style Questions

**Q1.** Which SQL statement is used to extract data from a database?
a) OPEN
b) EXTRACT
c) SELECT
d) GET

**Answer: c**

---

**Q2.** Which SQL statement is used to update data in a database?
a) SAVE
b) MODIFY
c) UPDATE
d) SAVE AS

**Answer: c**

---

**Q3.** Which SQL statement is used to delete data from a database?
a) REMOVE
b) COLLAPSE
c) DELETE
d) DROP

**Answer: c**

---

**Q4.** Which SQL statement is used to insert new data in a database?
a) INSERT INTO
b) ADD RECORD
c) ADD NEW
d) INSERT NEW

**Answer: a**

---

**Q5.** With SQL, how do you select all the records from a table named "Persons" where the "LastName" is alphabetically between (and including) "Hansen" and "Pettersen"?
a) `SELECT * FROM Persons WHERE LastName BETWEEN 'Hansen' AND 'Pettersen'`
b) `SELECT * FROM Persons WHERE LastName > 'Hansen'`
c) `SELECT LastName > 'Hansen' AND LastName < 'Pettersen' FROM Persons`
d) `SELECT * FROM Persons WHERE LastName > 'Hansen' AND LastName < 'Pettersen'`

**Answer: a**

---

**Q6.** Which SQL statement is used to return only different values?
a) `SELECT DIFFERENT`
b) `SELECT UNIQUE`
c) `SELECT DISTINCT`
d) `SELECT SINGLE`

**Answer: c**

---

**Q7.** Which SQL statement is used to return the number of rows in a table?
a) `SELECT COUNT(*) FROM table_name`
b) `SELECT COUNT FROM table_name`
c) `SELECT ROWS FROM table_name`
d) `SELECT * FROM table_name`

**Answer: a**

---

**Q8.** With SQL, how can you return all the records from a table named "Persons" sorted descending by "FirstName"?
a) `SELECT * FROM Persons SORT 'FirstName' DESC`
b) `SELECT * FROM Persons ORDER BY FirstName DESC`
c) `SELECT * FROM Persons ORDER FirstName DESC`
d) `SELECT * FROM Persons SORT BY 'FirstName' DESC`

**Answer: b**

---

**Q9.** What does the `WHERE` clause do?
a) Sorts the result
b) Filters rows
c) Groups rows
d) Limits rows

**Answer: b**

---

**Q10.** Difference between `HAVING` and `WHERE`?
a) No difference
b) `HAVING` filters rows, `WHERE` filters groups
c) `HAVING` filters groups, `WHERE` filters rows
d) Both filter groups

**Answer: c**

---

**Q11.** Which JOIN returns all rows from the left table?
a) INNER JOIN
b) LEFT JOIN
c) RIGHT JOIN
d) CROSS JOIN

**Answer: b**

---

**Q12.** Which JOIN produces the Cartesian product of two tables?
a) INNER JOIN
b) LEFT JOIN
c) CROSS JOIN
d) FULL OUTER JOIN

**Answer: c**

---

**Q13.** What does `SELECT DISTINCT city FROM students;` return?
a) All cities including duplicates
b) Unique cities only
c) Count of cities
d) First city only

**Answer: b**

---

**Q14.** What does `COUNT(*)` return?
a) Count of non-NULL columns
b) Count of all rows
c) Count of distinct rows
d) Count of unique columns

**Answer: b**

---

**Q15.** Do aggregate functions ignore NULLs?
a) No
b) Yes, except `COUNT(*)`
c) Only `SUM`
d) Only `AVG`

**Answer: b**

---

**Q16.** Correct order of SQL clauses in a SELECT statement?

**Answer:**

```
SELECT → FROM → WHERE → GROUP BY → HAVING → ORDER BY → LIMIT
```

---

**Q17.** What is the difference between `DELETE`, `TRUNCATE`, and `DROP`?

**Answer:**

| DELETE | TRUNCATE | DROP |
|--------|----------|------|
| DML | DDL | DDL |
| Removes rows | Removes all rows | Removes table |
| Supports WHERE | No WHERE | No WHERE |
| Can rollback | Usually cannot | Cannot |

---

**Q18.** What are ACID properties?

**Answer:** Atomicity, Consistency, Isolation, Durability — properties that ensure reliable transactions.

---

**Q19.** What is the difference between `UNION` and `UNION ALL`?

**Answer:** `UNION` removes duplicates; `UNION ALL` keeps them and is faster.

---

**Q20.** Write a query to find the second-highest salary.

**Answer (MySQL):**

```sql
SELECT MAX(salary) FROM employees
WHERE salary < (SELECT MAX(salary) FROM employees);
```

**PostgreSQL:**

```sql
SELECT salary FROM employees ORDER BY salary DESC LIMIT 1 OFFSET 1;
```

---

**Q21.** Write a query to find duplicate emails.

**Answer:**

```sql
SELECT email, COUNT(*) FROM users
GROUP BY email
HAVING COUNT(*) > 1;
```

---

**Q22.** Write a query to find employees with no manager.

**Answer:**

```sql
SELECT name FROM employees WHERE manager_id IS NULL;
```

---

**Q23.** Write a query to find the department with the highest average salary.

**Answer:**

```sql
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
ORDER BY avg_salary DESC
LIMIT 1;
```

---

**Q24.** Delete duplicate rows keeping the lowest id.

**Answer (MySQL):**

```sql
DELETE t1 FROM users t1
JOIN users t2
ON t1.email = t2.email AND t1.id > t2.id;
```

---

**Q25.** What is the difference between a view and a table?

**Answer:** A table stores data physically; a view is a saved query that produces a virtual table.

---

**Q26.** What is an index? Downside?

**Answer:** Speeds up lookups. Downsides: slows writes and consumes storage.

---

**Q27.** Difference between a stored procedure and a function?

**Answer:** Procedures use `CALL`, may not return values; functions are called in queries and must return a value.

---

**Q28.** What does a trigger do?

**Answer:** Automatically runs code when INSERT/UPDATE/DELETE occurs on a table.

---

**Q29.** What is a transaction?

**Answer:** A group of operations that execute as a single unit — all succeed or all fail.

---

**Q30.** What is normalization? Why do it?

**Answer:** Structuring tables to reduce redundancy and anomalies. Improves integrity and efficiency.

---

## 33. Quick Reference Cheat Sheet

| Task | Command |
|------|---------|
| Create database | `CREATE DATABASE db;` |
| Drop database | `DROP DATABASE db;` |
| Create table | `CREATE TABLE t (...);` |
| Drop table | `DROP TABLE t;` |
| Truncate table | `TRUNCATE TABLE t;` |
| Alter table | `ALTER TABLE t ADD COLUMN c type;` |
| Insert row | `INSERT INTO t (c1,c2) VALUES (v1,v2);` |
| Insert multi-row | `INSERT INTO t (c1,c2) VALUES (v1,v2),(v3,v4);` |
| Update | `UPDATE t SET c = v WHERE cond;` |
| Delete | `DELETE FROM t WHERE cond;` |
| Select all | `SELECT * FROM t;` |
| Select columns | `SELECT c1, c2 FROM t;` |
| Distinct | `SELECT DISTINCT c FROM t;` |
| Alias | `SELECT c AS name FROM t;` |
| Where | `SELECT * FROM t WHERE c = v;` |
| AND/OR | `WHERE c1 = v1 AND c2 = v2` |
| BETWEEN | `WHERE c BETWEEN a AND b` |
| IN | `WHERE c IN (v1, v2, v3)` |
| LIKE | `WHERE c LIKE 'A%'` |
| IS NULL | `WHERE c IS NULL` |
| Order | `SELECT * FROM t ORDER BY c DESC;` |
| Limit | `SELECT * FROM t LIMIT 10;` |
| Offset | `SELECT * FROM t LIMIT 10 OFFSET 20;` |
| Count | `SELECT COUNT(*) FROM t;` |
| Sum | `SELECT SUM(c) FROM t;` |
| Avg | `SELECT AVG(c) FROM t;` |
| Min/Max | `SELECT MIN(c), MAX(c) FROM t;` |
| Group by | `SELECT c, COUNT(*) FROM t GROUP BY c;` |
| Having | `... GROUP BY c HAVING COUNT(*) > 5;` |
| Inner join | `... INNER JOIN t2 ON a.id = b.a_id;` |
| Left join | `... LEFT JOIN t2 ON a.id = b.a_id;` |
| Right join | `... RIGHT JOIN t2 ON a.id = b.a_id;` |
| Full outer join | `... FULL OUTER JOIN t2 ON a.id = b.a_id;` |
| Cross join | `... CROSS JOIN t2;` |
| Self join | `... FROM t e JOIN t m ON e.mgr = m.id;` |
| Subquery | `SELECT * FROM t WHERE c > (SELECT AVG(c) FROM t);` |
| Exists | `WHERE EXISTS (SELECT 1 FROM t2 WHERE t2.id = t.id)` |
| Union | `SELECT ... UNION SELECT ...;` |
| Union all | `SELECT ... UNION ALL SELECT ...;` |
| Intersect | `SELECT ... INTERSECT SELECT ...;` |
| Except | `SELECT ... EXCEPT SELECT ...;` |
| Case | `CASE WHEN c THEN v ELSE v2 END` |
| Coalesce | `COALESCE(col, 'default')` |
| String upper | `UPPER(col)` |
| String lower | `LOWER(col)` |
| Substring | `SUBSTRING(col, 1, 3)` |
| Concat | `CONCAT(a, b)` |
| Length | `LENGTH(col)` |
| Trim | `TRIM(col)` |
| Replace | `REPLACE(col, 'a', 'b')` |
| Current date | `CURDATE()` |
| Current time | `NOW()` |
| Year | `YEAR(date_col)` |
| Date add | `DATE_ADD(d, INTERVAL 1 DAY)` |
| Date diff | `DATEDIFF(d1, d2)` |
| Round | `ROUND(n, 2)` |
| Ceil | `CEIL(n)` |
| Floor | `FLOOR(n)` |
| Abs | `ABS(n)` |
| Mod | `MOD(a, b)` |
| Create index | `CREATE INDEX idx ON t(c);` |
| Drop index | `DROP INDEX idx;` |
| Create view | `CREATE VIEW v AS SELECT ...;` |
| Drop view | `DROP VIEW v;` |
| Grant | `GRANT SELECT ON t TO user;` |
| Revoke | `REVOKE SELECT ON t FROM user;` |
| Begin | `BEGIN;` or `START TRANSACTION;` |
| Commit | `COMMIT;` |
| Rollback | `ROLLBACK;` |
| Savepoint | `SAVEPOINT sp;` |
| Rollback to | `ROLLBACK TO sp;` |
| Procedure | `CREATE PROCEDURE p(...) BEGIN ... END;` |
| Call procedure | `CALL p(...);` |
| Trigger | `CREATE TRIGGER t AFTER INSERT ON tbl ...` |

---

# SQL & PostgreSQL Complete Notes — Based on Practice Screenshots

> A full compilation of all topics, questions, correct answers, and explanations from the screenshots.
> Copy this entire file into VS Code or GitHub as your study notes.

---

## Table of Contents

1. [PostgreSQL CLI (`psql`)](#1-postgresql-cli-psql)
2. [PostgreSQL Roles & Privileges](#2-postgresql-roles--privileges)
3. [PostgreSQL Data Types & Columns](#3-postgresql-data-types--columns)
4. [Data Integrity & Constraints](#4-data-integrity--constraints)
5. [SQL Query Clauses](#5-sql-query-clauses)
6. [SQL Joins](#6-sql-joins)
7. [SQL Window Functions](#7-sql-window-functions)
8. [SQL DDL (Data Definition Language)](#8-sql-ddl-data-definition-language)
9. [SQL Transactions & Foreign Keys](#9-sql-transactions--foreign-keys)
10. [Exam Tips & Common Traps](#10-exam-tips--common-traps)
11. [Quick Reference Cheat Sheet](#11-quick-reference-cheat-sheet)

---

## 1. PostgreSQL CLI (`psql`)

Based on questions about `psql` options and variables.

### The `-c` Option
**Q: What does the `-c` option do?**
**Correct Answer:** Executes a single SQL command or query and then exits.

*   Do not confuse this with `-d` (which specifies the database) or `\cd` (which changes the working directory inside psql).
*   **Example:**
    ```bash
    psql -d mydatabase -c "SELECT * FROM users;"
    ```

### Variables (`-v`)
**Q: To display all SQL statements that `psql` sends to the server, including those generated internally, which variable would you set?**
**Correct Answer:** `psql -v ECHO_HIDDEN=on`
*(Note: `ECHO_SQL` and `ECHO_ALL` are not valid `psql` variables. `ECHO_HIDDEN` reveals the internal queries generated by meta-commands like `\d` or `\dt`).*

---

## 2. PostgreSQL Roles & Privileges

Based on questions about `INHERIT`, `CREATEDB`, and `NOLOGIN`.

### Role Inheritance (`INHERIT`)
**Q: By default, when a role is a member of another role, does it automatically inherit the privileges of the parent role?**
**Correct Answer:** Yes, by default, roles inherit privileges from roles they are members of.

*   `INHERIT` is the default attribute in PostgreSQL.
*   `NOINHERIT` must be explicitly set to disable this behavior.

### Creating Databases (`CREATEDB`)
**Q: Which attribute, when granted to a PostgreSQL role, allows that role to create new databases?**
**Correct Answer:** `CREATEDB`

```sql
-- Grant at creation
CREATE ROLE alice WITH CREATEDB LOGIN;
-- Grant to existing role
ALTER ROLE alice CREATEDB;
```

### No Login (`NOLOGIN`)
**Q: If a role is created with the `NOLOGIN` attribute, what does this imply?**
**Correct Answer:** The role cannot be used to directly connect to the database.

*   Used for "group roles" to manage permissions centrally.
*   You cannot log in as a `NOLOGIN` role, but you can grant it to other roles that *do* have `LOGIN`.

### Default Database Owner
**Q: When a new database is created in PostgreSQL without specifying an owner, who typically becomes the owner by default?**
**Correct Answer:** The role that executed the `CREATE DATABASE` command.

*   It does **not** automatically become owned by the `postgres` superuser.
*   If `alice` (with `CREATEDB`) runs it, `alice` owns it.

---

## 3. PostgreSQL Data Types & Columns

Based on questions about `SERIAL`, `AUTO_INCREMENT`, and column order.

### Auto-Incrementing Columns
**Q: In PostgreSQL, which keyword is typically used to define an auto-incrementing integer column?**
**Correct Answer:** `SERIAL` (or `BIGSERIAL`)

**Q: Besides `SERIAL` or `BIGSERIAL`, what is another way to define an auto-incrementing column in PostgreSQL 10+?**
**Correct Answer:** Using `IDENTITY` columns.

*   **`SERIAL`**: Classic PostgreSQL pseudo-type. Implicitly creates a sequence.
    ```sql
    CREATE TABLE users (id SERIAL PRIMARY KEY, name VARCHAR(50));
    ```
*   **`IDENTITY`**: Modern SQL standard way.
    ```sql
    CREATE TABLE users (id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY, name VARCHAR(50));
    ```
*   **`AUTO_INCREMENT`**: **MySQL ONLY.** Does NOT work in PostgreSQL.

### Column Definition Order
**Q: When defining columns in a `CREATE TABLE` statement, is the order of column definitions significant for anything other than `SELECT *` output?**
**Correct Answer:** Yes, it affects the physical storage order of data on disk, which can sometimes have minor performance implications.

### Data Types
*   `INTEGER` (or `INT`): Standard 4-byte integer.
*   `BIGINT`: 8-byte integer for larger numbers.
*   `NUMERIC`: Exact precision, good for money.

---

## 4. Data Integrity & Constraints

Based on questions about `UNIQUE`, `NOT NULL`, and `PRIMARY KEY`.

### Ensuring Unique Values
**Q: Which constraint ensures that all values in a column are unique?**
**Correct Answer:** `UNIQUE`

*   **`PRIMARY KEY`**: Combines `UNIQUE` + `NOT NULL`. It does more than just enforce uniqueness, so it is the wrong answer to this specific question.
*   **`UNIQUE`**: Specifically enforces uniqueness. Allows `NULL` values (multiple `NULL`s are allowed in PostgreSQL).
*   **`NOT NULL`**: Ensures no empty values, but doesn't prevent duplicates.

### Preventing NULLs
**Q: Which constraint ensures that a column cannot store NULL values?**
**Correct Answer:** `NOT NULL`

*   `PRIMARY KEY` implicitly includes `NOT NULL`, but `NOT NULL` is the direct, specific constraint.

---

## 5. SQL Query Clauses

Based on questions about `FROM`, `SELECT`, `WHERE`, `LIMIT`, and `COUNT`.

### The `FROM` Clause
**Q: The `FROM` clause in a SQL query specifies:**
**Correct Answer:** The table(s) or view(s) from which data will be retrieved.

*   `SELECT` → Specifies the **columns**.
*   `FROM` → Specifies the **tables/views**.
*   `WHERE` → Filters **rows**.
*   `GROUP BY` → Groups rows for aggregation.

### `WHERE` with `AND`/`OR`
**Q: To select orders placed by 'customer_A' AND with a 'total_amount' greater than 100, OR orders placed by 'customer_B', which query logic is correct?**
**Correct Answer:** `WHERE (customer_id = 'customer_A' AND total_amount > 100) OR customer_id = 'customer_B'`

*   **Operator Precedence:** `AND` binds tighter than `OR`. Always use parentheses `()` to make your logic explicit and correct.
*   *Example of how SQL interprets a query without parentheses:*
    `WHERE customer_id = 'customer_A' OR (customer_id = 'customer_B' AND total_amount > 100)`

### `LIMIT` without `OFFSET`
**Q: If you use `LIMIT 5` without an `OFFSET` clause, which rows will be returned?**
**Correct Answer:** The first 5 rows of the result set (after any `ORDER BY`).

*   `LIMIT 5` → First 5 rows.
*   `LIMIT 5 OFFSET 4` → Skips 4 rows, returns the next 5.

### `WHERE NOT LIKE` Wildcard Usage
**Q: To select all product names that do NOT end with 'Kit', which condition is correct?**
**Correct Answer:** `WHERE product_name NOT LIKE '%Kit'`

*   `%` matches any sequence of characters.
*   `NOT LIKE` inverts the pattern match.

### Aggregate Function: `COUNT`
**Q: To count the total number of rows in a table named 'orders', which function would you use with SELECT?**
**Correct Answer:** `COUNT(*)`

*   Counts all rows, regardless of whether any columns contain `NULL` values.
*   `SUM(*)`, `AVG(*)`, and `MAX(*)` are invalid syntax. These require a specific column name inside the parentheses.

---

## 6. SQL Joins

Based on questions about `INNER JOIN`, `OUTER JOIN`, `LEFT JOIN`, and multiple joins.

### `INNER JOIN` vs `OUTER JOIN`
**Q: What is the fundamental difference in the result set between an `INNER JOIN` and any type of `OUTER JOIN` (LEFT, RIGHT, FULL)?**
**Correct Answer:** `INNER JOIN` returns only matching rows, while `OUTER JOIN` returns matching rows plus non-matching rows (filled with NULLs).

### `LEFT JOIN` vs `LEFT OUTER JOIN`
**Q: What is the difference between `LEFT JOIN` and `LEFT OUTER JOIN` in SQL?**
**Correct Answer:** There is no difference. `OUTER` is an optional keyword and `LEFT JOIN` is shorthand for `LEFT OUTER JOIN`.

### Joining Multiple Tables
**Q: When joining three or more tables, how are the `JOIN` clauses typically structured?**
**Correct Answer:** By chaining multiple `JOIN` clauses together, one after the other.

```sql
SELECT c.name, o.order_date, p.product_name
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
JOIN products p ON o.product_id = p.product_id;
```

---

## 7. SQL Window Functions

Based on questions about `ROW_NUMBER()`.

### `ROW_NUMBER()` Tie-breaking
**Q: If `ROW_NUMBER()` is used with `ORDER BY score DESC`, and two rows have the same `score`, how does it assign their ranks?**
**Correct Answer:** It assigns unique, consecutive numbers based on an arbitrary but consistent tie-breaking mechanism (e.g., physical order, internal ID).

### `ROW_NUMBER()` Uniqueness
**Q: Can `ROW_NUMBER()` assign the same number to two different rows within the same partition?**
**Correct Answer:** No, `ROW_NUMBER()` always assigns a unique sequential number within its partition.

### Comparison of Ranking Functions

| Function | Tie Behavior | Example Scores (10, 10, 8) |
| :--- | :--- | :--- |
| `ROW_NUMBER()` | Always unique (1, 2, 3) | 1, 2, 3 |
| `RANK()` | Ties get same number, next number skips | 1, 1, 3 |
| `DENSE_RANK()` | Ties get same number, no gaps | 1, 1, 2 |

---

## 8. SQL DDL (Data Definition Language)

Based on questions about `DROP TABLE IF EXISTS`, `ALTER TABLE`, and derived values.

### `DROP TABLE IF EXISTS`
**Q: What is the benefit of using `DROP TABLE IF EXISTS my_table;`?**
**Correct Answer:** It prevents an error if `my_table` does not exist, allowing the script to continue.

*   Does **not** prompt for confirmation.
*   Does **not** force drop if there are dependencies (use `CASCADE` for that).
*   Does **not** create the table.

### `ALTER TABLE RENAME COLUMN`
**Q: To rename a column 'old_name' to 'new_name', what is the syntax?**
**Correct Answer:** `ALTER TABLE my_table RENAME COLUMN old_name TO new_name;`

### Derived Values
**Q: Which of the following are examples of derived (computed) values in SQL?**
**Correct Answer:**
*   The total amount of an order calculated from item prices and quantities.
*   The age of a person calculated from their birth date.

**Why:**
*   A unique product ID assigned upon creation is a **generated base value** (like a `SERIAL`), not derived from other columns.
*   A customer's name directly stored is a **base value**.

---

## 9. SQL Transactions & Foreign Keys

Based on questions about transaction isolation and `ON DELETE` rules.

### SQL Transaction Isolation
**Q: Which of the following statements about SQL transactions is true?**
**Correct Answer:** Transactions ensure that a series of database operations are treated as a single, atomic unit of work.

*   Related to the 'A' in ACID (Atomicity).
*   Autocommit mode is a default setting, not a universal truth about transactions.

### `ON DELETE RESTRICT` vs `ON DELETE NO ACTION`
**Q: The key difference in *timing* between `ON DELETE RESTRICT` and `ON DELETE NO ACTION` is that `RESTRICT` checks immediately, while `NO ACTION` checks:**
**Correct Answer:** At the end of the transaction.

*   **`RESTRICT`**: Checks immediately. You cannot temporarily violate the constraint.
*   **`NO ACTION`**: Checks at the end of the transaction. Allows temporary violations within a transaction (deferred check).

### ACID Properties
*   **Atomicity:** All or nothing.
*   **Consistency:** Data remains valid.
*   **Isolation:** Transactions don't interfere.
*   **Durability:** Committed data persists.

---

## 10. Exam Tips & Common Traps

1.  **MySQL vs PostgreSQL:** `AUTO_INCREMENT` is MySQL. `SERIAL` or `IDENTITY` is PostgreSQL.
2.  **Constraints:** `UNIQUE` is the pure constraint for uniqueness. `PRIMARY KEY` = `UNIQUE` + `NOT NULL`.
3.  **`FROM` vs `SELECT`:** `FROM` specifies tables. `SELECT` specifies columns.
4.  **`RESTRICT` vs `NO ACTION`:** `RESTRICT` = immediate check. `NO ACTION` = end of transaction check.
5.  **Operator Precedence:** Always use parentheses `()` when mixing `AND` and `OR` in `WHERE` clauses.
6.  **`LIMIT` vs `OFFSET`:** `LIMIT` = how many to return. `OFFSET` = how many to skip.
7.  **`LEFT JOIN` vs `LEFT OUTER JOIN`:** They are exactly the same. `OUTER` is optional.
8.  **Derived Values:** Look for calculations using *other columns* (e.g., `price * quantity`). Generated IDs are base values.
9.  **`psql -c`:** Executes one command and exits (very useful for bash scripts).
10. **`psql ECHO_HIDDEN`:** The secret to seeing the internal queries behind meta-commands like `\d`.

---

## 11. Quick Reference Cheat Sheet

| Task | Command / Concept |
|------|-------------------|
| Auto-increment (Postgres) | `SERIAL` or `GENERATED AS IDENTITY` |
| Auto-increment (MySQL) | `AUTO_INCREMENT` |
| Constraint for uniqueness | `UNIQUE` |
| Constraint for no NULLs | `NOT NULL` |
| Combine UNIQUE + NOT NULL | `PRIMARY KEY` |
| Retrieve tables | `FROM` |
| Retrieve columns | `SELECT` |
| Filter rows | `WHERE` |
| Filter groups | `HAVING` |
| Sort results | `ORDER BY` |
| Limit results | `LIMIT N` |
| Skip results | `OFFSET N` |
| Join only matching rows | `INNER JOIN` |
| Join all left + matching right | `LEFT JOIN` (or `LEFT OUTER JOIN`) |
| Join all right + matching left | `RIGHT JOIN` |
| Unique sequential number | `ROW_NUMBER()` |
| Rank with gaps | `RANK()` |
| Rank without gaps | `DENSE_RANK()` |
| Safe drop table | `DROP TABLE IF EXISTS t;` |
| Rename column | `ALTER TABLE t RENAME COLUMN a TO b;` |
| Not ending with X | `NOT LIKE '%X'` |
| Immediate FK check | `ON DELETE RESTRICT` |
| Deferred FK check | `ON DELETE NO ACTION` |
| Run single SQL from bash | `psql -c "SELECT ..."` |
| See hidden psql queries | `psql -v ECHO_HIDDEN=on` |
| Total rows in table | `SELECT COUNT(*) FROM t;`



# SQL `PARTITION BY` — Complete Notes

> A full compilation of `PARTITION BY` concepts, syntax, use cases, and exam traps.
> Copy this into VS Code or GitHub as your study notes.

---

## Table of Contents

1. [What is `PARTITION BY`?](#1-what-is-partition-by)
2. [`PARTITION BY` vs `GROUP BY`](#2-partition-by-vs-group-by)
3. [Syntax](#3-syntax)
4. [Common Use Cases with Examples](#4-common-use-cases-with-examples)
5. [`PARTITION BY` with Different Window Functions](#5-partition-by-with-different-window-functions)
6. [Multiple Columns in `PARTITION BY`](#6-multiple-columns-in-partition-by)
7. [`PARTITION BY` without `ORDER BY`](#7-partition-by-without-order-by)
8. [Exam Tips & Common Traps](#8-exam-tips--common-traps)
9. [Quick Reference Cheat Sheet](#9-quick-reference-cheat-sheet)

---

## 1. What is `PARTITION BY`?

`PARTITION BY` is a clause used with **window functions** (also called analytic functions) in SQL. It divides the result set into **partitions** (groups) and performs a calculation **within each partition separately**.

- It does **not** collapse rows like `GROUP BY`.
- It keeps **all rows** in the output.
- It resets the calculation for each new partition.

Think of it as: "Split the data into groups, then do the math inside each group, but keep all the original rows."

**Basic Example:**

```sql
SELECT
    department,
    employee_name,
    salary,
    ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) AS rank_in_dept
FROM employees;
```

This assigns a rank to each employee **within their own department**, based on salary (highest first).

---

## 2. `PARTITION BY` vs `GROUP BY`

| Feature | `GROUP BY` | `PARTITION BY` |
|---------|------------|----------------|
| Purpose | Aggregate rows into groups | Calculate within groups |
| Output rows | One row per group | All original rows preserved |
| Used with | Aggregate functions (`SUM`, `COUNT`, etc.) | Window functions (`ROW_NUMBER`, `RANK`, etc.) |
| Example | `SELECT dept, AVG(salary) FROM emp GROUP BY dept;` | `SELECT dept, salary, AVG(salary) OVER (PARTITION BY dept) FROM emp;` |
| Result | Collapses rows | Does not collapse rows |

**Key Point for Exams:**
- `GROUP BY` → fewer rows (one per group).
- `PARTITION BY` → same number of rows as the original table.

---

## 3. Syntax

```sql
<window_function>() OVER (
    PARTITION BY column1, column2
    ORDER BY column3
)
```

- **`PARTITION BY`** → splits the data into groups (optional in a window function).
- **`ORDER BY`** → sorts the rows within each partition (optional, but required for ranking functions).
- **`OVER()`** → the clause that turns a regular function into a window function.

**Example:**

```sql
SELECT
    product_name,
    category,
    price,
    AVG(price) OVER (PARTITION BY category) AS avg_category_price
FROM products;
```

---

## 4. Common Use Cases with Examples

### 4.1 Rank within each group

```sql
SELECT
    employee_name,
    department,
    salary,
    RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS salary_rank
FROM employees;
```

**Result:** Each employee gets a rank within their department (not the whole company).

### 4.2 Running total within each group

```sql
SELECT
    order_date,
    customer_id,
    amount,
    SUM(amount) OVER (PARTITION BY customer_id ORDER BY order_date) AS running_total
FROM orders;
```

**Result:** A running total of each customer's orders over time.

### 4.3 Row number within each group

```sql
SELECT
    product_name,
    category,
    ROW_NUMBER() OVER (PARTITION BY category ORDER BY price DESC) AS rn
FROM products
WHERE rn <= 3;
```

*(Note: You can't use `rn` in `WHERE` directly; you need a subquery or CTE.)*

**Correct version:**

```sql
SELECT * FROM (
    SELECT
        product_name,
        category,
        price,
        ROW_NUMBER() OVER (PARTITION BY category ORDER BY price DESC) AS rn
    FROM products
) t
WHERE rn <= 3;
```

**Result:** Top 3 most expensive products in each category.

### 4.4 Moving average

```sql
SELECT
    sale_date,
    product_id,
    amount,
    AVG(amount) OVER (
        PARTITION BY product_id
        ORDER BY sale_date
        ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
    ) AS moving_avg_3
FROM sales;
```

**Result:** 3-day moving average of sales per product.

### 4.5 Difference from group average

```sql
SELECT
    employee_name,
    department,
    salary,
    salary - AVG(salary) OVER (PARTITION BY department) AS diff_from_dept_avg
FROM employees;
```

**Result:** How much each employee earns above or below their department's average.

### 4.6 Percentage of group total

```sql
SELECT
    employee_name,
    department,
    salary,
    ROUND(100.0 * salary / SUM(salary) OVER (PARTITION BY department), 2) AS pct_of_dept
FROM employees;
```

**Result:** Each employee's salary as a percentage of their department's total payroll.

---

## 5. `PARTITION BY` with Different Window Functions

| Function | What it does with `PARTITION BY` |
|----------|-----------------------------------|
| `ROW_NUMBER()` | Unique sequential number per partition |
| `RANK()` | Rank with gaps for ties, per partition |
| `DENSE_RANK()` | Rank without gaps for ties, per partition |
| `SUM()` | Sum per partition |
| `AVG()` | Average per partition |
| `MIN()` | Min per partition |
| `MAX()` | Max per partition |
| `COUNT()` | Count per partition |
| `LAG()` | Previous row value per partition |
| `LEAD()` | Next row value per partition |
| `FIRST_VALUE()` | First value per partition |
| `LAST_VALUE()` | Last value per partition |
| `NTILE(n)` | Divides partition into n buckets |

**Example with `LAG`:**

```sql
SELECT
    employee_name,
    department,
    salary,
    LAG(salary) OVER (PARTITION BY department ORDER BY salary) AS prev_salary
FROM employees;
```

**Result:** The salary of the previous employee (in order) within the same department.

---

## 6. Multiple Columns in `PARTITION BY`

You can partition by more than one column:

```sql
SELECT
    year,
    month,
    region,
    salesperson,
    SUM(sales) OVER (PARTITION BY year, region) AS yearly_region_total
FROM sales_data;
```

**Result:** Sum of sales per year per region, keeping all original rows.

---

## 7. `PARTITION BY` without `ORDER BY`

If you omit `ORDER BY`, the window function operates on the **entire partition** without a specific order.

```sql
SELECT
    employee_name,
    department,
    salary,
    SUM(salary) OVER (PARTITION BY department) AS dept_total
FROM employees;
```

**Result:** Each row shows the total salary for the department. No ordering is needed because it's a total over the whole partition.

**Note:** For ranking functions like `ROW_NUMBER()` or `RANK()`, if you omit `ORDER BY`, the result is non-deterministic (arbitrary order).

---

## 8. Exam Tips & Common Traps

1. **`PARTITION BY` does NOT reduce rows.** If you want to reduce rows, use `GROUP BY`.

2. **`PARTITION BY` is used with `OVER()`.** Without `OVER()`, it's not a window function.

3. **`PARTITION BY` and `ORDER BY` are different:**
   - `PARTITION BY` = groups
   - `ORDER BY` = sorting within each group

4. **You can't use a window function alias in `WHERE`.** You must use a subquery or CTE:
   ```sql
   -- WRONG
   SELECT ROW_NUMBER() OVER (...) AS rn FROM t WHERE rn <= 3;
   
   -- CORRECT
   SELECT * FROM (
       SELECT ROW_NUMBER() OVER (...) AS rn FROM t
   ) x WHERE rn <= 3;
   ```

5. **`PARTITION BY` vs `GROUP BY` in one query:** You can use both in a single query, but they serve different purposes.
   ```sql
   SELECT
       department,
       AVG(salary) AS avg_salary,
       COUNT(*) OVER (PARTITION BY department) AS emp_count
   FROM employees
   GROUP BY department;
   ```

6. **`PARTITION BY` can reference any column** (not just the ones in the `SELECT` list).

7. **`PARTITION BY` order does matter** for output: partitions are processed independently, and results are combined.

8. **Common exam question:** "What's the difference between `GROUP BY` and `PARTITION BY`?"
   - `GROUP BY` → one row per group.
   - `PARTITION BY` → all rows preserved, calculation within groups.

9. **`PARTITION BY` resets at each boundary.** Calculations start fresh for every new partition.

10. **Performance tip:** `PARTITION BY` can be slower than `GROUP BY` on large datasets because it processes every row, not just groups.

---

## 9. Quick Reference Cheat Sheet

| Task | SQL |
|------|-----|
| Rank within department | `RANK() OVER (PARTITION BY department ORDER BY salary DESC)` |
| Row number within category | `ROW_NUMBER() OVER (PARTITION BY category ORDER BY price DESC)` |
| Running total per customer | `SUM(amount) OVER (PARTITION BY customer_id ORDER BY order_date)` |
| Department total (all rows) | `SUM(salary) OVER (PARTITION BY department)` |
| Department average | `AVG(salary) OVER (PARTITION BY department)` |
| Previous row value | `LAG(salary) OVER (PARTITION BY department ORDER BY salary)` |
| Next row value | `LEAD(salary) OVER (PARTITION BY department ORDER BY salary)` |
| Difference from group average | `salary - AVG(salary) OVER (PARTITION BY department)` |
| Percent of group total | `100.0 * salary / SUM(salary) OVER (PARTITION BY department)` |
| Multiple columns | `PARTITION BY year, region` |
| Top N per group | `SELECT * FROM (SELECT ..., ROW_NUMBER() OVER (PARTITION BY ...) AS rn FROM t) x WHERE rn <= N;` |
| 3-day moving average | `AVG(amount) OVER (PARTITION BY product_id ORDER BY sale_date ROWS BETWEEN 2 PRECEDING AND CURRENT ROW)` |
| Bucket into quartiles | `NTILE(4) OVER (PARTITION BY department ORDER BY salary DESC)` |

---

### Example Table for Practice

**employees**

| id | name | department | salary |
|----|------|------------|--------|
| 1 | Alice | HR | 50000 |
| 2 | Bob | HR | 60000 |
| 3 | Carol | IT | 80000 |
| 4 | Dave | IT | 75000 |
| 5 | Eve | IT | 90000 |
| 6 | Frank | Sales | 70000 |

**Query:**

```sql
SELECT
    name,
    department,
    salary,
    ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) AS rn,
    AVG(salary) OVER (PARTITION BY department) AS dept_avg,
    SUM(salary) OVER (PARTITION BY department) AS dept_total
FROM employees;
```

**Result:**

| name | department | salary | rn | dept_avg | dept_total |
|------|------------|--------|----|-----------|------------|
| Bob | HR | 60000 | 1 | 55000 | 110000 |
| Alice | HR | 50000 | 2 | 55000 | 110000 |
| Eve | IT | 90000 | 1 | 81666.67 | 245000 |
| Carol | IT | 80000 | 2 | 81666.67 | 245000 |
| Dave | IT | 75000 | 3 | 81666.67 | 245000 |
| Frank | Sales | 70000 | 1 | 70000 | 70000 |

**Observation:**
- `rn` resets for each department.
- `dept_avg` and `dept_total` repeat for every row in the same department.
- All original rows are preserved.

---


| Concept | Rule |
| :--- | :--- |
| **LEFT JOIN** | Returns all rows from the left table, plus matching rows from the right. Non-matches get NULL. |
| **LEFT OUTER JOIN** | Exactly the same as LEFT JOIN. OUTER is an optional keyword. |
| **INNER JOIN** | Returns only matching rows from both tables. (This is what your wrong answer described). |
| **COUNT(*)** | Counts the total number of rows in a table. |
| **SUM(col) / AVG(col)** | Requires a specific numeric column name inside the parentheses. |


# Complete Guide to SQL "BY" Clauses

> A full breakdown of all SQL clauses that use the keyword "BY", when to use them, and how they work in a query.
> Copy this into VS Code or GitHub as your study notes.

---

## Table of Contents

1. [Overview of All "BY" Clauses](#1-overview-of-all-by-clauses)
2. [GROUP BY](#2-group-by)
3. [ORDER BY](#3-order-by)
4. [PARTITION BY](#4-partition-by)
5. [Special Cases: DISTRIBUTE BY, SORT BY, CLUSTER BY](#5-special-cases-distribute-by-sort-by-cluster-by)
6. [Logical Execution Order](#6-logical-execution-order)
7. [Quick Reference Cheat Sheet](#7-quick-reference-cheat-sheet)

---

## 1. Overview of All "BY" Clauses

| Clause | Purpose | Collapses Rows? | Used With |
|--------|---------|-----------------|-----------|
| `GROUP BY` | Aggregate rows into groups | Yes | Aggregate functions (`SUM`, `COUNT`, `AVG`, etc.) |
| `ORDER BY` | Sort the final result set | No | Any `SELECT` statement |
| `PARTITION BY` | Divide rows into groups for window functions | No | Window functions (`OVER()`) |
| `DISTRIBUTE BY` | Distribute rows among reducers (Hive/Spark) | No | Big data tools |
| `SORT BY` | Sort within partitions (Hive/Spark) | No | Big data tools |
| `CLUSTER BY` | Combination of `DISTRIBUTE BY` + `SORT BY` | No | Big data tools |

---

## 2. GROUP BY

### What it does:
Groups rows that have the same values in specified columns into summary rows.

### When to use:
- When you want to calculate aggregates (`SUM`, `COUNT`, `AVG`, `MIN`, `MAX`) per group.
- When you want **one row per unique group**.

### Syntax:

```sql
SELECT column1, aggregate_function(column2)
FROM table_name
GROUP BY column1;
```

### Example:

```sql
SELECT department, COUNT(*) AS num_employees, AVG(salary) AS avg_salary
FROM employees
GROUP BY department;
```

**Result:** One row per department, with the count of employees and the average salary.

| department | num_employees | avg_salary |
|------------|---------------|------------|
| HR | 2 | 55000 |
| IT | 3 | 81666.67 |
| Sales | 1 | 70000 |

### Key Rules:
- Every column in the `SELECT` list that is **not** an aggregate must appear in the `GROUP BY`.
- `WHERE` filters rows *before* grouping.
- `HAVING` filters groups *after* grouping.

---

## 3. ORDER BY

### What it does:
Sorts the final result set by one or more columns.

### When to use:
- When you want results in a specific order (alphabetical, numerical, chronological).
- When you use `LIMIT` or `OFFSET` (always order first so you know which rows you're getting).

### Syntax:

```sql
SELECT column1, column2
FROM table_name
ORDER BY column1 [ASC|DESC], column2 [ASC|DESC];
```

### Example:

```sql
SELECT name, salary
FROM employees
ORDER BY salary DESC, name ASC;
```

**Result:** Employees sorted by salary (highest first). If two have the same salary, sort by name alphabetically.

### Key Rules:
- Default is `ASC` (ascending).
- Use `DESC` for descending order.
- Can sort by multiple columns (separated by commas).
- Can sort by column position (e.g., `ORDER BY 2` means the 2nd column in `SELECT`).

---

## 4. PARTITION BY

### What it does:
Divides the result set into partitions (groups) and performs a window function calculation **within each partition**, while keeping **all rows**.

### When to use:
- When you want to calculate something per group (e.g., rank within a department) **without** collapsing rows.
- When you need running totals, moving averages, or rankings.
- When you want to compare a row to its group average/total.

### Syntax:

```sql
SELECT column1, column2,
       window_function() OVER (PARTITION BY column1 ORDER BY column2)
FROM table_name;
```

### Example:

```sql
SELECT name, department, salary,
       RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS rank_in_dept
FROM employees;
```

**Result:** Every employee is listed, with a rank showing where they fall within their department.

| name | department | salary | rank_in_dept |
|------|------------|--------|--------------|
| Bob | HR | 60000 | 1 |
| Alice | HR | 50000 | 2 |
| Eve | IT | 90000 | 1 |
| Carol | IT | 80000 | 2 |
| Dave | IT | 75000 | 3 |
| Frank | Sales | 70000 | 1 |

### Key Rules:
- Used with `OVER()`.
- Does **not** collapse rows.
- `ORDER BY` inside `OVER()` defines the order of calculation *within* each partition.
- Without `ORDER BY`, the calculation applies to the whole partition.

---

## 5. Special Cases: DISTRIBUTE BY, SORT BY, CLUSTER BY

These are used in **Hive** and **Spark SQL** (big data tools), not standard SQL. Included for completeness.

### DISTRIBUTE BY
- Distributes rows to reducers based on column values.
- Used to control data movement.

```sql
SELECT * FROM sales DISTRIBUTE BY region;
```

### SORT BY
- Sorts data **within each reducer** (not globally).

```sql
SELECT * FROM sales SORT BY amount DESC;
```

### CLUSTER BY
- Combination of `DISTRIBUTE BY` and `SORT BY`.

```sql
SELECT * FROM sales CLUSTER BY region;
```

---

## 6. Logical Execution Order

SQL clauses are written in one order, but executed in a different order:

```
1. FROM         →  Get the table(s)
2. WHERE        →  Filter rows
3. GROUP BY     →  Group rows
4. HAVING       →  Filter groups
5. SELECT       →  Pick columns
6. PARTITION BY →  Apply window functions (with OVER)
7. ORDER BY     →  Sort final result
8. LIMIT        →  Limit rows
```

### Example Query with All Clauses:

```sql
SELECT department, COUNT(*) AS num_emp, AVG(salary) OVER (PARTITION BY department) AS avg_by_dept
FROM employees
WHERE salary > 30000
GROUP BY department, salary
HAVING COUNT(*) > 1
ORDER BY num_emp DESC
LIMIT 10;
```

---

## 7. Quick Reference Cheat Sheet

| Clause | Use It When You Want To... | Example |
|--------|----------------------------|---------|
| `GROUP BY` | Aggregate rows into one per group | `SELECT dept, COUNT(*) FROM emp GROUP BY dept;` |
| `ORDER BY` | Sort the result set | `SELECT * FROM emp ORDER BY salary DESC;` |
| `PARTITION BY` | Calculate within groups without collapsing | `SELECT name, RANK() OVER (PARTITION BY dept ORDER BY salary DESC) FROM emp;` |
| `DISTRIBUTE BY` | Distribute rows in big data tools | `SELECT * FROM sales DISTRIBUTE BY region;` |
| `SORT BY` | Sort within partitions in big data tools | `SELECT * FROM sales SORT BY amount DESC;` |
| `CLUSTER BY` | Combine distribute + sort in big data tools | `SELECT * FROM sales CLUSTER BY region;` |

---

### Golden Rule:
- **`GROUP BY`** → Collapses rows into groups (one row per group).
- **`PARTITION BY`** → Keeps all rows but calculates within groups.
- **`ORDER BY`** → Sorts the final output.

Think of it like this:
- `GROUP BY` = "Summarize this for me."
- `PARTITION BY` = "Show me everything, but calculate a group stat next to each row."
- `ORDER BY` = "Put it in this order."

---

**End of SQL "BY" Clauses Notes.**