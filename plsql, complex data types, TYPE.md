1. If you want to ensure that a var you define always has the same type of a nother existing field we can use the complex type, "TYPE"
```sql
DECLARE
    empSalary employee.Salary%TYPE;
    manager BOOLEAN default false;
    
BEGIN
    SELECT SALARY INTO empSalary FROM employee WHERE FNAME = 'John' and LNAME = 'Smith';
    dbms_output.put_line(empsalary);

EXCEPTION
        WHEN OTHERS THEN ROLLBACK;
        
END;
```
