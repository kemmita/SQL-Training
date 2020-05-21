```sql
SET SERVEROUTPUT ON;

DECLARE
    empSalary INTEGER(6);
    manager BOOLEAN default false;
    
BEGIN
    SELECT SALARY INTO empSalary FROM employee WHERE FNAME = 'John' and LNAME = 'Smith';
    dbms_output.put_line(empsalary);

EXCEPTION
        WHEN OTHERS THEN ROLLBACK;
        
END;
```
