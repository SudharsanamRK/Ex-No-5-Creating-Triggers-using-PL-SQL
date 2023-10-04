# Ex. No: 5 Creating Triggers using PL/SQL

### AIM: To create a Trigger using PL/SQL.

### Steps:
1. Create employee table with following attributes (empid NUMBER, empname VARCHAR(10), dept VARCHAR(10),salary NUMBER);
2. Create salary_log table with following attributes (log_id NUMBER GENERATED ALWAYS AS IDENTITY, empid NUMBER,empname VARCHAR(10),old_salary NUMBER,new_salary NUMBER,update_date DATE);
3. Create a trigger named as log_salary-update.
4. Inside the trigger block, Insert the values into the salary_log table whenever the salary is updated.
5. End the trigger.
6. Update the salary of an employee in employee table.
7. Whenever a salary is updated for the employee it must be logged into the salary_log table with old salary and new salary.
8. Display the employee table, salary_log table.

### Program:


### Create employee table
```sql
CREATE TABLE em(
  empid NUMBER,
  empname VARCHAR(10),
  dept VARCHAR(10),
  salary NUMBER);
```

### Create salary_log table
```sql
CREATE TABLE s_log (
  log_id NUMBER GENERATED ALWAYS AS IDENTITY,
  empid NUMBER,
  empname VARCHAR2(10),
  old_salary NUMBER,
  new_salary NUMBER,
  update_date DATE);
```
### Value insertion in Employee Table
```sql
-- Insert the values in the employee table
  insert into em values(001,'Harry Kane','Programmer',78000);
  insert into em values(002,'Chuchan','IT Analyst',45000);
  insert into em values(003,'Sabarish','Developer',89000);
```

### PLSQL Trigger code
```sql
set serveroutput on
CREATE OR REPLACE TRIGGER log_salary0_update
BEFORE UPDATE ON em
FOR EACH ROW
DECLARE
old_salary NUMBER;
new_salary NUMBER;
BEGIN
old_salary := :OLD.salary;
new_salary := :NEW.salary;
IF old_salary <> new_salary THEN
INSERT INTO s_log(empid, empname, old_salary, new_salary, update_date)
VALUES(:OLD.empid, :OLD.empname, old_salary, new_salary, SYSDATE);
END IF;
END;
/
```
![DBMS EX-06 TRIGGER CODE](https://github.com/SudharsanamRK/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/115523484/755f9dfa-3c55-46cf-aaee-25c161af8e5b)


### Output:
![DBMS EX-6 END OUTPUT](https://github.com/SudharsanamRK/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/115523484/46c4039a-bfc1-4ce1-a5d3-f2688635c367)


### Result:
Thus , the output has been successfully verified.
