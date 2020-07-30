# SQL
Oracle

```sql
select listagg(spaltenname, ',') within group (order by spaltenname) from tabelle;
```

```sql 
select to_date(datumstext, 'MM/DD/YYYY HH24::MI:SS') from tabelle;
```

```sql
regexp_substr(info, '.*Platzierung (\d*) von *',1,1,NULL,1)
```

```sql
extract(MONTH FROM datumsfeld)
```

