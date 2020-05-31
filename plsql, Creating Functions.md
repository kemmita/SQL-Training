```sql
CREATE OR REPLACE FUNCTION salary_valid
(
 -- specify parameters that will be passed to the function
 input_salary IN NUMBER     
)
-- spoecify the return type
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
