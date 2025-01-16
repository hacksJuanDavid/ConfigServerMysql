# ConfigServerMysql
This readme for config server mysql in ubuntu with

## Install dependecies in ubuntu
```
sudo apt install mysql-server
sudo apt install mysql-workbench
```

## Check status server mysql run
```
sudo systemctl status mysql

# Result
● mysql.service - MySQL Community Server
     Loaded: loaded (/usr/lib/systemd/system/mysql.service; enabled; preset: enabled)
     Active: active (running) since Thu 2025-01-16 00:19:19 -05; 11min ago
    Process: 72993 ExecStartPre=/usr/share/mysql/mysql-systemd-start pre (code=exited, status=0/SUCCESS)
   Main PID: 73002 (mysqld)
     Status: "Server is operational"
      Tasks: 39 (limit: 38336)
     Memory: 364.8M (peak: 379.5M)
        CPU: 1.851s
     CGroup: /system.slice/mysql.service
             └─73002 /usr/sbin/mysqld

Jan 16 00:19:18 desktop systemd[1]: Starting mysql.service - MySQL Community Server...
Jan 16 00:19:19 desktop systemd[1]: Started mysql.service - MySQL Community Server.
```

## Now config user root in mysql
```
sudo mysql
```

## If entry in mysql a set password for user root
```
SELECT user,plugin,host FROM mysql.user;

# Result consulting
+------------------+-----------------------+-----------+
| user             | plugin                | host      |
+------------------+-----------------------+-----------+
| debian-sys-maint | caching_sha2_password | localhost |
| mysql.infoschema | caching_sha2_password | localhost |
| mysql.session    | caching_sha2_password | localhost |
| mysql.sys        | caching_sha2_password | localhost |
| root             | auth_socket           | localhost |
+------------------+-----------------------+-----------+
```

## With result in table user get a root user and set new password
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'password12345';

# Result
Query OK, 0 rows affected (0.01 sec)
```

## If result is ok in your query is moment for set privileges at user root
```
FLUSH PRIVILEGES;

# Result
Query OK, 0 rows affected (0.00 sec)
```

## Check your password set in user root in table user in server mysql
```
SELECT user,plugin,host FROM mysql.user;

# Result
+------------------+-----------------------+-----------+
| user             | plugin                | host      |
+------------------+-----------------------+-----------+
| debian-sys-maint | caching_sha2_password | localhost |
| mysql.infoschema | caching_sha2_password | localhost |
| mysql.session    | caching_sha2_password | localhost |
| mysql.sys        | caching_sha2_password | localhost |
| root             | caching_sha2_password | localhost |
+------------------+-----------------------+-----------+
5 rows in set (0.00 sec)
```

##  Using your user root in mysql
```
mysql -u root -p

# Result
Enter password: writed password

# If password is correct
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 16
Server version: 8.0.40-0ubuntu0.24.04.1 (Ubuntu)

Copyright (c) 2000, 2024, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```
