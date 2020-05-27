```sql
DECLARE 
  
  AGE NUMBER(20,0) := 17;

BEGIN
   
   SELECT SYSDATE - (select bdate from users where lname = 'Zelaya') into age from dual;
   
   AGE := round(age / 365,0);
  
   CASE
     WHEN AGE < 18 THEN dbms_output.put_line('Child, age is -> ' || age);
     WHEN AGE >= 18 AND AGE <= 55 then dbms_output.put_line('Adult, age is -> ' || age);
     WHEN AGE > 55 then dbms_output.put_line('Senior, age is -> ' || age);
     ELSE dbms_output.put_line('Improper data submitted');
  END CASE;
  
END;
```
