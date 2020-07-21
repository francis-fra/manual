# Basic
======
```
w; free; df;
```

Swithc to tty1
```
Ctrl+Alt+F1
```

To shutdown
```
shutdown -h now
```

Use -e to enable interpretation of back slash
```
echo -e "Hello\nWorld"
```

Use cat and grep for archived files
```
zcat and zgrep
```

Admin
======
Show running service
```
service --status-all
```

To show hostname
```
hostnamectl
```

Create a hard link
```
ln <existing_file> <new_link>
```

Create a soft link
```
ln -s <existing_file_or_directory> <new_link>
```

Mount devices
```
mount <source_device> <mount_point>
```

Find the matching names
```
find . -name \*.txt
```

append this to run the command from the output of find
```
-exec command {} \;
```

Example: change user own and group
```
find /home/chavez -exec chown chavez {} \; \ -exec chgrp physics {} \;
```

Check parameters
```
type -d (directory)
type -f (file)
type -l (symbolic link)
```

Find files
```
locate <filename>
find <src_dir> -name <file_name>
```

To see the content of zip file
```
gzcat
```

To examine the content of a tar file
```
tar -tf <xxx.tar>
```

Archive
======
###### Compress and tar a folder
compress files using parameter 'c'
```
tar cvf <xxx.tar> <target_directory>
```

###### To create .gz file
```
gzip xxxx.tar
```
###### To unzip
```
gunzip xxxx.tar.gz
```

###### Uncompress
Use param 'x' for extraction
```
tar -xvf <xxx.tgz> -C <destination folder>
tar -zxvf <xxx.tgz>
```

###### compress tgz file
```
tar cvzf <xxx.tgz> <target_dir>
```

###### Extract tgz file
```
tar xvzf <xxx.tgz> -C <destination_dir>
```

###### Tar and compress
One liner (tar and compress)
```
tar -cf - <source folder | gzip > <destination folder/xxx.tar.gz>
```

One liner (extract)
```
gzip -dc <xxxx.tar.gz> | tar -xf - -C <destination folder>
```

Useful commands
======
Issue schedule job
```
sudo apt-get install at
```
example:
```
at now + 7 hours
```

Cron jobs location
```
/etc/cron.*
```

word count
```
wc -l ~/Documents/ubuntu_setup.txt
```

Check running process
```
ps [-ef]
```

Sort by the 3rd field
```
sort -t: -k3,3 -n /etc/group
```
Word count
```
tr -sc 'A-Za-z' '\n' < <filename> | sort | uniq -c
```

File management
```
file <filename>
tree <directory>
```

Drive mount location
```
/etc/fstab
```

Disk space
```
df -h
```
Disk usage
```
du -h
```

Sorting (descending) the number
```
du -h | sort -nr
```

###### Grep
```
grep -option <string> <file or directory>
grep -r (recursive)
grep -n (line num)
grep -c (count only)
grep -i (ignore case)
grep -A (show additional lines after the target)
grep -o print only the matching  part
grep -l (list file name only)
```

these are equivalent:
```
cat <file> | grep <pattern>
grep <pattern> <file>
```

Show the output and also save the content to a file
```
tee <file_name>
```

Remove sections of text
```
cut -f (extract field)
cut -d (delimiter)
```
e.g. grep the word 'chapter' from the file 'alice.txt' and then extract the field from number 3 till the end where the delimiter is an empty space
```
grep -i chapter alice.txt | cut -d ' ' -f 3-
```
e.g. read the file 'alice.txt' and extract using the regular expression (every single word)
```
< alice.txt grep -oE '\w+'
```

coproc (putting in background)
```
coproc <command>
```
Excecute command line num from the history list
```
!<num>
```
alias
```
alias li='ls -li'
```

###### User management
add new user & group
```
sudo adduser <user_name>
sudo groupadd <group_name>
```

add user to sudo group (fedora)
```
sudo usermod -aG sudo <usename>  (reboot required)
```

to check all sudoers (or use visudo in RH)
```
grep -Po '^sudo.+:\K.*$' /etc/group
cat /etc/sudoers
```

change ownership
```
chown <new-owner> <files>
```

To set default file mode for newly created files
```
umask <code>
```

Environment Variables
======

Global environment variable
```
printenv
```
e.g.
```
printenv HOME
printevn USER
```

To set local variables
```
my_var=Hello
my_var="Hello World"
```
Echo variable:
```
echo $PATH
```

To remove env variable
```
unset <var name>
```

Some startup files are placed in:
```
/etc/profile.d
```

Variable arrays
```
mytest=(one tow three)
echo $mytest
echo ${mytest[1]}
echo ${mytest[*]}
```

File Permission
======
add new user and create home directory
```
useradd -m <username>
```
remove a user
```
userdel -r <username>
```
change password
```
passwd
```
change passwd expiration date
```
chage
```

account management
```
usermod
```

groups definition
```
/etc/group
```
To add new group
```
groupadd <name>
```

