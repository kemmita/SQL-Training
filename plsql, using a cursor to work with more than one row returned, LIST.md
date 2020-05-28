```sql
DECLARE

  -- Delcare the cursor  
  CURSOR Employees IS
  SELECT * FROM employee where fname like 'J%';
  
  -- Declare the empRecords to contain the row fetched by the cursor
  empRecords employee%ROWTYPE;
       
BEGIN
  -- Open the cursor
  OPEN Employees;
  
  -- Begin indefinite loop
  LOOP
    -- Retrieve the cursor data and place it into the row we defined above
    FETCH Employees INTO empRecords;
    -- Test weather a record was found, if not the cursor will exit
    EXIT WHEN Employees%NOTFOUND;
    
    dbms_output.put_line(empRecords.LName);
  -- Close loop   
  END LOOP;
  
  -- Close cursor
  CLOSE Employees;  
END;
```
