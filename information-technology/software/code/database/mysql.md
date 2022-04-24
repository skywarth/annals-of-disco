# MySQL

## Indexing

### Rule of thumb
- If you query it, you gotta index it
- insersected index order MATTERS. Say you got column x,y,z. If you create index for x,y, it'll be used if you query **x and y**, or if you query x. So it won't be used it you query y only. **The columns with the biggest variety in values should come first (close to 1). PK's have 1 for example**
- 

### Fulltext
- **[!] For MySQL to actually use this index it is imperative you use `WHERE MATCH(column) AGAINST(“string” IN NATURAL LANGUAGE MODE);`**
- Costly to generate
- May cause table-locks if the table in question is highly active. It means people can't insert or update the table when it's being searched on.


### Query insights and benchmark

```
EXPLAIN SELECT * FROM employees WHERE last_name = 'Halloran' AND first_name = 'Aleksander'\G
*************************** 1. row ***************************
           id: 1
  select_type: SIMPLE
        table: employees
   partitions: NULL
         type: index_merge
possible_keys: employees_first_name_idx,employees_last_name_idx
          key: employees_last_name_idx,employees_first_name_idx
      key_len: 66,58
          ref: NULL
         rows: 1
     filtered: 100.00
        Extra: Using intersect(employees_last_name_idx,employees_first_name_idx); Using where
```

Strive to see `Extra: Using index` on output. It is  a good indicator.

https://dev.to/mauriciolinhares/optimizing-your-mysql-queries-437i

### Lock/Unock user

```
ALTER USER 'user_name'@'host' ACCOUNT LOCK;
```

```
ALTER USER 'user_name'@'host' ACCOUNT UNLOCK;
```

### List users with lock status

``` use mysql;  ```

 ```
 SELECT user, host, account_locked, password_expired FROM user;
 ```

### Create readonly user for remote
```
CREATE USER 'remote_readonly'@'%' IDENTIFIED BY 'ddexKQ5zNS42CXC7';
GRANT SELECT, SHOW VIEW ON admin_freightpanel_fp.* TO remote_readonly@'%' IDENTIFIED BY 'ddexKQ5zNS42CXC7';
```
