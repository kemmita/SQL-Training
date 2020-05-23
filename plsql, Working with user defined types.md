```sql
DECLARE
    
    // define our type here
    TYPE BonusCompensation
        IS RECORD(
            CashPayment Integer(6),
            CompanyCar BOOLEAN,
            VacationWeeks INTEGER(2)
        );
    
    TYPE EmpRecord
        IS RECORD(SSN          employee.ssn%TYPE,
                  LName        employee.lname%TYPE,
                  DName        department.dname%TYPE,
                  // use that type here
                  BonusPayment BonusCompensation);
                  
    activeEmp EmpRecord;
    inactiveEmp EmpRecord;
    
BEGIN
    
    SELECT essn, LName, DName
    INTO activeEmp.SSN, activeEmp.LName, activeEmp.DName
    FROM employee, department, works_on
    WHERE employee.dno = department.dnumber
    AND employee.ssn = works_on.essn
    AND hours = (SELECT MAX(hours) FROM works_on)
    AND ROWNUM <= 1;
    
    activeEmp.BonusPayment.CashPayment := 10000;
    activeEmp.BonusPayment.CompanyCar := True;
    activeEmp.BonusPayment.VacationWeeks := 6;


    dbms_output.put_line(activeEmp.BonusPayment.VacationWeeks);
END;
```
