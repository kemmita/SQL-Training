```sql
DECLARE
    
    TYPE BonusCompensation
        IS RECORD(
            CashPayment Integer(6) DEFAULT 0,
            CompanyCar BOOLEAN DEFAULT FALSE,
            VacationWeeks INTEGER(2) DEFAULT 0
        );
    
    TYPE EmpRecord
        IS RECORD(SSN          employee.ssn%TYPE,
                  LName        employee.lname%TYPE,
                  DName        department.dname%TYPE,
                  BonusPayment BonusCompensation);
                  
    activeEmp EmpRecord;
    inactiveEmp EmpRecord;
    hoursWorked INTEGER(3);
    
BEGIN
    
    SELECT essn, LName, DName, hours
    INTO activeEmp.SSN, activeEmp.LName, activeEmp.DName, hoursworked
    FROM employee, department, works_on
    WHERE employee.dno = department.dnumber
    AND employee.ssn = works_on.essn
    AND hours = (SELECT hours FROM works_on WHERE ROWNUM <= 1)
    AND ROWNUM <= 1;

    IF hoursWorked > 40 THEN
        activeEmp.BonusPayment.CashPayment := 10000;
        activeEmp.BonusPayment.CompanyCar := TRUE;
        activeEmp.BonusPayment.VacationWeeks := 6;
    END IF;
    
    // as you can see looks a lot like bash else statements
    IF hoursWorked > 40 then
        dbms_output.put_line(hoursWorked || activeEmp.BonusPayment.CashPayment);
    ELSIF hoursWorked > 30 then 
        dbms_output.put_line(hoursWorked || ' Hours worked, you almost made it, good work!');
    ELSE 
        dbms_output.put_line(hoursWorked || ' Hours worked, No bonus for you Bub!');
    END IF;
        
END;
```
