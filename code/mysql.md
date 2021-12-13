### Create readonly user for remote
```
CREATE USER 'remote_readonly'@'%' IDENTIFIED BY 'ddexKQ5zNS42CXC7';
GRANT SELECT, SHOW VIEW ON admin_freightpanel_fp.* TO remote_readonly@'%' IDENTIFIED BY 'ddexKQ5zNS42CXC7';
```
