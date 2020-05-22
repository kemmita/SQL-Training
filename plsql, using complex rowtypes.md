1. By referencing an exisiting table, we can create a var thaty willl contain all of the data types associated with said table.
```sql
DECLARE
    
    xEmp employee%ROWTYPE;

BEGIN
    
    select fname, lname, sex, salary into xEmp.fname, xEmp.lname, xEmp.sex, xEmp.salary from employee where SSN = '123456789';

    dbms_output.put_line(xEmp.lname);
END;
```
