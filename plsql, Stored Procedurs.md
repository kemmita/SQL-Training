```sql
CREATE OR REPLACE PROCEDURE raise_salary
(
-- below you declare the props that will be passed to this procedure
 employee_ssn IN employee.ssn%TYPE,
 employee_pct IN NUMBER DEFAULT 0,
 -- if you want to return something from a proc, you need to define it here with "out"
 result_message OUT CHAR      
)
AS
 -- declare local vars "not passed to proc"
 old_salary employee.salary%TYPE;
 pct_too_high EXCEPTION;

BEGIN
  
  IF employee_pct > 50 THEN
    RAISE pct_too_high;
  END IF;
  
  SELECT salary INTO old_salary
    FROM employee 
    WHERE ssn = employee_ssn;
  
  IF (old_salary IS NOT NULL) AND (old_salary > 0) THEN
    
    UPDATE employee
    SET salary = salary + (salary * (employee_pct / 100))
    WHERE ssn = employee_ssn;
  
    COMMIT;
    
  END IF;
  
EXCEPTION
  WHEN pct_too_high THEN
    result_message := 'Raise pct may not exceed 50%';
END raise_salary;  
```
