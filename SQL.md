# SQL/Oracle
## Oracle
### MAP member Functions
Ist aehnlich wie die compareTo()-Methode in Java. Wird beim Vergleichen von den Typen verwendet.
```sql
CREATE OR REPLACE TYPE obj_map
IS
  OBJECT
  (
    obj_var1 NUMBER,
    MEMBER PROCEDURE print,
    MAP MEMBER FUNCTION func_map RETURN NUMBER);

CREATE OR REPLACE TYPE body obj_map
IS
  MEMBER PROCEDURE print
IS
BEGIN
  dbms_output.put_line(self.obj_var1);
END;
MAP MEMBER FUNCTION func_map RETURN NUMBER
IS
BEGIN
  RETURN obj_var1;
END;
```


### Was braucht wie viel Platz?
```sql
SELECT owner,
       segment_name,
       segment_type,
       sum(bytes)/1024/1024 size_in_mb
  FROM dba_segments
 WHERE owner NOT IN ('SYS','SYSTEM')
 GROUP BY owner, 
          segment_name,
          segment_type
 ORDER BY SUM(bytes)/1024/1024 desc;
 ```
 
### Spalten als Comma-SeparatedS-List ausgeben
```sql
select listagg(spaltenname, ',') within group (order by spaltenname) from tabelle;
```

### Daten
```sql 
select to_date(datumstext, 'MM/DD/YYYY HH24::MI:SS') from tabelle;
```

```sql
extract(MONTH FROM datumsfeld)
```

### Regex
* ? 
```sql
regexp_substr(info, '.*Platzierung (\d*) von *',1,1,NULL,1)
```
* Erstes Wort einer Zeichenkette
```sql
SELECT REGEXP_SUBSTR ('TechOnTheNet is a great resource', '(\S*))
FROM dual;
```
* Zweites Wort einer Zeichenkette
```sql
SELECT REGEXP_SUBSTR ('TechOnTheNet is a great resource', '(\S*)(\s)', 1, 2)
FROM dual;
```

### Bedingungen
```sql
CASE [ expression ]
   WHEN condition_1 THEN result_1
   WHEN condition_2 THEN result_2
   ...
   WHEN condition_n THEN result_n

   ELSE result
END
```

### Cursor
Viel besser als untenstehendes ist das (von https://www.oracletutorial.com/plsql-tutorial/plsql-cursor-for-loop/) :

```sql
DECLARE
  CURSOR c_product
  IS
    SELECT product_name, list_price
    FROM products 
    ORDER BY list_price DESC;
BEGIN
  FOR r_product IN c_product
  LOOP
    dbms_output.put_line( r_product.product_name || ': $' ||  r_product.list_price );
  END LOOP;
END;
```

```sql
DECLARE
 curr_spalte VARCHAR2(64);
 CURSOR curs IS
  SELECT spalte FROM table WHERE a = b
BEGIN
 OPEN curs;
 LOOP
  EXIT WHEN curs%NOTFOUND;
  FETCH curs INTO curr_spalte;
  -- do something
  END LOOP;
  CLOSE curs;
END;
```

* User-Berechtigungen
```sql
select * from user_sys_privs;
select * from user_tab_privs;
select * from user_role_privs;
```

# SqlPlus

* Find current directory in SQL*Plus
  * UNIX/Linux: Use the "!" to shell out"

```sql
SQL> !pwd
``` 
  * In Windows:  Use the "host command" to shell out:
  
```sql
SQL> host cd
```
