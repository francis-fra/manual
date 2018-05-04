### Basic
```
sudo dnf update
sudo dnf upgrade
```

To search a package
```
dnf search <search_string>
```

To install package
```
sudo dnf install <package>
sudo dnf install <local_rpm>
```

To show package
```
dnf info <package>
```

To list installed
```
dnf list installed <search-string>
```

To remove a package
```
sudo dnf erase <package>
```

To activate RPMFusion Repository
```
rpm -ivh http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-24.noarch.rpm
```

To fedora version
```
cat /etc/fedora-release
```

To list all package groups (and desktop environment)
```
dnf group list
```

To install desktop manager
```
dnf install @kde-desktop
```

### Install Dropbox
install dependecies
```
sudo yum install nautilus-extensions.x86_64 
```

To download rpm package from dropbox
```
sudo rpm -ivh nautilus-dropbox-1.6.2-1.fedora.x86_64.rpm
```

To uninstall:
```
sudo rpm -e nautilus-dropbox-1.6.2-1.fc10.x86_64
```

To remove DropBox from yum repository
```
yum-config-manager --disable Dropbox
yum-config-manager --enablerepo Dropbox
```

### Install Packages
To download and install
```
sudo yum localinstall <rpm_package>
```

To terminator
```
yum install terminator
```

To download rpm
```
sudo dnf install <rpm_package>
```

To install adobe flashInstall Packages
```
sudo rpm -ivh http://linuxdownload.adobe.com/adobe-release/adobe-release-i386-1.0-1.noarch.rpm
```

To import keys
```
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-adobe-linux
```

To install
```
sudo dnf install flash-plugin
```

### Install Oracle Java
To run rpm command
```
rpm -Uvh <package_name>
```

To edit .bash_profile or .bashrc
```
export JAVA_HOME=<path_name>
```

### Nvidia driver problem
To check video driver
```
lshw -c video
lspci | grep VGA
dpkg -l | grep nvidia
```

To check installed packages
```
dpkg --get-selections | grep -v deinstall | less
```
To check installed nvidia packages 
```
dpkg --get-selections | grep -v deinstall | grep nvidia
```
Some nvidia drivers
```
nvidia-367
nvidia-opencl-icd-367
nvidia-prime
nvidia-settings
nvidia-375
```

To check xorg setting
```
cat /etc/X11/xorg.cong.XXXXX
```

To login screen daemon
```
sudo lightdm stop
sudo lightdm start
```

```
modinfo nvidia-367
modinfo nvidia-current
```

To check logs
```
.xsession-errors
/var/log/Xorg.0.log
```

To list additional drivers
```
sudo ubuntu-drivers list
sudo ubuntu-drivers devices
```

To reinstall?
```
sudo systemctl stop lightdm

sudo apt-get purge nvidia-*
sudo apt-get update
sudo apt-get install nvidia-current
or
sudo apt-get install nvidia-375
or
sudo ubuntu-drivers autoinstall
```

updating the alternatives
```
sudo update-alternatives --config x86_64-linux-gnu_gl_conf
```

###### If blank screen after grub
* edit grub parameters
* press 'e' to edit ubuntu parameters
* add this line to the end
```
nouveau.modeset=0
```

error message?
fail to use bus name org.freedisktop.displaymanager

To add nvidia ppa:
```
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt update && sudo apt install nvidia-367
```
Check:
```
/etc/apt/sources.list
```

To use intel card instead of nvidia
```
prime-select intel
```

### Slackware Setup
1. Do disk fragmatation

2. For win 8, further steps to reduce the disk size before shrinking the volume

    * Disable pagefile: Control Panel -> System and Security -> System -> Advanced system settings -> Advanced tab -> [Performance] Settings... -> Advanced tab -> [Virtual memory] 
    * Change... -> uncheck Automatically manage paging file size for all drives -> select No paging file -> Set -> Yes -> OK...

    * Disable hibernation file (hiberfil.sys): lower left corner rt click -> Command Prompt (Admin) -> powercfg /h off ["powercfg /h on" to turn it back on]

    * Disable system restore: Control Panel -> System and Security -> System -> System protection -> select Local Disk (C:)(System) -> Configure... -> Disable system protection

    * Disable writing debugging information: Control Panel -> System and
