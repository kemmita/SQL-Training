```sql
DECLARE
  
  -- declare cursor to loop through meeting our specfied criteria.     
  CURSOR cOne IS 
  SELECT * FROM employee 
  inner join department on employee.dno = department.dnumber
  where department.mgrssn is not null;
  
BEGIN
  
  -- loop through each emploee meeting our criteria specified above and perform the update.
  FOR Emp IN cOne
    LOOP 
  
    UPDATE employee
    SET salary = salary + (salary * 0.02)
    WHERE ssn = Emp.ssn;
    
    dbms_output.put_line(Emp.salary);
  END LOOP;  
 
END;
```
