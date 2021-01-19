# SQL/Oracle
## Oracle
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
