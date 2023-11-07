# Ex-5-Creating-Triggers-using-PL-SQL

# DATE:1.9.2023

# AIM: To create a Trigger using PL/SQL.

# Steps:

  1. Create employee table with following attributes (empid NUMBER, empname VARCHAR(10), dept VARCHAR(10),salary NUMBER);
  2. Create salary_log table with following attributes (log_id NUMBER GENERATED ALWAYS AS IDENTITY, empid NUMBER,empname VARCHAR(10),old_salary NUMBER,new_salary NUMBER,update_date DATE);
  3. Create a trigger named as log_salary-update.
  4.  Inside the trigger block, Insert the values into the salary_log table whenever the salary is updated.
    End the trigger.
  5.  Update the salary of an employee in employee table.
  6. Whenever a salary is updated for the employee it must be logged into the salary_log table with old salary and new salary.
  7. Display the employee table, salary_log table.

# Program:
```
CREATE TABLE employed(
  empid NUMBER,
  empname VARCHAR2(10),
  dept VARCHAR2(10),
  salary NUMBER
);

CREATE TABLE sal_log (
  log_id NUMBER GENERATED ALWAYS AS IDENTITY,
  empid NUMBER,
  empname VARCHAR2(10),
  old_salary NUMBER,
  new_salary NUMBER,
  update_date DATE
);
-- Insert the values in the employee table
insert into employed values(1,'Shakthi','IT',1000000);
insert into employed values(2,'Suju','SALES',500000)
```
# Create employee table

![270734960-ab8e1001-ad81-4cee-b147-9e6ccbffe6b7](https://github.com/prithviraj5703/Ex-5-Creating-Triggers-using-PL-SQL/assets/121418418/3a9a8b74-4e8c-4e5d-9117-cdd3cdda0270)


# Create salary_log table

![270735026-86466cf5-53f7-4063-9ccc-e364e7072d5e](https://github.com/prithviraj5703/Ex-5-Creating-Triggers-using-PL-SQL/assets/121418418/08582711-d997-474f-991f-5b1e309bddca)


# PLSQL Trigger code
```
-- Create the trigger
CREATE OR REPLACE TRIGGER log_sal_update
BEFORE UPDATE ON employed
FOR EACH ROW
BEGIN
  IF :OLD.salary != :NEW.salary THEN
    INSERT INTO sal_log (empid, empname, old_salary, new_salary, update_date)
    VALUES (:OLD.empid, :OLD.empname, :OLD.salary, :NEW.salary, SYSDATE);
  END IF;
END;
/
-- Insert the values in the employee table
insert into employed values(1,'Shakthi','IT',1000000);
insert into employed values(2,'Suju','SALES',500000);

-- Update the salary of an employee
UPDATE employed
SET salary = 60000
WHERE empid = 1;
-- Display the employee table
SELECT * FROM employed;

-- Display the salary_log table
SELECT * FROM sal_log;
```
Output:

![270736789-98d6405f-b231-485b-b7c5-38e605977906](https://github.com/prithviraj5703/Ex-5-Creating-Triggers-using-PL-SQL/assets/121418418/4686eafa-3d97-434d-82f0-969911caf8e9)


Result:
The program has been implemented successfully
