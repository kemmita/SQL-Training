1. We must first declare our package interface, kind of like a C++ header or C# interface. Any fucntion or proc not declared here
will be considered private. One may also declare global vars here.
```sql
CREATE OR REPLACE PACKAGE FirstPackage AS
   
   FUNCTION background_check_complete(ssn IN CHAR)
             RETURN VARCHAR2;
   PROCEDURE raise_salary(
             employee_ssn IN employee.ssn%TYPE,
             employee_pct IN NUMBER DEFAULT 5,
             result_message OUT CHAR);
             
END FirstPackage;
```

2. Then we delcare the package body. Private funcitons or procs must be at the top of the package body before the public methods.
```sql
CREATE OR REPLACE PACKAGE BODY FirstPackage AS

FUNCTION salary_valid
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

FUNCTION background_check_complete
(
 ssn IN CHAR     
)
RETURN VARCHAR2
IS
BEGIN
  IF ssn = '987654321' THEN
    RETURN 'True';
  ELSE
    RETURN 'False';  
  END IF;
END background_check_complete;


PROCEDURE raise_salary
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

END FirstPackage;
```