To add new user to a group
```
usermod -G <group_name> <user_name>
```

To set default file permissions
```
umask <setting>
```
To change ownership
```
chown <owner> <file>
chown <owner>.<group> <file>
```
To change group
```
chgrp <group> <file>
```

To set SGID for directory
```
chmod g+s <dir>
```

To check user ids
```
id <user_name>
```

check file system
```
fsck <option> <fs>
```

###### Install software

Debian system
1. aptitude
2. apt-get
3. dkpg

Red hat system
1. yum
2. zypper


###### Networking
```
mtr google.com
```

config files
```
/etc/hosts : list of hostnames
/etc/services : network service, port
/etc/resolv.conf : DNS
/etc/host.conf : network info
/etc/host.conf : it list the order for hostname resolution
/etc/dhcp/dhclient.conf : DHCP client config
```

to find out the ip
```
hostname -I
```
to find more details
```
ip addr show
```
netmask config
```
ifconfig
```
IP routing table
```
netstat -rn
```
display all env
```
env
```
network statistics
```
netstat
```

###### Emacs setup
install ess
```
sudo apt-get install ess
```

config file
```
.emacs
```
start ess
```
M-x R
```
auto-complete package
```
M-x package_install [RET] auto-complete [RET]
```
python
```
M-x python-mode
C-c C-p
```

###### Bash
shebang
```
#!/bin/bash
echo "hello."
```
To run bash script
```
bash <file> or source <file>
```

shell script
```
DOC='/home/fra/Documents'
echo $DOC

comp='fra'
echo "I am ${comp}"
```

back quotes
```
echo "There are `wc -l /etc/passwd` lines in the password file."
```

###### Config files

grub
```
/etc/default/grub
```
Some setup files in etc:
```
/etc/group
/etc/passwd
/etc/hosts
/etc/services
```

SSH server
======
1. Install
```
sudo apt-get install openssh-server
sudo apt-get install openssh-client
```

2. setup firewall
```
sudo ufw allow 22
sudo ufw app list
sudo ufw status
```

3. The config file is stored at
```
/etc/ssh/sshd_config
```

e.g to edit port number different from 22
```
Port 2122
Protocol 2
LoginGraceTime 120
PermitRootLogin no
PasswordAuthenatication no
AllowUsers user1 user2
PrintLastlog yes
IgnoreRhosts yes
RhostsAuthentication no
RSAAuthentication yes
HostbasedAuthentication no
# ListenAddress 192.168.1.20
```

4.Edit welcome message
```
/etc/issue.net
```
To create banner message, add this line to sshd_config file
```
Banner /etc/issue.net
```

5. restart
```
sudo service ssh restart
sudo systemctl reload sshd (RH)
```

6. check if sshd is active
```
netstat -plant
```

7. Setup SSH client
LOCAL machine: SSH key generation
```
ssh-keygen -t rsa
```

LOCAL machine: default public key is stored at
```
~/.ssh/id_rsa.pub
```

LOCAL machine: default private key is stored at
```
~/.ssh/id_rsa
```

8. Make the key pairs private
```
chmod 700 .ssh
chmod 600 .ssh/id_rsa*
```

9. Copy and append the public key to the remote machine (use dropbox or scp)

To copy via scp (if password authentication allowed)
```
scp -P <port_number> ~/.ssh/id_rsa.pub username@serverip:~/tmp/.ssh
```

10. Append the local machine public key to the server authorized keys

backup first
```
cp ~/.ssh/authorized_keys ~/.ssh/authorized_keys_copy
```
then append
```
cat ~/id_rsa.pub >> ~/.ssh/authorized_keys
```

11. HOST machine: check ~/.ssh/authorized_keys in the remote host
```
chmod 600 ~/.ssh/authorized_keys
```

Examples
e.g. ssh -p 22 xxx@192.168.0.1
```
ssh -p <port_number> username@serverip
```

To login without keys
```
ssh -l username ipaddress
```

File Transfer
======
```
scp -P <port_num> <source> <destination>
```

to copy files to remote host, e.g.
```
scp -P <port_num> myfile.txt username@192.168.2.21:/home/demo
```

to copy from remote host, e.g.
```
scp -P <port_num> username@192.168.2.21:/home/demo/myfile.txt .
scp -P <port> <filename> <destination>:location
e.g. scp -P 22 mydoc.txt fra@192.168.1.6:Documents/
```

Rsync
======
```
sudo apt-get install rsync
yum install rsync
```

sync files locally
```
rsync -zvh <source_file> <target_directory>
```
e.g.
```
rsync -zvh backup.tar /tmp/backups
```

sync directory locally
```
rsync -avzh <source_directory> <target_directory>
e.g.
rsync -avzh /home/fra/Documents /tmp/backups/Documents
```

sync from local to remote
```
rsync -avz <local_source> <remote_target>
e.g.
rsync -avz /home/fra/Documents fra@192.168.1.10:/home/fra/
```

