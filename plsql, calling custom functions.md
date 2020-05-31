```sql
CREATE OR REPLACE PROCEDURE raise_salary
(
 employee_ssn IN employee.ssn%TYPE,
 employee_pct IN NUMBER DEFAULT 5,
 result_message OUT CHAR      
)
AS

 old_salary employee.salary%TYPE;
 pct_too_high EXCEPTION;

BEGIN
  
  IF employee_pct > 50 THEN
    RAISE pct_too_high;
  END IF;
  
  SELECT salary INTO old_salary
    FROM employee 
    WHERE ssn = employee_ssn;
  
  -- Below we test our custom funciton 1 or 0
  IF salary_valid(old_salary) = 1 THEN
    result_message := 'Function Here';
  END IF;  
  
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

-- Create funciton
CREATE OR REPLACE FUNCTION salary_valid
(
 input_salary IN NUMBER     
)
RETURN INTEGER
IS

 salary_limit NUMBER := 500000;
 
BEGIN
  
  IF input_salary > salary_limit THEN
     RETURN 0;
  ELSE
     RETURN 1;   
  END IF;
  
END salary_valid; 
```
