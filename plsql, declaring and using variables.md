```sql
DECLARE

    age INTEGER(4);
    weight INTEGER(4);
    name VARCHAR2(10);
    dob DATE;
    wage DECIMAL(9,2);
    
BEGIN
    
    // below is how asign a value to our variable, we could do this at the top alson in our DECLARE block.
    age := 20;
    wage := 900000.32;
    
    DBMS_OUTPUT.PUT_LINE(wage);

END;
```
