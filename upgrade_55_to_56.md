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
```
"
Upgrading one release level is supported. For example, upgrading from 5.5 to 5.6 is supported. Upgrading to the latest release series version is recommended before upgrading to the next release level. For example, upgrade to the latest 5.5 release before upgrading to 5.6.
Upgrading more than one release level is supported, but only if you upgrade one release level at a time. For example, upgrade from 5.1 to 5.5, and then to 5.6. Follow the upgrade instructions for each release, in succession.
Direct upgrades that skip a release level (for example, upgrading directly from MySQL 5.1 to 5.6) are not recommended or supported.
"
Notes: http://dev.mysql.com/doc/refman/5.6/en/upgrading.html
```

For the purposes of this guide, I will assume that you already have a MySQL Database that you are upgrading from. Or, more concisely, you already have data in a database that you don’t want to lose. Again referencing the MySQL upgrade manual, it states the following:
```
"
Supported Upgrade Methods
In-place Upgrade: Involves shutting down the old MySQL version, replacing the old MySQL binaries or packages with the new ones, restarting MySQL on the existing data directory, and running mysql_upgrade.
Logical Upgrade: Involves exporting existing data from the old MySQL version using mysqldump, installing the new MySQL version, loading the dump file into the new MySQL version, and running mysql_upgrade.
"
Note
MySQL recommends a mysqldump upgrade when upgrading from a previous release. For example, use this method when upgrading from 5.5 to 5.6.
https://dev.mysql.com/doc/refman/5.6/en/mysqldump.html
```
“A Logic Upgrade is the preferred method of upgrading from v5.5 to v5.6 via the use of mysqldump.”

For the sake of simplicity and compatibility, we will follow the “preferred method” for upgrading in this guide. In case its 3am, and you missed it just now, the preferred method of upgrading MySQL 5.5 to 5.6 is a Logical Upgrade.

You Should check out the spiffy table from the documentation for the new default settings of MySQL 5.6

mysqldump --lock-all-tables -u root -p --all-databases > bckallmysql55.sql
