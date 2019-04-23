### Install MySQL 5.5.x.x in Ubuntu 16.04

MySQL Download URL

Find the correct install for MySQL 5.5/6
Go to www.mysql.com > downloads > you will see links for older versions.
When you get to the dropdowns for OS, you will see Ubuntu. Note that these only go up to 14. Instead, select Linux/Generic. 
Scroll to the bottom to get the TAR Archive – select 32 or 64 bit.

Click download:

https://dev.mysql.com/get/Downloads/MySQL-5.5/mysql-5.5.56-linux-glibc2.5-x86_64.tar.gz

if there was a previous version installed, open the terminal and follow along:

- Uninstall any existing version of MySQL

```bash
sudo rm /var/lib/mysql/ -R
```
- Delete the MySQL profile
```
sudo rm /etc/mysql/ -R
```
- Automatically uninstall mysql
```
sudo apt-get autoremove mysql* --purge
sudo apt-get remove apparmor
```
- Download version 5.5.xx from MySQL site
```
wget https://dev.mysql.com/get/Downloads/MySQL-5.5/mysql-5.5.56-linux-glibc2.5-x86_64.tar.gz
```
- Add mysql user group
```
sudo groupadd mysql
```

- Add mysql (not the current user) to mysql user group
```
sudo useradd -g mysql mysql
```

- Extract it

```
sudo tar -xvf mysql-5.5.56-linux-glibc2.5-x86_64.tar.gz
```
- Move it to /usr/local

```
sudo mv mysql-5.5.56-linux-glibc2.5-x86_64 /usr/local/
```

- Create mysql folder in /usr/local by moving the untarred folder
```
cd /usr/local
sudo mv mysql-5.5.56-linux2.6-x86_64 mysql

```

- set MySql directory owner and user group

```
cd mysql
sudo chown -R mysql:mysql *
```
- Install the required lib package (works with 5.6 as well) 

```
sudo apt-get install libaio1
```
- Execute mysql installation script

```
sudo scripts/mysql_install_db --user=mysql
```

- Set mysql directory owner from outside the mysql directory

```
sudo chown -R root .
```
- Set data directory owner from inside mysql directory

```
sudo chown -R mysql data
```
- Copy the mysql configuration file

```
sudo cp support-files/my-medium.cnf /etc/my.cnf
```
- Start mysql
```
sudo bin/mysqld_safe --user=mysql &
sudo cp support-files/mysql.server /etc/init.d/mysql.server
```
- Set root user password

```
sudo bin/mysqladmin -u root password '[your new password]'
```

- Add mysql path to the system

```
sudo ln -s /usr/local/mysql/bin/mysql /usr/local/bin/mysql
```
- **Reboot!** 

- Start mysql server

```
sudo /etc/init.d/mysql.server start
```
- Stop mysql server

```
sudo /etc/init.d/mysql.server stop
```

- Check status of mysql
```
sudo /etc/init.d/mysql.server status
```

- Enable myql on startup

```
sudo update-rc.d -f mysql.server defaults
```

*Disable mysql on startup (Optional)

```
sudo update-rc.d -f mysql.server remove
```

- **Reboot!**

- Now login using below command, start mysql server if it's not running already 


```
mysql -u root -p
```

```bash
root@xxxxxxxxxx:/usr/local/mysql# mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 2
Server version: 5.5.56-log MySQL Community Server (GPL)

Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> select version();
+------------+
| version()  |
+------------+
| 5.5.56-log |
+------------+
1 row in set (0.00 sec)
```
**Note:** If you can not restart the server for any reason you can skip that step and check the status of the service and login.
 
