### Vulnerable Systems

* Metasploitable 2
```
http://sourceforge.net/projects/metasploitable/files/Metasploitable2/
```
```
account: msfadmin
passed: msfadmin
```

* linux distributions
```
http://www.distrowatch.com
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

### kali post setup


* set time
```
sudo date --set="10:37:00"
```

* miscellaneous
```
sudo apt install xfce4-settings 
sudo apt install dkms
```

* vcode
```
echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" \\n | sudo tee /etc/apt/sources.list.d/vcode.list\n
```

* chrome
```
sudo apt install ./google-chrome-stable_current_amd64.deb
cat /etc/apt/sources.list.d/google-chrome.list
```

### virtual box

* install
```
echo "deb [arch=amd64] http://download.virtualbox.org/virtualbox/debian $( lsb_release -cs ) contrib" \\n  | sudo tee /etc/apt/sources.list.d/virtualbox.list
cat /etc/apt/sources.list.d/virtualbox.list
```
note: replace $(lsb_release -cs) i.e. kali-rooling with the current release, e.g. buster

* to load vmware image to virtual box:

1. Open VirtualBox and create a new virtual machine, or open an existing one.
2. Click the "Settings" button.
3. Click "Storage."
4. Click "SATA Controller."
5. Click "Add Hard Disk."
6. Navigate to and double-click on the VDMK file.
7. Click "OK" to save the setting.
8. Click the green "Start" icon to open the VMDK file and boot the virtual machine.


### postgresql

enable serive to autorun at startup
```
systemctl enable --now postgresql.service
```
check status
```
service postgresql status
systemctl status postgresql.service
systemctl is-enabled postgresql
```


### Metasploit
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


