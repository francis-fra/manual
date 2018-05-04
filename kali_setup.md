### Downloads 
* Download kali VM

* Metasploitable 2
```
http://sourceforge.net/projects/metasploitable/files/Metasploitable2/
```

* linux distributions
```
http://www.distrowatch.com
```

### Vulnerable Systems
* Metasploitable 2
```
account: msfadmin
passed: msfadmin
```
* reboot
```
sudo shutdown -r now
```

* OWASP Borken Web
```
https://sourceforge.net/projects/owaspbwa/files/
```

* turnkey (wordpress)
```
https://www.turnkeylinux.org/
```

* LAMPSecuirty
```
http://sourceforge.net/projects/lampsecurity/
```

* Damn Vulnerable 
```
https://sourceforge.net/projects/virtualhacking/files/os/dvl/
```

* Hackxor
```
http://hackxor.sourceforge.net/cgi-bin/index.pl
```

* DVWA
```
http://www.dvwa.co.uk/
```

### Kali setup
* change password
```
passwd
```

* add a new user
```
sudo adduser <user_name>
```

* update image
```
apt-get update
apt-get dist-upgrade
```

* setup Metasploit database

* setting static IP
```
edit /etc/network/interfaces
```
* change eth0 as
```
auto eth0
iface eth0 inet static
address <ip>
netmask 255.255.255.0
gateway 192.168.1.1
```

* setup metasploit db
```
service postgresql start
```
* make autostart on boot
```
update-rc.d postgresql enable
```

* start apache server
```
service apache2 start
```

### start SSH
```
sshd-generate
service ssh start
```

* verify the server is up
```
netstat -tpan | grep 22
```

* start ftp server
```
service pure-ftpd start
```
* to verify
```
netstat -ant | grep 21
```

* to stop the service
```
service <servicename> stop
```

* to enamble  auto start
```
update-rc.d -f <servicename> defaults
```

### pfsense
* Download iso
```
https://www.pfsense.org/download/?section=downloads
```

* Create a pfsense VM 


### Windows host platform
* check playbook

### Windows Target system
* Download XAMPP
* Download DVWA
* Download Mutillidae

### Reference Book
* Kali Playbook
* Kali Cookbook
* Mastering Kali
* Intermediate Secuirty Testing


```
https://www.cybrary.it/0p3n/create-complete-virtual-environment-penetration-testing-part-1/
http://resources.infosecinstitute.com/building-your-own-pentesting-environment/
```

laptop:
* win7 / linux (CentOS) victim (dual boot)
* Kali
