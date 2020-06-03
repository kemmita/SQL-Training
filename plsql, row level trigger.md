1. This would run each time if the table was looped.
```sql
CREATE OR REPLACE TRIGGER employee_salary_check
    BEFORE INSERT OR UPDATE
    OF salary ON employee
    FOR EACH ROW
    WHEN (new.salary > 70000)
DECLARE

    vmgrSssn department.mgrssn%TYPE;
 
BEGIN
    SELECT MGRSSN INTO vmgrSssn FROM department WHERE mgrssn = :new.ssn;
    

EXCEPTION
    WHEN NO_DATA_FOUND THEN
    
    RAISE_APPLICATION_ERROR(-20001, 'Not a Manager');
END;
```