Security -> System -> Advanced system settings -> Advanced tab -> 
[Startup and Recovery] Settings -> change Write debugging information from Automatic memory dump to none

    * Disk cleanup: Control Panel -> System and Security -> Free up disk space [at bottom] -> check everything -> OK

    * Defragment: Control Panel -> System and Security -> Defragment and optimize your drives [under Administrative Tools]

    * shrink volume
```
Win + R
diskmgmt.msc
```

3. To check existing fs
```
fdisk -l /dev/sda
```

4. create partition (see command line manual)
```
fdisk
n: create new partiion
i: show partiion
p: print partitions
m: help
```

5. required drives and codes:
```
ef02 boot partition (+1M):
82 swap (+4G)
83 Linux filesystem
```

6. to prepare for grub
```
"1" is the number of the boot partition created /dev/sda refers to the hard disk
parted /dev/sda set 1 bios_grub on
```

7. check disk partition
```
parted /dev/sda print
chroot /mnt
```

8. install grub
```
grub-install --recheck /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
```

9. to update grub:
```
update-grub
grub-mkconfig -o /boot/grub/grub.cfgmkconfig
```

###### Additional Linux
Mount point
```
/etc/mtab
```

To mount other os
```
mount /dev/sda4 /mnt/centos
```

To auto mount, edit
```
/etc/fstab
```

To show file system type
```
df -T
```

To mount LVM group
To check logical volume
```
lvmdiskscan
lvdisplay
vgdisplay
lvscan
lvs
```

To set resolution:
```
modprobe dm-mod
```
To activate the logical group:
```
vgchange -ay
```

To check the lv group name:
```
mount <LVgroup name> <mount point>
mount /dev/centos/root /mnt/centos
```

### Centos YUM
To add EPEL Repository
```
yum -y install epel-release
```
To check installed packages
```
yum list installed
yum grouplist installed
yum check-update
yum info <package>
```

To remove a package
```
yum remove <package_name>
```

To search package
```
yum list <package>
```

To list repo
```
yum repolist
```

To list group package
```
yum grouplist
```

To install group package
```
yum groupinstall "Base"
yum groupinstall "Web Server"
yum groupinstall "Development tools"
```

To check group info
```
yum groupinfo "Base"
```

To update / install from repository
```
sudo yum update
sudo yum install <package>
```

other commands:
```
yum history list
yum history summary
yum groupinstall "Eclipse"
```

###### sudoers
Config file:
```
/etc/sudoers
```
To add a sudoers - edit with
```
visudo
```

###### GUI
To install KDE Desktop environment
```
yum -y groups install "KDE Plasma Workspaces"
yum install @kde-desktop
```

To insert into init file
```
echo "exec startkde" >> ~/.xinitrc
```

To enable graphical login, /etc/inittab is not used

to check default
```
systemctl get-default
```

To change default
```
systemctl set-default <setting>.target
```
where setting is: graphical (run-level 5) or  multi-user (runlevel 3)

###### Edit hostname
```
/etc/hostname
```

To check time setting
```
timedatectl
```
To set UTC
```
timedatectl -set-local-rtc 0
```
To set time
```
timedatectl set-time HH:MM:SS
```
To add new user
```
useradd ling
```
To set password for the first time
```
passwd ling
```
To check autostart service
```
chkconfig httpd on
```

###### HTTP Server
```
yum install httpd
```

to start
```
service httpd start
```

To check status
```
service httpd status  (RH)
service apache2 status (ubuntu)
```

config file location:
```
/etc/httpd/conf/httpd.conf
```
Change the port number in this file


###### Firewall settings
To display settings
```
firewall-cmd --state
firewall-cmd --get-active-zones
firewall-cmd --list-all
firewall-cmd --list-ports
firewall-cmd --list-services
```

To allow apache through firewall, enable immediately
```
firewall-cmd --add-port=22/tcp
firewall-cmd --add-service=http
```

To add the service permanently (but need to reload firewalld)
```
firewall-cmd --permanent -add-port-<port num>/tcp
```
for example
```
firewall-cmd --permanent -add-port=80/tcp
```

