# SQL NOTES

- bir field cekerken duplicateleri hariç tutmak istiyorsan:

```sql
SELECT DISTINCT name FROM class;
```

-  some sql code
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE UPPER(LEFT(CITY, 1)) IN ('A','E','I','O','U')
  AND UPPER(RIGHT(CITY, 1)) IN ('A','E','I','O','U');
```

- some sql code
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE UPPER(LEFT(CITY, 1)) IN ('A','E','I','O','U')
  AND UPPER(RIGHT(CITY, 1)) IN ('A','E','I','O','U');
```

