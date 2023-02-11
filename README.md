# cat-DB
<img width="235" alt="image" src="https://user-images.githubusercontent.com/69424250/216411915-175a6245-bad3-4727-85ba-d4c926ad6ceb.png"> <br>
- start the project with requirements. <br>
- don't jump to attributes directly.<br>
- derive ENTITIES/RELATONS/ATTRIBUTES from requirements.

<img width="651" alt="image" src="https://user-images.githubusercontent.com/69424250/216418126-8ead3ce1-3544-4195-81c7-db514848723d.png">


### Students and Departments table
```sql
select * from students;
 student_id | student_name | department_id 
------------+--------------+---------------
          5 | Mohit        |              
          7 | Cat          |            10
          8 | St1          |             1
          9 | St2          |             1
         10 | St3          |             2
(5 rows)

postgres=# select * from departments;
 department_id | department_name  |     professor      
---------------+------------------+--------------------
             1 | Computer Science | Dr. Smith
             2 | Mathematics      | Dr. Johnson
             3 | Physics          | Dr. Brown
             4 | EEE              | Prof Bhayanak Maut
(4 rows)
```

### Cross joining both the tables
```sql
SELECT * FROM students CROSS JOIN departments;

 student_id | student_name | department_id | department_id | department_name  |     professor      
------------+--------------+---------------+---------------+------------------+--------------------
          5 | Mohit        |               |             1 | Computer Science | Dr. Smith
          5 | Mohit        |               |             2 | Mathematics      | Dr. Johnson
          5 | Mohit        |               |             3 | Physics          | Dr. Brown
          5 | Mohit        |               |             4 | EEE              | Prof Bhayanak Maut
          7 | Cat          |            10 |             1 | Computer Science | Dr. Smith
          7 | Cat          |            10 |             2 | Mathematics      | Dr. Johnson
          7 | Cat          |            10 |             3 | Physics          | Dr. Brown
          7 | Cat          |            10 |             4 | EEE              | Prof Bhayanak Maut
          8 | St1          |             1 |             1 | Computer Science | Dr. Smith
          8 | St1          |             1 |             2 | Mathematics      | Dr. Johnson
          8 | St1          |             1 |             3 | Physics          | Dr. Brown
          8 | St1          |             1 |             4 | EEE              | Prof Bhayanak Maut
          9 | St2          |             1 |             1 | Computer Science | Dr. Smith
          9 | St2          |             1 |             2 | Mathematics      | Dr. Johnson
          9 | St2          |             1 |             3 | Physics          | Dr. Brown
          9 | St2          |             1 |             4 | EEE              | Prof Bhayanak Maut
         10 | St3          |             2 |             1 | Computer Science | Dr. Smith
         10 | St3          |             2 |             2 | Mathematics      | Dr. Johnson
         10 | St3          |             2 |             3 | Physics          | Dr. Brown
         10 | St3          |             2 |             4 | EEE              | Prof Bhayanak Maut
(20 rows)
```

### Left joining Students and Departments Table
```sql
SELECT * FROM students LEFT JOIN departments
ON students.department_id = departments.department_id;

 student_id | student_name | department_id | department_id | department_name  |  professor  
------------+--------------+---------------+---------------+------------------+-------------
          5 | Mohit        |               |               |                  | 
          7 | Cat          |            10 |               |                  | 
          8 | St1          |             1 |             1 | Computer Science | Dr. Smith
          9 | St2          |             1 |             1 | Computer Science | Dr. Smith
         10 | St3          |             2 |             2 | Mathematics      | Dr. Johnson
(5 rows)
```

### Right joining Students and Departments Table
```sql
SELECT * FROM students RIGHT JOIN departments
ON students.department_id = departments.department_id;

 student_id | student_name | department_id | department_id | department_name  |     professor      
------------+--------------+---------------+---------------+------------------+--------------------
          8 | St1          |             1 |             1 | Computer Science | Dr. Smith
          9 | St2          |             1 |             1 | Computer Science | Dr. Smith
         10 | St3          |             2 |             2 | Mathematics      | Dr. Johnson
            |              |               |             4 | EEE              | Prof Bhayanak Maut
            |              |               |             3 | Physics          | Dr. Brown
(5 rows)
```
### Outer joining Students and Departments Table

```sql
SELECT * FROM students                       
FULL OUTER JOIN departments
ON students.department_id = departments.department_id;
 student_id | student_name | department_id | department_id | department_name  |     professor      
------------+--------------+---------------+---------------+------------------+--------------------
          5 | Mohit        |               |               |                  | 
          7 | Cat          |            10 |               |                  | 
          8 | St1          |             1 |             1 | Computer Science | Dr. Smith
          9 | St2          |             1 |             1 | Computer Science | Dr. Smith
         10 | St3          |             2 |             2 | Mathematics      | Dr. Johnson
            |              |               |             4 | EEE              | Prof Bhayanak Maut
            |              |               |             3 | Physics          | Dr. Brown
(7 rows)

```

### Inner joining Students and Departments
```sql
select * from students inner join departments on
students.department_id = departments.department_id;
 student_id | student_name | department_id | department_id | department_name  |  professor  
------------+--------------+---------------+---------------+------------------+-------------
          8 | St1          |             1 |             1 | Computer Science | Dr. Smith
          9 | St2          |             1 |             1 | Computer Science | Dr. Smith
         10 | St3          |             2 |             2 | Mathematics      | Dr. Johnson
(3 rows)
```
