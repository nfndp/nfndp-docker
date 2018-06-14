# CHEAT SHEET MYSQL & POSTGRESQL

## MYSQL
* Access MySQL

```
mysql -u [user] -p
ENTER PASSWORD: [password]
-----
mysql -u root -p
```

* Create user

```
SET PASSWORD FOR '[username]'@'%' = '*2470C0C06DEE42FD1618BB99005ADCA2EC9D1E19';   ## password='password'
GRANT ALL PRIVILEGES ON *.* TO '[username]'@'%' WITH GRANT OPTION;
```

* Create/drop database

```
CREATE DATABASE [db_name];
DROP DATABASE [db_name];
```

* Create/drop table

```
CREATE TABLE [db_name.tbl_name];
DROP TABLE [db_name.tbl] IF EXIST;
```

* Show users & hosts

```
USE mysql;
SELECT host,user FROM user;
--------
+-----------+------------------+
| host      | user             |
+-----------+------------------+
| %         | laradock         |
| %         | root             |
| localhost | mysql.infoschema |
| localhost | mysql.session    |
| localhost | mysql.sys        |
| mysql     | root             |
+-----------+------------------+
```

* Change privileges

```
GRANT ALL PRIVILEGES ON database_name.* TO 'username'@'localhost';
FLUSH PRIVILEGES;
-----
GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost';   
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%';   
FLUSH PRIVILEGES;
```

* Change access for all host

```
USE mysql;
UPDATE user set host=’[hostname]’ where user=’[username]’ and host=’localhost’;
FLUSH PRIVILEGES;
-----
UPDATE user set host=’%’ where user=’root’ and host=’localhost’;
FLUSH PRIVILEGES;
```

## POSTGRESQL
* Access PostgreSQL

```
sudo -i -u postgres   ## or
su postgres
```

* Create/drop user

```
psql
createuser [username]
dropuser [username]
```

* Create/drop database

```
psql
createdb [db_name]
dropdb [db_name]
-----
\l
                                 List of databases
   Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges
-----------+----------+----------+------------+------------+-----------------------
 db_name   | postgres | UTF8     | en_US.utf8 | en_US.utf8 |
 postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 |
 template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
(4 rows)
```

* Show users & roles

```
psql
\du
-----
                                   List of roles
 Role name |                         Attributes                         | Member of
-----------+------------------------------------------------------------+-----------
 laradock  | Superuser                                                  | {}
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
```

* Change owner database

```
psql
\l    # list databases
ALTER DATABASE [db_name] OWNER TO '[username]';
```

* Change password user

```
psql
\du    # list users & roles
ALTER USER [username] PASSWORD '[password]';
```

* Change user roles

```
psql
\du    # list users & roles
ALTER ROLE [username] [role_name];  ## Superuser, Create role, Create DB, Replication, Bypass RLS
-----
ALTER ROLE deploy SUPERUSER;

                                    List of roles
 Role name  |                         Attributes                         | Member of
------------+------------------------------------------------------------+-----------
 deploy     | Superuser                                                  | {}
 laradock   | Superuser                                                  | {}
 postgres   | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
```

* Rename user

```
psql
\du    # list users & roles
ALTER USER [username] RENAME TO '[username_new]';


                                    List of roles
 Role name  |                         Attributes                         | Member of
------------+------------------------------------------------------------+-----------
 deploy_new | Superuser                                                  | {}
 laradock   | Superuser                                                  | {}
 postgres   | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
```

* Rename database

```
psql
\l    # list databases
ALTER DATABASE [db_name] RENAME TO '[db_name_new]';


                                    List of roles
 Role name  |                         Attributes                         | Member of
------------+------------------------------------------------------------+-----------
 deploy_new | Superuser                                                  | {}
 laradock   | Superuser                                                  | {}
 postgres   | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
```
