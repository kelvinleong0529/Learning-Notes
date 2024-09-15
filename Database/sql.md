# **FILTERING DATA**
## **ORDER BY**
- allows you to sort the rows returned by the SELECT clause by one or more sort expressions in ascending or descending order
```SQL
SELECT
	employee_id,
	first_name,
	last_name,
	hire_date,
	salary
FROM
	employees
ORDER BY
	first_name,
	last_name DESC;
```
- **FIRST** Sort by "first_name" in ascending order, **THEN** sort by "last_name" in descending order

## **DISTINCT**
- If you use one column after the DISTINCT operator, the DISTINCT operator uses values in that column to evaluate duplicates
- If you use two or more columns, the DISTINCT will use the combination of values in those columns to evaluate the duplicate
```SQL
SELECT DISTINCT
	job_id,
	salary
FROM
	employees
ORDER BY
	job_id,
	salary DESC;
```
- uses values from both "job_id" and "salary" to evaluate and remove the duplicate (only remove rows that has same job_id AND salary)
- **DISTINCT** keeps only one **NULL** in the result set

## **LIMIT**
- To limit the number of rows returned by a select statement
```SQL
SELECT 
    column_list
FROM
    table1
ORDER BY column_list
LIMIT row_count OFFSET offset_count;
```
1. The LIMIT row_count determines the number of rows (row_count) returned by the query.
2. The OFFSET offset_count clause skips the offset_count rows before beginning to return the rows.
```SQL
SELECT 
    employee_id, 
    first_name, 
    last_name
FROM
    employees
ORDER BY 
	first_name
LIMIT 5;   
```
![alt text](https://www.sqltutorial.org/wp-content/uploads/2016/04/SQL-LIMIT-5-example.png)
```SQL
SELECT 
    employee_id, first_name, last_name
FROM
    employees
ORDER BY first_name
LIMIT 5 OFFSET 3;
```
![alt text](https://www.sqltutorial.org/wp-content/uploads/2016/04/SQL-LIMIT-OFFSET-example.png)

# **LOGICAL OPERATORS**
1. AND
```SQL
SELECT 
    first_name, last_name, salary
FROM
    employees
WHERE
    salary > 5000 AND salary < 7000
ORDER BY salary;
```
2. OR
```SQL
SELECT 
    first_name, last_name, salary
FROM
    employees
WHERE
    salary = 7000 OR salary = 8000
ORDER BY salary;
```
3. IS NULL
```SQL
SELECT 
    first_name, last_name, phone_number
FROM
    employees
WHERE
    phone_number IS NULL
ORDER BY first_name , last_name;
```
4. BETWEEN
```SQL
SELECT 
    first_name, last_name, salary
FROM
    employees
WHERE
    salary BETWEEN 9000 AND 12000
ORDER BY salary;   
```
5. IN
```SQL
SELECT 
    first_name, last_name, department_id
FROM
    employees
WHERE
    department_id IN (8, 9)
ORDER BY department_id;
```
6. LIKE (REGEX)
- The percent sign ( %) represents zero, one, or multiple characters.
- The underscore sign ( _) represents a single character.
```SQL
SELECT 
    employee_id, first_name, last_name
FROM
    employees
WHERE
    first_name LIKE 'jo%'
ORDER BY first_name;
```
- return any records where "first_name" begins with **"jo"**
![alt text](https://www.sqltutorial.org/wp-content/uploads/2018/01/SQL-Logical-Operators-LIKE-example.png)
7. ALL
- compares a value to all values in another value set
- Must be preceded by a comparison operator and followed by a subquery
```SQL
SELECT 
    first_name, last_name, salary
FROM
    employees
WHERE
    salary >= ALL (SELECT 
            salary
        FROM
            employees
        WHERE
            department_id = 8)
ORDER BY salary DESC;
```
- finds all employees whose salaries are greater than all salaries of employees in the department 8
9. ANY
- compares a value to any value in a set according to the condition
```SQL
SELECT 
    first_name, last_name, salary
FROM
    employees
WHERE
    salary > ANY(SELECT 
            AVG(salary)
        FROM
            employees
        GROUP BY department_id)
ORDER BY first_name , last_name; 
```
- finds all employees whose salaries are greater than the average salary of every department
10. EXISTS
- tests if a subquery contains any rows
- If the subquery returns one or more rows, the result of the EXISTS is true; otherwise, the result is false
```SQL
SELECT 
    first_name, last_name
FROM
    employees e
WHERE
    EXISTS( SELECT 
            1
        FROM
            dependents d
        WHERE
            d.employee_id = e.employee_id);
```
11. NOT
- negate the result of any Boolean expression
```SQL
SELECT
	employee_id,
	first_name,
	last_name,
	salary
FROM
	employees
WHERE
	department_id = 5
AND NOT salary > 5000
ORDER BY
	salary;
```
- get the employees who work in the department id 5 and with a salary not greater than 5000
```SQL
SELECT
	employee_id,
	first_name,
	last_name
FROM
	employees e
WHERE
	NOT EXISTS (
		SELECT
			employee_id
		FROM
			dependents d
		WHERE
			d.employee_id = e.employee_id
	);
```
![alt text](https://www.sqltutorial.org/wp-content/uploads/2016/03/employees_dependents_tables.png)
- uses the NOT EXISTS operator to get the employees who do not have any dependents

12.CASE
- allows you to evaluate a list of conditions and returns one of the possible results
```SQL
SELECT 
    first_name,
    last_name,
    hire_date,
    CASE (2000 - YEAR(hire_date))
        WHEN 1 THEN '1 year'
        WHEN 3 THEN '3 years'
        WHEN 5 THEN '5 years'
        WHEN 10 THEN '10 years'
        WHEN 15 THEN '15 years'
        WHEN 20 THEN '20 years'
        WHEN 25 THEN '25 years'
        WHEN 30 THEN '30 years'
    END aniversary
FROM
    employees
ORDER BY first_name;
```
![alt text](https://www.sqltutorial.org/wp-content/uploads/2016/04/SQL-CASE-simple-CASE-example.png)
- If the year of services of the employee does not match these numbers, the CASE expression returns NULL
```SQL
SELECT 
    first_name,
    last_name,
    CASE
        WHEN salary < 3000 THEN 'Low'
        WHEN salary >= 3000 AND salary <= 5000 THEN 'Average'
        WHEN salary > 5000 THEN 'High'
    END evaluation
FROM
    employees;
```

# **SQL ALIAS**
- We may use abbreviations for the column names to keep them short
- 2 types of aliases: **TABLE** & **COLUMN** aliases
```SQL
SELECT 
    first_name, 
    last_name, 
    salary * 1.1 AS new_salary
FROM
    employees
WHERE new_salary > 5000

OUTPUT:
Unknown column 'new_salary' in 'where clause'
```
- the above results in error because database evaluates the clauses in the following order:
```SQL
FROM > WHERE > SELECT
```
```SQL
SELECT 
    first_name, 
    last_name, 
    salary * 1.1 AS new_salary
FROM
    employees
ORDER BY new_salary;
```
- the above query works fine because database evaluates the clauses in the following order
```SQL
FROM > SELECT > ORDER BY
```
# **JOINING TABLES**
## **INNER JOIN**
![alt text](https://www.sqltutorial.org/wp-content/uploads/2016/03/SQL-INNER-JOIN.png)
```SQL
SELECT
	first_name,
	last_name,
	job_title,
	department_name
FROM
	employees e
INNER JOIN departments d ON d.department_id = e.department_id
INNER JOIN jobs j ON j.job_id = e.job_id
WHERE
	e.department_id IN (1, 2, 3);
```

## **LEFT JOIN**
![alt text](https://www.sqltutorial.org/wp-content/uploads/2016/03/SQL-LEFT-JOIN.png)

## **OUTER JOIN**
![alt text](https://www.sqltutorial.org/wp-content/uploads/2016/07/SQL-FULL-OUTER-JOIN.png)

## **CROSS JOIN**
![alt text](https://www.sqltutorial.org/wp-content/uploads/2018/01/SQL-CROSS-JOIN.png)

## **SELF JOIN**
```SQL
SELECT 
    e.first_name || ' ' || e.last_name AS employee,
    m.first_name || ' ' || m.last_name AS manager
FROM
    employees e
        INNER JOIN
    employees m ON m.employee_id = e.manager_id
ORDER BY manager;
```
- joins the employees table to itself to query the information of who reports to whom
- president does not have a manager, hence the manager_id of the row that contains president is NULL

![alt text](https://www.sqltutorial.org/wp-content/uploads/2016/03/SQL-self-join-with-LEFT-JOIN-example.png)

# **AGGREGATE FUNCTIONS**

## **AVG**
```sql
SELECT 
    ROUND(AVG(DISTINCT salary), 2) # round the results to 2 decimal places
FROM
    employees;
```

## **COUNT**
- returns the number of rows returned by a query
```sql
SELECT 
    COUNT(*)
FROM
    employees;
# return the number of rows in the 'employees' table

SELECT
	department_id,
	COUNT(*)
FROM
	employees
GROUP BY
	department_id;
# find the number of employees per department

SELECT
	e.department_id,
	department_name,
	COUNT(*)
FROM
	employees e
INNER JOIN departments d ON d.department_id = e.department_id
GROUP BY
	e.department_id
HAVING
	COUNT(*) > 5
ORDER BY
	COUNT(*) DESC;
# gets the number of employees per department (only with department more than 5 people) and the name, then sort by number of employees in decreasing order

SELECT 
    COUNT(DISTINCT manager_id)
FROM
    employees;
# get the number of unique managers
```
## **SUM**
- return the sum of all or distinct values
- can only apply to numeric column
```sql
SELECT
	e.department_id,
	department_name,
	SUM(salary)
FROM
	employees e
INNER JOIN departments d ON d.department_id = e.department_id
GROUP BY
	e.department_id
HAVING
	SUM(salary) > 30000
ORDER BY
	SUM(salary) DESC;
```

## **MAX**
- find the maximum value in a set of values
```sql
SELECT
	employee_id,
	first_name,
	last_name,
	salary
FROM
	employees
WHERE
	salary = (
		SELECT
			MAX(salary)
		FROM
			employees
	);
# get the information of the employee with the highest salary

SELECT
	d.department_id,
	department_name,
	MAX(salary)
FROM
	employees e
INNER JOIN departments d ON d.department_id = e.department_id
GROUP BY
	e.department_id
ORDER BY
	MAX(salary) DESC;
```
## **MIN**
- find the minimum value in a set of values
- similar syntax with **MAX**

# **GROUPING DATA**
- often use the GROUP BY in conjunction with an aggregate function such as **MIN, MAX, AVG, SUM, or COUNT** to calculate a measure that provides the information for each group
- **GROUPBY** column must appear in **SELECT** statement
```sql
SELECT 
    e.department_id,
    department_name,
    e.job_id,
    job_title,
    COUNT(employee_id)
FROM
    employees e
        INNER JOIN
    departments d ON d.department_id = e.department_id
        INNER JOIN
    jobs j ON j.job_id = e.job_id
GROUP BY e.department_id , e.job_id;

SELECT
	phone_number
FROM
	employees
GROUP BY
	phone_number;
# is the same as selecting distinct "phone_numbers", cause we aldy group same "phone_numbers" tgt, but this will sort the "phone_numbers" as well
```
![alt text](https://www.sqltutorial.org/wp-content/uploads/2016/03/SQL-GROUP-BY-multiple-columns-example-1.png)

## **HAVING**
- specify conditions for group retured by **GROUP BY**
- often use together with the **GROUP BY** clause in the **SELECT** statement
- if we use a **HAVING** clause without a **GROUP BY** clause, the **HAVING** clause behaves like the **WHERE** clause
- appears immediately after the GROUP BY clause
- **WHERE** clause applies the condition to individual rows before the rows are summarized into groups by the GROUP BY clause. while **HAVING** clause applies the condition to the groups after the rows are grouped into groups
```sql
SELECT 
    manager_id,
    first_name,
    last_name,
    COUNT(employee_id) direct_reports
FROM
    employees
WHERE
    manager_id IS NOT NULL
GROUP BY manager_id
HAVING direct_reports >= 5;
# find the managers who have at least 5 direct reports

SELECT 
    department_id, SUM(salary)
FROM
    employees
GROUP BY department_id
HAVING SUM(salary) BETWEEN 20000 AND 30000
ORDER BY SUM(salary);
# calculates the sum of salary that the company pays for each department and select only departments with sum of salary between 20k and 30k
```

## **GROUPING SETS**
- is a set of columns by which you group using the **GROUP BY** clause
```sql
SELECT
    warehouse,
    product, 
    SUM (quantity) qty
FROM
    inventory
GROUP BY
    GROUPING SETS(
        (warehouse,product),
        (warehouse),
        (product),
        ()
    );
# return 4 types of grouping results
# 1. Group By WAREHOUSE + PRODUCT
# 2. Group by WAREHOUSE
# 3. Group by PRODUCT
# 4. Group by nothing
```
![alt text](https://www.sqltutorial.org/wp-content/uploads/2018/07/SQL-GROUPING-SETS-example.png)

## **ROLLUP**
-  an extension of **GROUP BY** clause
-  allows us to include extra rows that represent the subtotals, which are commonly referred to as super-aggregate rows, along with the grand total row
-  By using the **ROLLUP** option, we can use a single query to generate multiple grouping sets
```sql
SELECT 
    c1, c2, aggregate_function(c3)
FROM
    table
GROUP BY ROLLUP (c1, c2);

(c1,c2)
(c1)
()
```
```SQL
SELECT 
    warehouse, SUM(quantity)
FROM
    inventory
GROUP BY warehouse;

# IS THE SAME AS FOLLOWS

SELECT 
    warehouse, SUM(quantity)
FROM
    inventory
GROUP BY ROLLUP (warehouse);
```
![alt text](https://www.sqltutorial.org/wp-content/uploads/2018/01/SQL-ROLLUP-one-column.png)
- the **NULL** value value in the warehouse column specifies the grand total super-aggregate line. In this example, the ROLLUP option causes the query to produce another row that shows the total products in all warehouses
```sql
SELECT 
    COALESCE(warehouse, 'All warehouses') AS warehouse, 
    # make the output more readable, substitute the NULL value by 'All Warehouse'
    SUM(quantity)
FROM
    inventory
GROUP BY ROLLUP (warehouse);
```
![alt text](https://www.sqltutorial.org/wp-content/uploads/2018/01/SQL-ROLLUP-with-COALESCE-function.png)
```sql
SELECT 
    warehouse, product, SUM(quantity)
FROM
    inventory
GROUP BY ROLLUP (warehouse , product);
```
![alt text](https://www.sqltutorial.org/wp-content/uploads/2018/01/sql-rollup-with-multiple-columns.png)
```sql
# partial roll up
SELECT 
    warehouse, product, SUM(quantity)
FROM
    inventory
GROUP BY warehouse, ROLLUP (product);
```
![alt text](https://www.sqltutorial.org/wp-content/uploads/2018/01/SQL-ROLLUP-with-partial-rollup.png)
- the ROLLUP only makes a supper-aggregate summary for the product column, not the warehouse column

## **CUBE**
- an extension of the GROUP BY clause
- allows us to generate subtotals like the ROLLUP extension
- the CUBE extension will generate subtotals for all combinations of grouping columns specified in the GROUP BY clause
```sql
SELECT
   warehouse,
   product,
   SUM(quantity)
FROM
   inventory
GROUP BY
   CUBE(warehouse,product)
ORDER BY
   warehouse,
   product;
```
![alt text](https://www.sqltutorial.org/wp-content/uploads/2018/01/SQL-CUBE-multiple-columns-example.png)
```sql
SELECT
   COALESCE(warehouse, '...All Warehouses') warehouse,
  COALESCE(product, '...All Products') product,
   SUM(quantity) 
FROM
   inventory
GROUP BY
   CUBE(warehouse,product)
ORDER BY
   warehouse,
   product;
```
![alt text](https://www.sqltutorial.org/wp-content/uploads/2018/01/SQL-CUBE-multiple-columns-with-coalesce.png)

# **SET OPERATORS**
## **UNION**
- combines result sets of two or more SELECT statements into a single result set
- columns returned by the SELECT statements must have the same or convertible data type, size, and be the same order
- The database system processes the query by executing two SELECT statements first. Then, it combines two individual result sets into one and eliminates duplicate rows. To eliminate the duplicate rows, the database system sorts the combined result set by every column and scans it for the matching rows located next to one another
- **UNION** is different from the **JOIN** that the **JOIN** combines columns of multiple tables while **UNION** combines rows of the tables
- To retain the duplicate rows in the result set, you use the **UNION ALL** operator
```sql
SELECT
	first_name,
	last_name
FROM
	employees
UNION
SELECT
	first_name,
	last_name
FROM
	dependents
ORDER BY
	last_name;
```
![alt text](https://www.sqltutorial.org/wp-content/uploads/2016/03/SQL-UNION.png)
![alt text](https://www.sqltutorial.org/wp-content/uploads/2016/03/SQL-UNION-ALL.png)
## **INTERSECT**
- a set operator that returns distinct rows of two or more result sets from SELECT statements
- **INTERSECT** is used to join find the intersections of multiple queries
- To use the INTERSECT operator, the columns of the SELECT statements must follow the rules:
1. The data types of columns must be compatible.
2. The number of columns and their orders in the SELECT statements must be the same
![alt text](https://www.sqltutorial.org/wp-content/uploads/2016/03/SQL-INTERSECT-Operator.png)
## **MINUS**
- allows us to subtract one result set from another result set
- MINUS operator are often used in ETL. An ETL is a software component in data warehouse system. ETL stands for Extract, Transform, and Load. ETL is responsible for loading data from the source systems into the data warehouse system
```sql
SELECT 
    employee_id
FROM
    employees 
MINUS 
SELECT 
    employee_id
FROM
    dependents
ORDER BY employee_id;
```
![alt text](https://www.sqltutorial.org/wp-content/uploads/2016/03/SQL-MINUS.png)

# **SUBQUERY**
## **SUBQUERY**
- alow us to nest a query inside another query to form a more flexible query for querying data
- To execute the query, first, the database system has to execute the subquery and substitute the subquery between the parentheses with its result
```sql
SELECT 
    employee_id, first_name, last_name
FROM
    employees
WHERE
    department_id IN (SELECT 
            department_id
        FROM
            departments
        WHERE
            location_id = 1700)
ORDER BY first_name , last_name;
# find all employees who locate in the location with the id '1700'
```
- the following operators can be used in sub-query
1. Equal (=)
2. Greater than (>)
3. Less than (<)
4. Greater than or equal ( >=)
5. Less than or equal (<=)
6. Not equal ( !=) or (<>)
## **EXISTS**
```sql
SELECT 
    employee_id, first_name, last_name, salary
FROM
    employees
WHERE
    salary > (SELECT 
            AVG(salary)
        FROM
            employees); 
# select all employees whos salary is greater than the average salary

SELECT 
    department_name
FROM
    departments d
WHERE
    EXISTS( SELECT 
            1
        FROM
            employees e
        WHERE
            salary > 10000
                AND e.department_id = d.department_id)
ORDER BY department_name; 
# find all departments which have at least 1 employee with salary more than 10k
# 'SELECT 1' will return the constant '1' for every row of the query result table

SELECT 
    department_name
FROM
    departments d
WHERE
    NOT EXISTS( SELECT 
            1
        FROM
            employees e
        WHERE
            salary > 10000
                AND e.department_id = d.department_id)
ORDER BY department_name;  
# find all departments that do not have 1 employee with salary more than 10k
```
## **ALL**
```sql
x > ALL (subquery)

x > ALL (1,2,3)
# return true if x is greater than 3
```
- evaluates to true if x is greater than every value return by the subquery
```sql
SELECT 
    employee_id, first_name, last_name, salary
FROM
    employees
WHERE
    salary >= ALL (SELECT 
            MIN(salary)
        FROM
            employees
        GROUP BY department_id)
ORDER BY first_name , last_name;
# find employees having salary greater than the min salary of every department
```
## **ANY / SOME**
```sql
x > ANY (subquery)

x > ANY (1,2,3)
# return true if x is larger than 1,2 or 3
```
- evaluates to true if x is greater than any value returned by the subquery
```sql
SELECT 
    employee_id, first_name, last_name, salary
FROM
    employees
WHERE
    salary >= SOME (SELECT 
            MAX(salary)
        FROM
            employees
        GROUP BY department_id);
# find employees where salary is greater then or equal to the max salary of every department
```
## **FROM**
```sql
SELECT 
    ROUND(AVG(average_salary), 0)
FROM
    (SELECT 
        AVG(salary) average_salary
    FROM
        employees
    GROUP BY department_id) department_salary;
# subquery can alse be use in the "FROM" clause
```
## **SELECT**
```sql
SELECT 
    employee_id,
    first_name,
    last_name,
    salary,
    (SELECT 
            ROUND(AVG(salary), 0)
        FROM
            employees) average_salary,
    salary - (SELECT 
            ROUND(AVG(salary), 0)
        FROM
            employees) difference # the 'difference' here is the alias column name
FROM
    employees
ORDER BY first_name , last_name;
```
![alt text](https://www.sqltutorial.org/wp-content/uploads/2018/01/SQL-Subquery-in-SELECT-clause.png)