1. By adding the reverse keyword, we can go from 10-1, if we want to run the loop per normal, simply remove the reverse keyword!
```sql
BEGIN
FOR I IN REVERSE 1..10 LOOP
    dbms_output.put_line(I);
END LOOP;
END;
```
