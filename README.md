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

Create Employees table
CREATE TABLE employees (
  id SERIAL PRIMARY KEY,
  name VARCHAR(255),
  salary NUMERIC(10,2),
  department_id INT,
  hire_date DATE
);

INSERT INTO employees (name, salary, department_id, hire_date)
VALUES 
  ('Tom', 4550.50, 1, '2022-01-01'),
  ('John', 5100.75, 1, '2022-01-01'),
  ('Tina', 5550.25, 1, '2022-01-01'),
  ('Jane', 6100.50, 2, '2022-04-01'),
  ('Bob', 7200.25, 2, '2022-04-01'),
  ('Tim', 7750.75, 2, '2022-04-01'),
  ('Sam', 8000.00, 3, '2022-08-01'),
  ('Tara', 8500.00, 3, '2022-08-01');
  ('Bleh1', 4552.50, 1, '2022-01-02');
  ('Bleh', 4550.50, 1, '2022-01-02');
Select all Employees
select * from employees;
 id | name | salary  | department_id | hire_date  
----+------+---------+---------------+------------
  1 | Tom  | 4550.50 |             1 | 2022-01-01
  2 | John | 5100.75 |             1 | 2022-01-01
  3 | Tina | 5550.25 |             1 | 2022-01-01
  4 | Jane | 6100.50 |             2 | 2022-04-01
  5 | Bob  | 7200.25 |             2 | 2022-04-01
  6 | Tim  | 7750.75 |             2 | 2022-04-01
  7 | Sam  | 8000.00 |             3 | 2022-08-01
  8 | Tara | 8500.00 |             3 | 2022-08-01
  9 | Bleh  | 4550.50 |             1 | 2022-01-02
 10 | Bleh1 | 4552.50 |             1 | 2022-01-02
(10 rows)
Non-aggregate function
select id, name, salary, department_id, hire_date, round(salary) as rounded_salary from employees;
 id | name  | salary  | department_id | hire_date  | rounded_salary 
----+-------+---------+---------------+------------+----------------
  1 | Tom   | 4550.50 |             1 | 2022-01-01 |           4551
  2 | John  | 5100.75 |             1 | 2022-01-01 |           5101
  3 | Tina  | 5550.25 |             1 | 2022-01-01 |           5550
  4 | Jane  | 6100.50 |             2 | 2022-04-01 |           6101
  5 | Bob   | 7200.25 |             2 | 2022-04-01 |           7200
  6 | Tim   | 7750.75 |             2 | 2022-04-01 |           7751
  7 | Sam   | 8000.00 |             3 | 2022-08-01 |           8000
  8 | Tara  | 8500.00 |             3 | 2022-08-01 |           8500
  9 | Bleh  | 4550.50 |             1 | 2022-01-02 |           4551
 10 | Bleh1 | 4552.50 |             1 | 2022-01-02 |           4553
(10 rows)

Aggregate function
 select  sum(salary) as salary_sum from employees;
 salary_sum 
------------
   61856.00
(1 row)
Aggregate function: FAIL
select  id, sum(salary) as salary_sum from employees;
ERROR:  column "employees.id" must appear in the GROUP BY clause or be used in an aggregate function
LINE 1: select  id, sum(salary) as salary_sum from employees;
Group by: Single Column
select department_id, sum(salary) from employees group by department_id; 
 department_id |   sum    
---------------+----------
             3 | 16500.00
             2 | 21051.50
             1 | 24304.50
(3 rows)
Group by: Multiple columns
select department_id, hire_date, sum(salary) from employees group by department_id, hire_date; 
 department_id | hire_date  |   sum    
---------------+------------+----------
             3 | 2022-08-01 | 16500.00
             1 | 2022-01-02 |  9103.00
             1 | 2022-01-01 | 15201.50
             2 | 2022-04-01 | 21051.50
(4 rows)
Group by: With Having Clause
Order of execution is important, notice that having clause cann't access salary_sum but sum(salary)
select department_id, hire_date, sum(salary) as salary_sum from employees group by department_id, hire_date having sum(salary) > 10000;  
 department_id | hire_date  | salary_sum 
---------------+------------+------------
             3 | 2022-08-01 |   16500.00
             1 | 2022-01-01 |   15201.50
             2 | 2022-04-01 |   21051.50
(3 rows)
