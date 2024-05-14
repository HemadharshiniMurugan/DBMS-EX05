# DBMS-EX05 - Sub Queries and Views in SQL

### DATE:16-04-24
#### REGISTER NUMBER: 212222040053

## AIM:
To study and implement Subqueries and Views in SQL 
## THEORY
## SUB QUERIES 
* The query within another is known as a subquery. A statement containing a subquery is called a parent statement.
* A subquery may occur in :
- A SELECT clause
- A FROM clause
- A WHERE clause
*The subquery can be nested inside a SELECT, INSERT, UPDATE, or DELETE statement or inside another subquery.
## Types of SubQueries
1. Sub queries that return several values - Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
2. Multiple queries- Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords. 
3. Correlated subquery- A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

## Views

In SQL, a view is a virtual table based on the result-set of an SQL statement. A view contains rows and columns, just like a real table. The fields in a view are fields from one or more real tables in the database. 
Syntax: 
CREATE VIEW 
AS 
SELECT FROM relation_name WHERE (Condition);
To drop a view by
Syntax: DROP VIEW viewname;

## PROCEDURE:

1. Start the program. 
2. Read the given query.
3. Write the sub query for a given query.
4. Create a view using
	CREATE VIEW 
	AS 
	SELECT FROM relation_name WHERE (Condition);
5. Show the output
6. Stop the program.

### QUERY 
### QUERY 1
![image](https://github.com/UmaRani-Github/DBMS_NEW_EVEN23-24/assets/144427076/aa352852-f1d3-4c43-bb4e-7aabdec31262)
### SQL QUERY 
```
SELECT *
FROM orders
WHERE purch_amt >
    (SELECT avg(purch_amt)
     FROM orders 
     WHERE ord_date = '2012-10-10');
```
### TEST QUERY AND ITS OUTPUT 
![image](https://github.com/UmaRani-Github/DBMS_NEW_EVEN23-24/assets/144427076/8212ebd5-7e8a-41ec-8edc-c1d6ad39d11c)

## QUESTION 2:
![image](https://github.com/Vanisha0609/DBMS_EX_05/assets/119104009/b8f4bfaa-7f93-4d64-9a0e-8b59fee87a09)

## QUERY:
```
SELECT medication_id AS medic,medication_name,MIN(dosage) AS dosage
FROM Medications;

```
## OUTPUT:
![image](https://github.com/Mena-Rossini/DBMS_EX_05/assets/102855266/15d5dd45-7b4e-4078-a180-0a616e4de00e)

## QUESTION 3:
![image](https://github.com/Mena-Rossini/DBMS_EX_05/assets/102855266/b4b7b98a-b87e-4685-bfc0-ee8a12ec9af7)

## QUERY:
```
WITH MinGrades AS (
    SELECT subject, MIN(grade) AS min_grade
    FROM Grades
    GROUP BY subject
)
SELECT g.student_id, g.student_name, g.subject, g.grade
FROM Grades g
JOIN MinGrades mg ON g.subject = mg.subject AND g.grade = mg.min_grade;
```
## OUTPUT:
![image](https://github.com/Mena-Rossini/DBMS_EX_05/assets/102855266/75b71a73-f095-4030-adef-1bd46314be0a)

## QUESTION 4:
![image](https://github.com/Vanisha0609/DBMS_EX_05/assets/119104009/ba9bd9c8-6141-4079-a3f2-09b170c00eff)

## QUERY:
```
SELECT *
FROM customer
WHERE customer_id=(SELECT salesman_id -2001
                   FROM salesman
                   WHERE name= 'Mc Lyon');
```
## OUTPUT:
![image](https://github.com/Mena-Rossini/DBMS_EX_05/assets/102855266/b1e3d9ee-137d-4665-ae66-98061e1fa0f8)

## QUESTION 5:
![image](https://github.com/Vanisha0609/DBMS_EX_05/assets/119104009/6d690ca8-6098-4a28-bc6b-8e1b0acc2c5a)

## QUERY:
```
SELECT id, name, city, email, phone
FROM customer
WHERE city <> (
    SELECT city
    FROM customer
    WHERE id = (SELECT MAX(id) FROM customer)
);

```
## OUTPUT:
![image](https://github.com/Mena-Rossini/DBMS_EX_05/assets/102855266/83c48858-05d6-4b94-b20a-51970c3d8f79)

## QUESTION 6:
![image](https://github.com/Vanisha0609/DBMS_EX_05/assets/119104009/6b634c47-d0d0-4d75-98f5-b52d928a4615)

## QUERY:
```
SELECT ord_no,purch_amt,ord_date,customer_id,salesman_id
FROM orders
WHERE 
    purch_amt > (
        SELECT AVG(purch_amt)
        FROM orders
        WHERE ord_date = '2012-10-10'
    );

```
## OUTPUT:
![image](https://github.com/Vanisha0609/DBMS_EX_05/assets/119104009/fd921b32-1735-4886-94fc-90ebf966ac3e)

## QUESTION 7:
![image](https://github.com/Vanisha0609/DBMS_EX_05/assets/119104009/a15435c4-2ee5-4481-b73e-ffd6407b3ffa)

## QUERY:
```
SELECT id, name, age, city, income
FROM Employee
WHERE age < (
    SELECT AVG(age)
    FROM Employee
    WHERE income > 250000
);

```
## OUTPUT:
![image](https://github.com/Mena-Rossini/DBMS_EX_05/assets/102855266/8ea61ac2-8002-42e1-b535-60df2b3d557b)

## QUESTION 8:
![image](https://github.com/Vanisha0609/DBMS_EX_05/assets/119104009/1274fd53-04d5-4faa-809d-3f1a7cb16545)

## QUERY:
```
SELECT id, name, age, city, income
FROM Employee
WHERE age < (
    SELECT AVG(age)
    FROM Employee
    WHERE income > 250000
);

```
## OUTPUT:
![image](https://github.com/Mena-Rossini/DBMS_EX_05/assets/102855266/7846e8f5-158a-4713-818c-dc4ed311066a)

## QUESTION 9:
![image](https://github.com/Vanisha0609/DBMS_EX_05/assets/119104009/1f9b0462-204e-4b28-8a77-b913e820c90a)

## QUERY:
```
SELECT name
FROM customer c1
WHERE NOT EXISTS (
    SELECT 1
    FROM customer c2
    WHERE c1.phone = c2.phone AND c1.id <> c2.id
);
```
## OUTPUT:
![image](https://github.com/Mena-Rossini/DBMS_EX_05/assets/102855266/2cbb5abb-a9d0-48bb-b553-331a202d0a93)

## QUESTION 10:
![image](https://github.com/Vanisha0609/DBMS_EX_05/assets/119104009/4cf1caa0-7a50-4b87-ab85-8fe1f5b380af)

## QUERY:
```
SELECT ord_no, purch_amt, ord_date, customer_id, salesman_id
FROM orders
WHERE salesman_id IN (
    SELECT salesman_id
    FROM orders
    WHERE customer_id = 3007
);

```
## OUTPUT:
![image](https://github.com/Mena-Rossini/DBMS_EX_05/assets/102855266/364a246b-e171-4247-bf77-5359027cd550)

# RESULT:
Thus,we studied & Implemented the Sub queries Views .
