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

Step 1 ; CREATE DATABASE
Environment for the data school_system 

```bash
CREATE DATABASE school_system;
```

Step 2 ; Switch to the new database environment to create the tables 

```bash
\c school_system
```
Explain command;

1. /c - used to connect database named school_system .Hence, it intsructs the terminal to disconnect from your current database and open a new session and the target database we want to access is the school_system 

Step 3 ; Inside the database (environment) we need specific structures that hold our data .

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

Step 4 ; Inserting data into our tables 

```bash
INSERT INTO students (first_name, last_name) VALUES 
('Purity', 'Nkirote'),
('Brianna', 'Makena'),
('Zion', 'Gitonga'),
('Kenan', 'Ndungu'),
('Grace', 'Magoma'),
('Arlene', 'Khakai');
```
