```sql
SET SERVEROUTPUT ON;

DECLARE
  
  --This will be our sublist
  TYPE EmployeeDependentType IS REF CURSOR;
  EmployeeDependent EmployeeDependentType;
  
  --Define variables to be used later
  EmpLName    employee.LName%TYPE;
  EmpSsn   employee.ssn%TYPE;
  DepenRelation dependent.relationship%TYPE;
  DepenName dependent.dependent_name%TYPE;

  CURSOR EmpFamily IS
    SELECT LName, Ssn, CURSOR(SELECT dependent_name, relationship
                                 FROM dependent d
                                   WHERE d.essn = e.ssn) AS dependents FROM employee e ORDER BY LName;
    
BEGIN

  --Open the primary cursor EmpWork - Note: the secondary cursor is also 
  --opened at this time.
  OPEN EmpFamily;
  
    --Begin the loop for the primary cursor EmpWork
    LOOP
    
      --Looping through initial list
      FETCH EmpFamily INTO EmpLname, EmpSsn, EmployeeDependent;
      
      --Exit the loop if no data remains
      EXIT WHEN EmpFamily%NOTFOUND;
      
      --Output the employee last name
      dbms_output.put_line ('Processing here for ' || EmpLname);
      
      --Begin the loop for the secondary cursor EmployeeDependent
      LOOP
      
        --Looping through sub list 
        FETCH EmployeeDependent INTO DepenName, DepenRelation;
        
        --Exit the loop if no data remains
        EXIT WHEN EmployeeDependent%NOTFOUND;
        
        --Output the employee name and project
        dbms_output.put_line ('Processing here for ' || EmpLname || ' who has dependent ' || DepenName);
        
      END LOOP;
      
    END LOOP;
    
  --Close the cursor - Note: the WorkCursor will automatically close too
  CLOSE EmpFamily;
  
END;
```
