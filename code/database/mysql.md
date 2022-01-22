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
