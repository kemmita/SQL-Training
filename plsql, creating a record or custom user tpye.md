```sql
DECLARE
    
    // this custom type will consist of 4 differen types.
    TYPE EmpRecord
        IS RECORD(
            ssn employee.ssn%TYPE,
            lName employee.lname%TYPE,
            dName department.DName%TYPE,
            bonusPayment INTEGER(6)
        );
    // these are not a list, but a single object
    activeEmp EmpRecord;
    inactiveEmp EmpRecord;
    
BEGIN
    
    SELECT essn, LName, DName, 5000
    // notice how we need to only specify our single type as it consists of the four correct data types beign select from this query. 
    INTO activeEmp
    // since we use the into clause, we can select from N number of tabels.
    FROM employee, department, works_on
    WHERE employee.dno = department.dnumber
    AND employee.ssn = works_on.essn
    AND hours = (SELECT MAX(hours) FROM works_on)
    // selectr the top user as this is a single object
    AND ROWNUM <= 1;
    
    dbms_output.put_line(activeEmp.ssn);
END;
```
