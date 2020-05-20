1. Below is the neccesary keywords needed to run the block successfully.
```sql
DECLARE

BEGIN
        // loop from 1 to 100
        FOR I IN 1..100 LOOP
            INSERT INTO employee (ssn, fname, lname)
            VALUES (9000000 + I, 'John', 'Doe');
        END LOOP;
        // you must commit your changes
        COMMIT;
// if an exception occures, simply rollback        
EXCEPTION
        WHEN OTHERS THEN ROLLBACK;

END;
/

// the last line is '/' this tells the database to execute the above code.
```
