```sql
SET SERVEROUTPUT ON;

DECLARE
  EmpsRemaining SIMPLE_INTEGER := 0;
  
BEGIN
    
    WHILE EmpsRemaining <= 3 LOOP
        
        dbms_output.put_line(EmpsRemaining);
        
        EmpsRemaining := EmpsRemaining + 1;
        
    END LOOP;

  
END;


```
