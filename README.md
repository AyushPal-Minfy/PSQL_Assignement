** PSQL ASSIGNMENT **
```js
PS C:\Users\Minfy> psql -U postgres
Password for user postgres:
psql (17.5)
WARNING: Console code page (850) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

PS C:\Users\Minfy> psql -U ayush -d university_db;
Password for user ayush:
psql (17.5)
WARNING: Console code page (850) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

university_db=> \l
                                                              List of databases
     Name      |  Owner   | Encoding | Locale Provider |      Collate       |       Ctype        | Locale | ICU Rules |   Access privileges
---------------+----------+----------+-----------------+--------------------+--------------------+--------+-----------+-----------------------
 postgres      | postgres | UTF8     | libc            | English_India.1252 | English_India.1252 |        |           |  template0     | postgres | UTF8     | libc            | English_India.1252 | English_India.1252 |        |           | =c/postgres          +
               |          |          |                 |                    |                    |        |           | postgres=CTc/postgres
 template1     | postgres | UTF8     | libc            | English_India.1252 | English_India.1252 |        |           | =c/postgres          +
               |          |          |                 |                    |                    |        |           | postgres=CTc/postgres
 university_db | ayush    | UTF8     | libc            | English_India.1252 | English_India.1252 |        |           | =Tc/ayush            +
               |          |          |                 |                    |                    |        |           | ayush=CTc/ayush
(4 rows)


university_db=> CREATE TABLE students (
university_db(>     student_id INTEGER,
university_db(>     first_name VARCHAR(50),
university_db(>     last_name VARCHAR(50),
university_db(>     email VARCHAR(100),
university_db(>     date_of_birth DATE
university_db(> );
CREATE TABLE
university_db=>
university_db=> \d
         List of relations
 Schema |   Name   | Type  | Owner
--------+----------+-------+-------
 public | students | table | ayush
(1 row)


university_db=> select * from students ;
 student_id | first_name | last_name | email | date_of_birth
------------+------------+-----------+-------+---------------
(0 rows)


university_db=> alter table students add column enrollment_date date;
ALTER TABLE
university_db=> select * from students ;
 student_id | first_name | last_name | email | date_of_birth | enrollment_date
------------+------------+-----------+-------+---------------+-----------------
(0 rows)


university_db=> alter table students drop column enrollment_date ;
ALTER TABLE
university_db=> select * from students ;
 student_id | first_name | last_name | email | date_of_birth
------------+------------+-----------+-------+---------------
(0 rows)


university_db=>  alter table students alter column email TYPE VARCHAR(150);
ALTER TABLE


university_db=> ALTER TABLE students RENAME COLUMN date_of_birth TO dob;
ALTER TABLE


university_db=>  ALTER TABLE students ADD CONSTRAINT unique_email UNIQUE (email);
ALTER TABLE


university_db=> select * from students ;
 student_id | first_name | last_name | email | dob
------------+------------+-----------+-------+-----
(0 rows)


university_db=> INSERT INTO students (student_id,first_name,last_name,email,dob)
university_db-> VALUES(1, 'Ayush', 'Pal', 'ayush@gmail.com', '2003-03-07');
INSERT 0 1
university_db=> select * from students;
 student_id | first_name | last_name |      email      |    dob
------------+------------+-----------+-----------------+------------
          1 | Ayush      | Pal       | ayush@gmail.com | 2003-03-07
(1 row)


university_db=> INSERT INTO students (student_id, first_name, last_name, email, dob)
university_db-> VALUES
university_db->   (1, 'Ayush', 'Pal', 'ayush1@gmail.com', '2003-03-07'),   
                  (2, 'Amrit', 'Kumar', 'amritk@gmail.com', '2003-01-24'),
university_db->   (3, 'Amrit', 'Subhash', 'amrits@gmail.com', '2003-08-13'),
university_db->   (4, 'Satya', 'Brat', 'satya@gmail.com', '1995-04-24'),
university_db->   (5, 'Mahith', 'K', 'mahith@gmail.com', '2010-12-24');
INSERT 0 5


university_db=> select * from students
university_db-> ;
 student_id | first_name | last_name |      email       |    dob
------------+------------+-----------+------------------+------------
          1 | Ayush      | Pal       | ayush@gmail.com  | 2003-03-07
          1 | Ayush      | Pal       | ayush1@gmail.com | 2003-03-07
          2 | Amrit      | Kumar     | amritk@gmail.com | 2003-01-24
          3 | Amrit      | Subhash   | amrits@gmail.com | 2003-08-13
          4 | Satya      | Brat      | satya@gmail.com  | 1995-04-24
          5 | Mahith     | K         | mahith@gmail.com | 2010-12-24
(6 rows)


university_db=> DELETE FROM students
university_db-> WHERE student_id = 1 AND email = 'ayush1@gmail.com';
DELETE 1


university_db=> select * from students;
 student_id | first_name | last_name |      email       |    dob
------------+------------+-----------+------------------+------------
          1 | Ayush      | Pal       | ayush@gmail.com  | 2003-03-07
          2 | Amrit      | Kumar     | amritk@gmail.com | 2003-01-24
          3 | Amrit      | Subhash   | amrits@gmail.com | 2003-08-13
          4 | Satya      | Brat      | satya@gmail.com  | 1995-04-24
          5 | Mahith     | K         | mahith@gmail.com | 2010-12-24
(5 rows)


university_db=>  SELECT * FROM students WHERE student_id = 2;
 student_id | first_name | last_name |      email       |    dob
------------+------------+-----------+------------------+------------
          2 | Amrit      | Kumar     | amritk@gmail.com | 2003-01-24
(1 row)

                                         ^
university_db=> SELECT * FROM students WHERE dob < '2002-01-01';
 student_id | first_name | last_name |      email      |    dob
------------+------------+-----------+-----------------+------------
          4 | Satya      | Brat      | satya@gmail.com | 1995-04-24
(1 row)


university_db=> SELECT * FROM students WHERE first_name LIKE 'B%' OR first_name LIKE 'C%';
 student_id | first_name | last_name | email | dob
------------+------------+-----------+-------+-----
(0 rows)


university_db=> SELECT * FROM students
university_db-> WHERE email LIKE '%@gmail.com';
 student_id | first_name | last_name |      email       |    dob
------------+------------+-----------+------------------+------------
          1 | Ayush      | Pal       | ayush@gmail.com  | 2003-03-07
          2 | Amrit      | Kumar     | amritk@gmail.com | 2003-01-24
          3 | Amrit      | Subhash   | amrits@gmail.com | 2003-08-13
          4 | Satya      | Brat      | satya@gmail.com  | 1995-04-24
          5 | Mahith     | K         | mahith@gmail.com | 2010-12-24
(5 rows)


university_db=> SELECT * FROM students WHERE email IS NULL;
 student_id | first_name | last_name | email | dob
------------+------------+-----------+-------+-----
(0 rows)


university_db=> UPDATE students
university_db-> SET email = 'satyab@example.com'
university_db-> WHERE student_id = 4;
UPDATE 1


university_db=> select * from students;
 student_id | first_name | last_name |       email        |    dob
------------+------------+-----------+--------------------+------------
          1 | Ayush      | Pal       | ayush@gmail.com    | 2003-03-07
          2 | Amrit      | Kumar     | amritk@gmail.com   | 2003-01-24
          3 | Amrit      | Subhash   | amrits@gmail.com   | 2003-08-13
          5 | Mahith     | K         | mahith@gmail.com   | 2010-12-24
          4 | Satya      | Brat      | satyab@example.com | 1995-04-24
(5 rows)


university_db=> SELECT * FROM students ORDER BY last_name ASC;
 student_id | first_name | last_name |       email        |    dob
------------+------------+-----------+--------------------+------------
          4 | Satya      | Brat      | satyab@example.com | 1995-04-24
          5 | Mahith     | K         | mahith@gmail.com   | 2010-12-24
          2 | Amrit      | Kumar     | amritk@gmail.com   | 2003-01-24
          1 | Ayush      | Pal       | ayush@gmail.com    | 2003-03-07
          3 | Amrit      | Subhash   | amrits@gmail.com   | 2003-08-13
(5 rows)


university_db=> SELECT * FROM students ORDER BY dob DESC;
 student_id | first_name | last_name |       email        |    dob
------------+------------+-----------+--------------------+------------
          5 | Mahith     | K         | mahith@gmail.com   | 2010-12-24
          3 | Amrit      | Subhash   | amrits@gmail.com   | 2003-08-13
          1 | Ayush      | Pal       | ayush@gmail.com    | 2003-03-07
          2 | Amrit      | Kumar     | amritk@gmail.com   | 2003-01-24
          4 | Satya      | Brat      | satyab@example.com | 1995-04-24
(5 rows)


university_db=> SELECT * FROM students ORDER BY last_name, first_name;
 student_id | first_name | last_name |       email        |    dob
------------+------------+-----------+--------------------+------------
          4 | Satya      | Brat      | satyab@example.com | 1995-04-24
          5 | Mahith     | K         | mahith@gmail.com   | 2010-12-24
          2 | Amrit      | Kumar     | amritk@gmail.com   | 2003-01-24
          1 | Ayush      | Pal       | ayush@gmail.com    | 2003-03-07
          3 | Amrit      | Subhash   | amrits@gmail.com   | 2003-08-13
(5 rows)


university_db=> SELECT * FROM students ORDER BY dob DESC LIMIT 3;
 student_id | first_name | last_name |      email       |    dob
------------+------------+-----------+------------------+------------
          5 | Mahith     | K         | mahith@gmail.com | 2010-12-24
          3 | Amrit      | Subhash   | amrits@gmail.com | 2003-08-13
          1 | Ayush      | Pal       | ayush@gmail.com  | 2003-03-07
(3 rows)


university_db=> SELECT * FROM students ORDER BY student_id LIMIT 2 OFFSET 2;
 student_id | first_name | last_name |       email        |    dob
------------+------------+-----------+--------------------+------------
          3 | Amrit      | Subhash   | amrits@gmail.com   | 2003-08-13
          4 | Satya      | Brat      | satyab@example.com | 1995-04-24
(2 rows)


university_db=> SELECT DISTINCT last_name FROM students ORDER BY last_name;
 last_name
-----------
 Brat
 K
 Kumar
 Pal
 Subhash
(5 rows)


university_db=> SELECT DISTINCT last_name, first_name FROM students;
 last_name | first_name
-----------+------------
 Pal       | Ayush
 Kumar     | Amrit
 Brat      | Satya
 Subhash   | Amrit
 K         | Mahith
(5 rows)


university_db=> SELECT COUNT (*) AS total_students FROM students;
 total_students
----------------
              5
(1 row)

                                      ^
university_db=> SELECT COUNT(email) AS students_with_email FROM students;
 students_with_email
---------------------
                   5
(1 row)


university_db=> SELECT MIN(dob) AS oldest_student_dob FROM students;
 oldest_student_dob
--------------------
 1995-04-24
(1 row)


university_db=> SELECT MAX(dob) AS youngest_student_dob FROM students;
 youngest_student_dob
----------------------
 2010-12-24
(1 row)


university_db=> select * from students;
 student_id | first_name | last_name |       email        |    dob
------------+------------+-----------+--------------------+------------
          1 | Ayush      | Pal       | ayush@gmail.com    | 2003-03-07
          2 | Amrit      | Kumar     | amritk@gmail.com   | 2003-01-24
          3 | Amrit      | Subhash   | amrits@gmail.com   | 2003-08-13
          5 | Mahith     | K         | mahith@gmail.com   | 2010-12-24
          4 | Satya      | Brat      | satyab@example.com | 1995-04-24
(5 rows)


university_db=> SELECT last_name, COUNT(*) AS number_of_students FROM students GROUP BY last_name
university_db-> ORDER BY number_of_students DESC;
 last_name | number_of_students
-----------+--------------------
 Brat      |                  1
 Subhash   |                  1
 Pal       |                  1
 Kumar     |                  1
 K         |                  1
(5 rows)


university_db=> SELECT last_name, COUNT(*) AS number_of_students
university_db-> FROM students
university_db-> GROUP BY last_name
university_db-> HAVING COUNT(*) > 1
university_db-> ORDER BY number_of_students DESC;
 last_name | number_of_students
-----------+--------------------
(0 rows)


university_db=> SELECT EXTRACT(YEAR FROM dob) AS birth_year, COUNT(*) AS students_in_year
university_db-> FROM students
university_db-> WHERE dob IS NOT NULL
university_db-> GROUP BY birth_year
university_db-> ORDER BY birth_year;
 birth_year | students_in_year
------------+------------------
       1995 |                1
       2003 |                3
       2010 |                1
(3 rows)


university_db=> DROP TABLE students;
DROP TABLE


university_db=> CREATE TABLE students(
university_db(> student_id INTEGER,
university_db(> first_name VARCHAR(50) NOT NULL,
university_db(> last_name VARCHAR(50) NOT NULL,
university_db(> email VARCHAR(100) unique,
university_db(> dob DATE,
university_db(> enrollment_status VARCHAR(10) CHECK (enrollment_status IN ('enrolled', 'graduated', 'dropped'))
university_db(> );
CREATE TABLE


university_db=> SELECT * FROM students;
 student_id | first_name | last_name | email | dob | enrollment_status
------------+------------+-----------+-------+-----+-------------------
(0 rows)


university_db=> DROP TABLE students;
DROP TABLE


university_db=> CREATE TABLE students(
university_db(> student_id SERIAL PRIMARY KEY,
university_db(> first_name VARCHAR(50) NOT NULL,
university_db(> last_name VARCHAR(50) NOT NULL,
university_db(> email VARCHAR(100) unique,
university_db(> dob DATE,
university_db(> enrollment_status VARCHAR(10) CHECK (enrollment_status IN ('enrolled', 'graduated', 'dropped', 'Pending'))
university_db(> );
CREATE TABLE


university_db=> SELECT * FROM students;
 student_id | first_name | last_name | email | dob | enrollment_status
------------+------------+-----------+-------+-----+-------------------
(0 rows)


university_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
university_db-> VALUES ('Alice', 'Smith', 'alice.smith@example.com', '2003-05-15', 'enrolled');
INSERT 0 1
university_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
university_db-> VALUES ('Robert', 'Johnson', 'robert.j@example.com', '2002-08-22', 'enrolled');
INSERT 0 1


university_db=> select * from students;
 student_id | first_name | last_name |          email          |    dob     | enrollment_status
------------+------------+-----------+-------------------------+------------+-------------------
          1 | Alice      | Smith     | alice.smith@example.com | 2003-05-15 | enrolled
          2 | Robert     | Johnson   | robert.j@example.com    | 2002-08-22 | enrolled
(2 rows)


university_db=> SELECT * FROM students;
 student_id | first_name | last_name |          email          |    dob     | enrollment_status
------------+------------+-----------+-------------------------+------------+-------------------
          1 | Alice      | Smith     | alice.smith@example.com | 2003-05-15 | enrolled
          2 | Robert     | Johnson   | robert.j@example.com    | 2002-08-22 | enrolled
(2 rows)


university_db=> CREATE TABLE courses(
university_db(> course_id SERIAL PRIMARY KEY,
university_db(> course_name VARCHAR(100) NOT NULL UNIQUE,
university_db(> credits INTEGER CHECK (credits > 0 AND credits < 10)
university_db(> );
CREATE TABLE
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Introduction to SQL', 3);
INSERT 0 1
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Database Design', 4);
INSERT 0 1
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Web Development', 3);
INSERT 0 1
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Data Structures', 4);
INSERT 0 1


university_db=> SELECT * FROM courses;
 course_id |     course_name     | credits
-----------+---------------------+---------
         1 | Introduction to SQL |       3
         2 | Database Design     |       4
         3 | Web Development     |       3
         4 | Data Structures     |       4
(4 rows)


university_db=> CREATE TABLE enrollments(
university_db(> enrollment_id SERIAL PRIMARY KEY,
university_db(> student_id INTEGER NOT NULL,
university_db(> course_id INTEGER NOT NULL,
university_db(> enrollment_date DATE DEFAULT CURRENT_DATE,
university_db(> grade CHAR(1) CHECK (grade IN ('A', 'B', 'C', 'D', 'F', 'W', NULL)),
university_db(> CONSTRAINT fk_student
university_db(> FOREIGN KEY (student_id)
university_db(>         REFERENCES students(student_id)
university_db(>         ON DELETE CASCADE,
university_db(> CONSTRAINT fk_course
university_db(>         FOREIGN KEY (course_id)
university_db(>         REFERENCES courses(course_id)
university_db(>         ON DELETE RESTRICT,
university_db(> UNIQUE (student_id, course_id)
university_db(> );
CREATE TABLE


university_db=> SELECT * FROM enrollments;
 enrollment_id | student_id | course_id | enrollment_date | grade
---------------+------------+-----------+-----------------+-------
(0 rows)


university_db=> INSERT INTO enrollments (student_id, course_id, grade) VALUES (1, 1, 'A');
INSERT 0 1
university_db=> INSERT INTO enrollments (student_id, course_id) VALUES (1, 2);
INSERT 0 1


university_db=> SELECT * FROM enrollments;
 enrollment_id | student_id | course_id | enrollment_date | grade
---------------+------------+-----------+-----------------+-------
             1 |          1 |         1 | 2025-05-30      | A
             2 |          1 |         2 | 2025-05-30      |
(2 rows)


university_db=> INSERT INTO enrollments (student_id, course_id, grade) VALUES (2, 1, 'B');
INSERT 0 1


university_db=> SELECT * FROM enrollments;
 enrollment_id | student_id | course_id | enrollment_date | grade
---------------+------------+-----------+-----------------+-------
             1 |          1 |         1 | 2025-05-30      | A
             2 |          1 |         2 | 2025-05-30      |
             3 |          2 |         1 | 2025-05-30      | B
(3 rows)
```
