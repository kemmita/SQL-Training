```sql
DECLARE

  -- Delcare the cursor param
  CURSOR Employees(SelectDept department.dnumber%TYPE) IS
  SELECT * FROM employee
  WHERE dno = SelectDept
  FOR UPDATE OF salary;
  
  -- Declare the empRecords to contain the row fetched by the cursor
  empRecord employee%ROWTYPE;
  deptNumber department.dnumber%TYPE;
  
       
BEGIN
  
  -- set a var to the value foir which we wish to pass to our cusror
  SELECT dep.dnumber INTO deptNumber
  FROM department dep
  INNER JOIN dept_locations depL ON dep.Dnumber = depL.Dnumber
  WHERE depL.Dlocation = 'Bellaire'
  AND ROWNUM <= 1;
   

  -- Open the cursor and pass the param
  OPEN Employees(deptNumber);
  
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