To reload firewall to take effect
```
firewall-cmd --reload
```

###### Services
To restart
```
systemctl restart httpd.service
```
To Check status
```
systemctl status httpd
```
To start
```
systemctl start httdp.service
systemctl enable httdp.service
```

To autostart on boot
```
chkconfig httpd on
```

### PHP Server
```
sudo yum install php php-mysql php-devel
```
others:
```
php-gd php-pecl-memcache php-pspell php-snmp php-xmlrpc php-xml
```

To restart httpd after installation
```
systemctl restart httpd.service
```

To create a test page
```
echo -e "<?php\nphpinfo();\n?>"  > /var/www/html/phpinfo.php
```

To restart apache2
```
service restart httpd
systemctl restart httpd.service
```

###### MariaDB Server
* go to mariadb download page
* get the repository entry
* copy the setup text and save it to
```
/etc/yum.repos.d/MariaDB.repo
```

* If existing version is present
```
systemctl stop mariadb
yum remove mariadb-server mariadb mariadb-libs
yum clean all
```

* To install
```
yum -y install mariadb-server mariadb-client
```
```
systemctl start mysql
systemctl start mariadb
```
```
systemctl enable mysql
systemctl enable mariadb
```
```
sudo mysql_upgrade
```

* Download SQL client: sql workbench
* Download mariadb JDBC driver


###### optional:
To set passwords
```
mysql_secure_installation
```

To add firewall
```
firewall-cmd --add-service=mysql
```

###### SSH
```
ssh -V
```

To edit config file
```
/etc/ssh/ssh_config
```

To change port number and options?
```
semanage port -a -t ssh_port_t -p tcp 2882
```

###### Others
Needed to mount windows
```
yum install ntfs-3g
yum install nmap
yum install telent
yum install vsftpd
```

config file location:
```
/etc/vsftpd/vsftpd.conf
```

cron jobs config file:
```
/etc/crontab
```

###### Intellij

* Download tar.gz file
* Extract compressed archive
```
tar xfz <ideaIC or ideaIU>-*.tar.gz
e.g.
sudo tar xf <ideaIC or ideaIU>-*.tar.gz -C /opt/
```
* run the installation script
```
cd opt/<ideaIC or ideaIU>-*/bin
idea.sh
```

###### Eclipse
* install the eclipse installer 
* install using sudo root  
* turn OFF bundle pool


###### Applications
terminator
```
yum install terminator
```
auto start:
```
terminator -m --layout=myLayout
```

community enreprise linux repository
```
rpm -Uvh
http://www.elrepo.org/elrepo-release-7.0-2.el7.elrepo.noarch.rpm

yum install R
yum install emacs
```

calibre
```
sudo -v && wget -nv -O- https://download.calibre-ebook.com/linux-installer.py | sudo python -c "import sys; main=lambda:sys.stderr.write('Download failed\n'); exec(sys.stdin.read()); main()"
```

To add items in KDE
* right click panel -> edit applications


###### python

```
yum groupinstall 'Development Tools'
sudo yum -y install python34 
sudo yum -y install python-pip
sudo python -m pip install --upgrade pip
sudo yum install python-devel.x86_64
```

To setup tools problem, use old version
```
pip install --user setuptools==33.1.1
```

It is NOT recommend to install using sudo
```
pip install --user numpy scipy matplotlib ipython jupyter pandas sympy nose
pip install --user -U scikit-learn
pip install --user csvkit
```


###### FFMPEG
For python animation
```
yum install tkinter
sudo rpm --import http://li.nux.ro/download/nux/RPM-GPG-KEY-nux.ro
sudo rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-5.el7.nux.noarch.rpm
```

For matplotlib backend config file:
```
import matplotlib
matplotlib.matplotlib_fname()
```

###### Locale
To enable / disable ibus:
```
im-chooser
```

To check status
```
localectl
```
Sample output:
```
   System Locale: LANG=en_US.UTF-8
       VC Keymap: us
      X11 Layout: us
```

To install ibus method
```
yum search ibus
yum install ibus-table-chinese-XXXXX
```

```
ibus-setup
localectl set-locale LANG=locale_name
```
example:
```
localectl set-locale LANG=en_GB.utf8
```
