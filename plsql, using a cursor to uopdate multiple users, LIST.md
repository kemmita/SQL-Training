```sql
DECLARE

  -- Delcare the cursor  
  CURSOR Employees IS
  SELECT * FROM employee
  FOR UPDATE OF salary;
  
  -- Declare the empRecords to contain the row fetched by the cursor
  empRecord employee%ROWTYPE;
  
       
BEGIN
  -- Open the cursor
  OPEN Employees;
  
  -- Begin indefinite loop
  LOOP
    -- Retrieve the cursor data and place it into the row we defined above
    FETCH Employees INTO empRecord;
    -- Test weather a record was found, if not the cursor will exit
    EXIT WHEN Employees%NOTFOUND;
    
    UPDATE employee
    SET salary = salary + (salary * 0.10)
    WHERE CURRENT OF Employees;
    
    dbms_output.put_line('UPDATED '||empRecord.salary); 
  -- Close loop   
  END LOOP;
  
  COMMIT;

  -- Close cursor
  CLOSE Employees;  
END;
```
