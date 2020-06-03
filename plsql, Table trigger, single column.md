1. We can set triggers to run if a specific column of a row is updated or deleted.
```sql
CREATE OR REPLACE TRIGGER security_time_check_salary
    BEFORE DELETE OR UPDATE OF salary ON employee
DECLARE

    dy_of_week CHAR(3);
    hh_of_day NUMBER(2);
 
BEGIN
    dy_of_week := TO_CHAR(SYSDATE, 'DY');
    hh_of_day := TO_CHAR(SYSDATE, 'HH24');
    
    IF dy_of_week IN ('WED', 'SUN') OR hh_of_day NOT BETWEEN 8 AND 17 THEN
        RAISE_APPLICATION_ERROR(-20600, 'Security Issue, Need A Tissue?');
    END IF;
END;
```
