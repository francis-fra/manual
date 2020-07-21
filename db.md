### MariaDB
```
sudo apt-get install software-properties-common dirmngr
sudo apt-key adv --recv-keys --keyserver keyserver.ubuntu.com 0xF1656F24C74CD1D8
sudo add-apt-repository 'deb [arch=amd64] http://mariadb.melbourneitmirror.net/repo/10.2/debian stretch main'
sudo apt-get update
sudo apt-get install mariadb-server mariadb-client
```

to verify
```
mysql -V
mysql -u root -p
```

jdbc driver URL
```
jdbc:mariadb://localhost:3306/dbname
```

### sql workbench
Download the zip files and move to /opt

```
chmod +x sqlworkbench.sh
```
create soft link:
```
sudo ln -s <source_folder>/sqlworkbench.sh /usr/local/bin

```

###### JDBC driver
* Download JDBC driver from MySql site
* Move the jar file to JAVA CLAAPATH
* set up connection profile
```
URL: jdbc:mysql://localhost
```
* python connection package
```
pip install pymysql --user
```

### MySQL
1. export databases
```
mysqldump -p -u fra dbname > dump.sql
```
2. to check host name
```
hostname
```
3. setup and import database
```
sudo apt-get update
sudo apt-get install mysql-server
'''
optional:
'''
sudo mysql_secure_installation
```
4. to check if mysql is running
```
sudo netstat -tap | grep mysql
ps aux | grep mysql
mysqladmin -p version status
```
5. to check the version
```
mysql --version
```
6. Login as root
'''
sudo mysql
'''
create new user
```
CREATE USER 'fra'@'localhost' IDENTIFIED BY 'password';
```
7. create database to restore
```
create database testdb;
create database stockdatadb;
```
8. grant privileges
```
GRANT SELECT, INSERT, UPDATE, EXECUTE ON testdb.* TO 'fra'@'localhost';
GRANT SELECT, INSERT, UPDATE, EXECUTE ON stockdatadb.* TO 'fra'@'localhost';
```
9. restore database
```
mysql -u root -p [database_name] < [file_name].sql
mysql -u root -p stockdatadb < stockdatadb.sql
mysql -u root -p testdb < testdb.sql
```
10. login with password
```
mysql -u <user> -p
```

11. Create another super user
```
GRANT ALL PRIVILEGES ON *.* TO '<username>'@'localhost';
FLUSH PRIVILEGES;
```
12. Grant privileges to specific database
```
GRANT ALL PRIVILEGES ON <dbname>  TO '<username>'@'localhost';
```

13. show privileges
```
show grants;
```

14. show schema
```
describe schema.tablename
```

15. Switch databases
```
use <db>;
show databases;
show tables;
```

16. To import table from csv (examples)
```
LOAD DATA LOCAL INFILE 'abalone.csv' INTO TABLE uci.abalone
 FIELDS TERMINATED BY "," LINES TERMINATED BY "\n";

LOAD DATA LOCAL INFILE 'small.csv' INTO TABLE uci.small
 FIELDS TERMINATED BY "," LINES TERMINATED BY "\n" IGNORE 1 LINES;
```

### MongoDB
Import public key
```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4
```
Create a list ifle for MongoDB
```
echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
```
Update
```
sudo apt update
```
Install
```
sudo apt-get install -y mongodb-org
```
Start mongod manually
```
sudo service mongod start
```
Check status
```
sudo systemctl status mongod
```
To verify, check the log file
```
/var/log/mongodb/mongod.log 
```

To start at boot
```
sudo systemctl enable mongod
```
Stop or Restart
```
sudo service mongod stop
sudo service mongod restart
```

### Robo 3T

```
mkdir /user/local/bin/robomongo
sudo mv robo3t-1.2.1-linux-x86_64-3e50a65.tar.gz /usr/local/bin/robomongo
cd /usr/local/bin/robomonog
sudo tar -xvzf robo3t-1.2.1-linux-x86_64-3e50a65.tar.gz
sudo ln -s /usr/local/bin/robomongo/robo3t-1.3.1-linux-x86_64-7419c406/bin/robo3t ./robot3t
```

### sqlite3
To start
```
sqlite3 <filename>
```

show all tables
```
.tables
```

import csv
```
.mode csv
.import <filename> <tablename>
```

### Redis
PPA repository
```
sudo add-apt-repository ppa:chris-lea/redis-server
sudo apt-get update
```

Install 
```
sudo apt install redis-server
```
Edit config file
```
sudo nano /etc/redis/redis.conf
```
change this line:
```
supervised systemd
```

Restart deamon
```
sudo systemctl restart redis-server.service
```

Verify
```
systemctl status redis-server
```
Command line client
```
redis-cli
> ping
> get test
```

To enable to start at boot
```
sudo systemctl enable redis-server
```

To set password in the config file, under SECURITY section
```
requirepass ><password>
```
To authenticate Redis server
```
redis-cli
> auth <your-redis-password>
```


### PostgreSQL

Create the file /etc/apt/sources.list.d/pgdg.list and add a line for the repository
```
deb http://apt.postgresql.org/pub/repos/apt/ bionic-pgdg main
```
import the repository signing key, and update the package lists
```
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo apt-get update
apt-get install postgresql-11
```

Start server
```
pg_ctlcluster 11 main start
```

Login as postgres admin user
```
sudo su - postgres
```

then create user role (account) with createdb permission:
```
create role fra LOGIN PASSWORD <password> createdb;
\q
```

With the user privilige:
```
createdb <username>
```

createdb Test
```
createdb <dbname> -O <rolename>
psql -l  | grep <rolename>
psql -h localhost
```

Now user can login with:
```
psql <dbname> <rolename>
```

edit /etc/postgresql/<version>/main/pg_hba.conf
```
encrypted password
local   all  all    md5
or (not password needed)
local   all  all    trust
```

reload postgresql
```
/etc/init.d/postgresql reload
```

### DBeaver
Install Ubuntu PPA
```
sudo add-apt-repository ppa:serge-rider/dbeaver-ce
sudo apt-get update
sudo apt-get install dbeaver-ce
```
Download deb file
alternatively install via deb package
```
sudo apt update
sudo dpkg -i dbeaver-<version>.deb
```
check version
```
apt policy  dbeaver-ce 
```
