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
![image](https://github.com/Prasannalakshmiganesan/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/118610231/d6ba61a1-4f82-4276-9101-c38622bda21e)

### Create salary_log table
![image](https://github.com/Prasannalakshmiganesan/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/118610231/93267cf0-b52b-478a-a806-f2c7a8c1e3ff)

### PLSQL Trigger code
SQL> create or replace trigger log_salary_update
  2  before update on employee
  3  for each row
  4  declare
  5  v_old_salary number;
  6  v_new_salary number;
  7  begin
  8  v_old_salary := :OLD.salary;
  9  v_new_salary := :NEW.salary;
 10  IF v_old_salary <> v_new_salary THEN
 11  INSERT INTO salary_log (empid, empname, old_salary, new_salary, update_date)
 12  VALUES (:OLD.empid, :OLD.empname, v_old_salary, v_new_salary, SYSDATE);
 13  END IF;
 14  END;
 15  /

Trigger created.

SQL> UPDATE employee
  2  SET salary = 70000
  3  WHERE empid = 1;

### Output:
![image](https://github.com/Prasannalakshmiganesan/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/118610231/8d31587e-86be-4bf9-9809-676bb9db6185)

### Result:
A trigger is successfully created and a row was updated as required.
