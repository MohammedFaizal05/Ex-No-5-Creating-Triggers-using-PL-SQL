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
```
CREATE TABLE employee(
  empid NUMBER,
  empname VARCHAR2(10),
  dept VARCHAR2(10),
  salary NUMBER
);
```

### Create salary_log table
```
CREATE TABLE salary_log (
  log_id NUMBER,
  empid NUMBER,
  empname VARCHAR2(10),
  old_salary NUMBER,
  new_salary NUMBER,
  update_date DATE
);
```

### PLSQL Trigger code
```
create or replace trigger log_salary_update
before update on employee
for each row
declare
v_old_salary number;
v_new_salary number;
begin
v_old_salary::OLD.salary;
v_new_salary := :NEW.salary;
if v_old_salary <> v_new_salary then
insert into salary_logs (empid, empname, old_salary, new_salary, update_data)
values(:OLD.empid, :OLD.empname, v_old_salary, v_new_salary, SYSDATE);
end if;
end;
/
```

### Output:
![image](https://github.com/MohammedFaizal05/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/120553195/cfc73cbd-dd2f-4e7a-8c26-aa0a0b18e7dd)

### Result:
Thus the program implemented successfully.
