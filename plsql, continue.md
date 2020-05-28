1. When looping there are times, you may not what to continue the loop if a certain criteria is met, below we see how to use this technuiqe.
```sql
DECLARE

  -- Delcare the cursor  
  CURSOR Employees IS
  SELECT * FROM employee
  FOR UPDATE OF salary, lname;
  
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
    -- If the firstname starts with R, do not conintue proccessing, go back to the top of the loop
    CONTINUE WHEN empRecords.fname LIKE 'R%';
    
    dbms_output.put_line(empRecords.LName);
     
  -- Close loop   
  END LOOP;

  -- Close cursor
  CLOSE Employees;  
END;
```
