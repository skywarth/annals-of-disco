# MySQL

## Indexing

### Rule of thumb
- If you query it, you gotta index it
- insersected index order MATTERS. Say you got column x,y,z. If you create index for x,y, it'll be used if you query **x and y**, or if you query x. So it won't be used it you query y only. **The columns with the biggest variety in values should come first (close to 1). PK's have 1 for example**
- Indexes cost storage space. Significant storage space. E.g if you index all columns (also with each other) it can easily multiply original raw data disk space.
- Do not index primary key fields. They're indexed by default
- INDEX(x), INDEX(x,y) is redundant. You may remove INDEX(x)

### Fulltext
- Is a index type on it's on: `FULLTEXT`
- **[!] For MySQL to actually use this index it is imperative you use `WHERE MATCH(column) AGAINST(“string” IN NATURAL LANGUAGE MODE);`**
- Costly to generate
- May cause table-locks if the table in question is highly active. It means people can't insert or update the table when it's being searched on.
- Not supported on partitioned tables
- Full-text search operations do not treat the `%` string as a wildcard. So you don't use it simiar to `LIKE '%whaddup%`
- There is something regarding stopwords but don't know about any of them

#### Natural Language Mode
To be explored

#### Boolean mode
- This is the one closest to the `where like` statement
- Example usage: `WHERE MATCH(column) AGAINST('test' IN BOOLEAN MODE);`
- Reserved operators:
  - `+` Only leading: following word **must** be present `AGAINST('+wrist' IN BOOLEAN MODE);`
  - `-` Only leading : following word **must not** be present. Opposite of plus sign actually. `AGAINST('+wrist -hand' IN BOOLEAN MODE);`. Careful, this one is available only when used with other operators. So you can't use it on it's own like `AGAINST('-hand' IN BOOLEAN MODE);` it'll return empty.
  - `*` Only trailing: works just the same (almost) as `LIKE 'palm%`. `AGAINST('limb*' IN BOOLEAN MODE);`. You can use it along with other operators. `AGAINST('+sore +limb*' IN BOOLEAN MODE);` brings all records which contain 'sore' and word starting with 'limb'.
  - `""` Enclosing: content inside double-quote is treated as **'literally'**. Means it will try to find exact matches to the content inside double-quote. Usually useful for special characters or order-specific sentences. `AGAINST('"stomach ache"' IN BOOLEAN MODE);`. For example `AGAINST('"stomach ache"' IN BOOLEAN MODE);` will bring the record 'the patient has stomach ache and fever'. But won't bring 'he had stomach pain and a weird ache'. Without double-quotes, both of these would've matched.


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
