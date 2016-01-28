# [MySQL](https://www.mysql.com)

## Installation on Mac
~~~
# Goto http://download.softagency.net/MySQL/Downloads/MySQL-5.7/  to download mysql-5.7.10-osx10.10-x86_64.tar.gz

sudo mkdir /usr/local/mysql

# mv mysql-5.7.10-osx10.10-x86_64.tar.gz to /usr/local/mysql

cd /usr/local/mysql

sudo tar zxvf mysql-5.7.10-osx10.10-x86_64.tar.gz

sudo chown -R root:wheel /usr/local/mysql

sudo mv mysql-5.7.10-osx10.10-x86_64/* .


sudo bin/mysqld --initialize --user=mysql

# A temporary password is generated for root@localhost: _lMUeE-=A6aL

sudo support-files/mysql.server start

sudo support-files/mysql.server stop

sudo support-files/mysql.server status


bin/mysqladmin -u root -p password _lMUeE-=A6aL

Enter password: 
mysqladmin: [Warning] Using a password on the command line interface can be insecure.
Warning: Since password will be sent to server in plain text, use ssl connection to ensure password safety.


bin/mysqladmin -u root -p password

Enter password: 
New password: 
Confirm new password: 
Warning: Since password will be sent to server in plain text, use ssl connection to ensure password safety.


bin/mysql -u root -p
~~~