rsync from remote to local
```
rsync -avz <remote_target> <local_source>
rsync -avzh fra@192.168.1.10:/home/fra /home/fra/Documents
```

to transfer via ssh, add -e to options

to show progress, add -progress to options
```
rsync -avzh -e 'ssh -p 22' --progress fra@192.168.1.10:/home/fra /home/fra/Documents
```

HTTP Server
======
```
sudo apt-get install apache2
```
try
```
"http://<local_IP_address>
```

check app list
```
sudo ufw app list
```
To check details
```
sudo ufw app info "Apache Full"
sudo ufw allow in "Apache Full"
```

To find the server IP address
```
ip addr show eth0 | grep inet | awk '{ print $2; }' | sed 's/\/.*$//'
```

start, restart and stop
```
sudo /etc/init.d/apache2 start   #start apache
sudo /etc/init.d/apache2 stop   #stop apache
sudo /etc/init.d/apache2 restart   #restart apache
```
alternatively
```
sudo service httpd restart
sudo service apache2 restart
```

to prevent from starting at boot
```
sudo update-rc.d -f apache2 remove
```
to autostart
```
sudo update-rc.d apache2 defaults
```
existing host location
```
/etc/hosts
```

To change ownership
```
sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html/
```

Default location is at
```
/var/www/html
```

To change another location, edit
```
/etc/apache2/sites-enabled/000-default
```
Replace the DocumentRoot and Directory to the new location

Manual restart
```
sudo /etc/init.d/apache2 restart
```
alternatively
```
sudo systemctl restart apache2
```


optional:
To create multiple sites, config file:
```
/etc/apache2/apache2.conf
```

Two subdirectories in
```
/etc/apache2:
```
Hosts config files defining virtualHosts
```
/etc/apache2/sites-available
```
Contain symlinks to sites-available
```
/etc/apache2/sites-enabled
```

To create a new virtual host, create a new file mysite.com.conf under sites-available
example:
```
<VirtualHost *:80>
ServerAdmin webmaster@mysite.com
DocumentRoot /var/www/mysite.com
ServerName www.mysite.com
ErrorLog /var/log/apache2/error.log
</VirtualHost>
```

To create multiple sites
```
cp /etc/apache2/sites-available/default /etc/apache2/sites-available/newsite
```
then edit /etc/apache2/sites-available/newsite
```
sudo a2dissite default
sudo a2ensite newsite
```

To enable SSL
```
sudo a2enmod ssl
```
Setup wordpress db
```
CREATE DATABASE wpdb;
CREATE USER wpuser@localhost IDENTIFIED BY 'new_password_here';
GRANT ALL ON wpdb.* to wpuser@localhost;
FLUSH PRIVILEGES;
```


PHP
=====
```
sudo apt-get install php libapache2-mod-php php-mcrypt php-mysql
```

Default config file:
```
/etc/php5/apache2/php.ini
```

optional
```
sudo apt-get install libapache2-mod-php5 php5-mysql
php5-curl php5-gd php5-intl php-pear php5-imagick php5-imap
php5-mcrypt php5-memcache php5-ming php5-ps php5-pspell
php5-recode php5-sqlite php5-tidy php5-xmlrpc php5-xsl
```

Default index file
```
/etc/apache2/mods-enabled/dir.conf
```

To check php modules available
```
apt-cache search php- | less
apt-cache show <package_name>
```

Edit info.php
```
/var/www/html/info.php
<?php phpinfo(); ?>
```

Check
```
http://localhost/info.php
```

To install php myadmin
```
sudo apt-get install phpmyadmin
```

check
```
http://localhost/phpmyadmin/
```


Word Press
=====
create a new mysql database
To inside mysql:
```
CREATE DATABASE wpdb;
CREATE USER wpuser@localhost IDENTIFIED BY 'password';
GRANT ALL ON wpdb.* TO wpuser@localhost;
```

Install via package
```
# sudo apt-get install wordpress
```

To download
```
cd ~/Downloads/ && wget http://wordpress.org/latest.tar.gz
```

To extract
```
tar -xvzf latest.tar.gz
```

some setup
```
touch wordpress/.htaccess
chmod 660 wordpress/.htaccess
cp wordpress/wp-config-sample.php wordpress/wp-config.php
mkdir wordpress/wp-content/upgrade
```

To edit this file:
```
// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define('DB_NAME', 'wpdb');
```

MySQL database username
```
define('DB_USER', 'wpuser');
```


MySQL database password
```
define('DB_PASSWORD', 'password');
```

Copy the wordpress files to /var/www/html
```
sudo cp -a wordpress/* /var/www/html
```


To set permission
```
sudo chown -R fra:www-data /var/www/html/
sudo chmod g+w /var/www/html/wp-content
sudo chmod -R g+w /var/www/html/wp-content/themes
sudo chmod -R g+w /var/www/html/wp-content/plugins

```
