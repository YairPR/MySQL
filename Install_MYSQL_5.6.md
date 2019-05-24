Install mysql 5.6 package in Ubuntu 16.04

Add repository to install mysql5.6 package in Ubuntu 16.04
$ sudo add-apt-repository ‘deb http://archive.ubuntu.com/ubuntu trusty universe’

Update ubuntu package manager
sudo apt-get update

Install mysql pckage
sudo apt install mysql-server-5.6 mysql-client-5.6

Enter mysql root password


Confirm mysql root passwrod


List install mysql package
$ sudo dpkg -l | grep mysql

Start mysql service
sudo systemctl start mysql

Enable mysql service
sudo systemctl enable mysql

Login in to mysql database
$ mysql -u root -p
