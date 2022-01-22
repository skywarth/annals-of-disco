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
