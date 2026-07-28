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
# QUERY QUESTIONS ; 

### 1. Display students named Alice.

* From the students table .

```bash
SELECT * FROM student WHERE name LIKE 'Alice%';
```
Explain the command ;

1. 'Alice%'- The percentage sif=gn is a wildcard character used with he LIKE operator in SQL . It acts a placeholder that matches any sequence of characters including no characters at all . hence, it finds any students whose name start with alice followed by anything else eg ; Alice C Kimani .

### 2. How many students are from Mombasa (count_id=1) county?

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
Explaining the command 

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

* Displaying the initia data 

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

```bash
SELECT c.name AS county_name, ROUND(CAST(float8(AVG(ss.score)) as numeric), 4) as ave_score
FROM county c
JOIN student s ON c.id = s.county_id
JOIN student_subject ss ON s.id = ss.student_id
GROUP BY c.id, c.name
ORDER BY ave_score DESC;
```
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

