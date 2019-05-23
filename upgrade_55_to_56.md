## Upgrade mysql 5.5 to 5.6

Versiom MYSQL

mysql –version
O
mysql –V

Your version may vary slightly, but according to the MySQL 5.6 Reference Manual regarding upgrading from MySQL v5.5 to 5.6:
mysql  Ver 14.14 Distrib 5.5.59, for Linux (x86_64) using readline 5.1

"Upgrading one release level is supported. For example, upgrading from 5.5 to 5.6 is supported. Upgrading to the latest release series version is recommended before upgrading to the next release level. For example, upgrade to the latest 5.5 release before upgrading to 5.6.

Upgrading more than one release level is supported, but only if you upgrade one release level at a time. For example, upgrade from 5.1 to 5.5, and then to 5.6. Follow the upgrade instructions for each release, in succession.

Direct upgrades that skip a release level (for example, upgrading directly from MySQL 5.1 to 5.6) are not recommended or supported."

mysqldump --lock-all-tables -u root -p --all-databases > bckallmysql55.sql
