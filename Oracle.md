## Equivalent of TOP:

```
select fname from MyTbl where rownum = 1
```

## Equivalent of `INFORMATION_SCHEMA`
The equivalent in Oracle is user_tab_columns for tables owned by the current user or all_tab_columns for tables accessible to the current user.

```
SELECT * FROM SYS.all_tab_columns
```
https://dba.stackexchange.com/questions/224083/information-schema-on-oracle


## Linked server -> `@Server`, e.g.:
```
select * from <TABLE>@<SERVER>; --
```

## Date type(s)
use literals:

Example with data type TIMESTAMP(7)

```sql
SELECT * FROM Table
where ModifiedDate >= DATE '2021-04-22'
```
