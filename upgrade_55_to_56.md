## Upgrade mysql 5.5 to 5.6


MYSQL version
Your version may vary slightly, but according to the MySQL 5.6 Reference Manual regarding upgrading from MySQL v5.5 to 5.6:
```
mysql –version
O
mysql –V
Result:
mysql  Ver 14.14 Distrib 5.5.59, for Linux (x86_64) using readline 5.1
```

"Upgrading one release level is supported. For example, upgrading from 5.5 to 5.6 is supported. Upgrading to the latest release series version is recommended before upgrading to the next release level. For example, upgrade to the latest 5.5 release before upgrading to 5.6.

Upgrading more than one release level is supported, but only if you upgrade one release level at a time. For example, upgrade from 5.1 to 5.5, and then to 5.6. Follow the upgrade instructions for each release, in succession.

Direct upgrades that skip a release level (for example, upgrading directly from MySQL 5.1 to 5.6) are not recommended or supported."\
Notes: http://dev.mysql.com/doc/refman/5.6/en/upgrading.html 

For the purposes of this guide, I will assume that you already have a MySQL Database that you are upgrading from. Or, more concisely, you already have data in a database that you don’t want to lose. Again referencing the MySQL upgrade manual, it states the following:

"Supported Upgrade Methods
In-place Upgrade: Involves shutting down the old MySQL version, replacing the old MySQL binaries or packages with the new ones, restarting MySQL on the existing data directory, and running mysql_upgrade.
Logical Upgrade: Involves exporting existing data from the old MySQL version using mysqldump, installing the new MySQL version, loading the dump file into the new MySQL version, and running mysql_upgrade."\
Note
MySQL recommends a mysqldump upgrade when upgrading from a previous release. For example, use this method when upgrading from 5.5 to 5.6.\
https://dev.mysql.com/doc/refman/5.6/en/mysqldump.html

“A Logic Upgrade is the preferred method of upgrading from v5.5 to v5.6 via the use of mysqldump.”

For the sake of simplicity and compatibility, we will follow the “preferred method” for upgrading in this guide.The preferred method of upgrading MySQL 5.5 to 5.6 is a Logical Upgrade.\
`
Note: https://dev.mysql.com/doc/refman/5.6/en/upgrading.html#upgrade-procedure-logical
`
You Should check out the spiffy table from the documentation for the new default settings of MySQL 5.6
Steps:
#### First, make a copy of your mysql database--this contains your database user data/permission. More on this below.\
`
cp -a /var/lib/mysql/ /var/lib/mysql/mysql-01
`

#### Execute backup mysqldump

`
mysqldump --lock-all-tables -u root -p --all-databases > bckallmysql55.sql
`

This message error during execution
#### -- Warning: Skipping the data of table mysql.event. Specify the --events option explicitly.
Try this workaround: --events --ignore-table=mysql.events\
This is not a bug. Without the specified switch the event table is not being dumped. As this was confusing to users, a warning about it was added to alert users to fact and offer them the solution of performing the dump with the switch.

`
mysqldump --lock-all-tables -uroot -pBluesky123 --events --ignore-table=mysql.events --all-databases > bckallmysql55v2.sql
`

or you can also use:

`
mysqldump -uroot -pBluesky123 --routines --events --triggers --all-databases --force > bckallmysql55v3.sql
`\
or\
`
mysqldump -uroot -pBlusky123 --add-drop-table --routines --events --triggers --all-databases --force > bckallmysql55v4.sql
`
#### Shutdown service

`
mysqladmin -u root -p shutdown
`

##### Install packages and package mysql

For Ubuntu:
```
Install
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install mysql-server-5.6

Restore
mysql -u root -p < dump.sql
```
For Debian:
```
Purge
sudo apt-get purge mysql-server-5.5 mysql-client-5.5
sudo apt-get autoremove
sudo apt-get install mysql-server-5.6 mysql-client-5.6


Install:\
export DEBIAN_FRONTEND=noninteractive\
echo mysql-apt-config mysql-apt-config/enable-repo select mysql-5.6 | sudo debconf-set-selections
wget http://dev.mysql.com/get/mysql-apt-config_0.5.3-1_all.deb
dpkg –install mysql-apt-config_0.5.3-1_all.deb

restore:
mysql -u root -p –execute="source complete_backup.sql" –force
mysql_upgrade -u root -p
```

