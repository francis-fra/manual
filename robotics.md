### EV3

##### Getting strated
1. Download the image file: ev3dev-stretch beta
2. Flash the micro SDHC card using Etcher
3. Boot ev3dev
4. Set up wifi connection using dongle
5. Remote access (password: maker)
```
ssh robot@ev3dev.local
```
6. Verify the kernel version
```
ev3dev-sysinfo -m
uname -a
cat /etc/os-release
```
* Default debian (stretch) site:
```
deb http://httpredir.debian.org/debian stretch main contrib non-free
#deb-src http://httpredir.debian.org/debian stretch main contrib non-free
deb http://security.debian.org/ stretch/updates main contrib non-free
#deb-src http://security.debian.org/ stretch/updates main contrib non-free
deb http://archive.ev3dev.org/debian stretch main
#deb-src http://archive.ev3dev.org/debian stretch main
```
7. Create work directory
```
mkdir ev3dev-c
mkdir ev3dev-py
```


##### ev3dev-c
* Set up tools for the EV3 brick (Debian Jessie only)
```
sudo apt-get update
sudo apt-get install build-essential
sudo apt-get install git
```
* clone the git repository
```
cd /home/robot/
git clone https://github.com/in4lio/ev3dev-c.git
cd ev3dev-c/
git submodule update --init --recursive
```
* Compile and install static and shared libraries:
```
cd source/ev3/
make
sudo make install
make shared
sudo make shared-install
```
* Test example
```
cd ../../eg/hello/
gcc hello.c -lev3dev-c -o hello
./hello
```
* light example
```
cd ../../eg/light/
gcc light.c -lev3dev-c -o light
./light
```


##### python
* Install pip
```
sudo apt-get install python-pip
sudo apt-get install python3-pip
```
* Install python package
```
pip install ev3dev-c
```

##### ev3-python
* Download ev3dev visual studio code extension and the code template
```
https://github.com/ev3dev/vscode-ev3dev-browser
https://github.com/ev3dev/vscode-hello-python
```
* Install python3 library
```
sudo apt-get update
sudo apt-get install --only-upgrade python3-ev3dev2
```
* For Debian Jessie, need to update pip3. The new version is located at:
```
/usr/local/bin
```
* Update command
```
sudo pip3 install -U pip
```
* install package using pip
```
/user/loca/bin/pip3 install python-ev3dev2 --user
```

##### ev3dev-java-lang
* Install Oracle JRE on EV3 Brick (debian Jessie)
* Download the tar file from Orcale, then upload to the brick
```
scp "./ejdk-8-fcs-b132-linux-arm-sflt-03_mar_2014.tar.gz" "robot@192.168.1.6:/home/robot"
```
* Extract and install java
```
sudo tar -zxvf "/home/robot/ejdk-8-fcs-b132-linux-arm-sflt-03_mar_2014.tar.gz" -C /opt
sudo update-alternatives --install /usr/bin/java java /opt/ejdk1.8.0/linux_arm_sflt/jre/bin/java 8
```
* Install OpenJDK on EV3 Brick (debian stretch)
```
wget -N https://github.com/ev3dev-lang-java/openjdk-ev3/releases/download/v0.5.0/jri10-ev3.tar.gz
sudo tar -zxvf jri10-ev3.tar.gz -C /opt
sudo mv /opt/jri-ev3/ /opt/jri-10-build-050
sudo update-alternatives --install /usr/bin/java java /opt/jri-10-build-050/bin/java 10
```
* Installer (FIXME)
```
cd /home/robot
mkdir installer
cd installer
wget -N https://raw.githubusercontent.com/ev3dev-lang-java/installer/master/installer.sh
chmod +x installer.sh
sudo ./installer.sh help
sudo ./installer.sh java
```
* If the java.sh is not downloaded automatically, download and run manually:
```
wget -N https://raw.githubusercontent.com/ev3dev-lang-java/installer/develop/modules/java.sh
chmod +x java.sh
./java.sh
```
* Download gradel project template to local machine
```
git clone https://github.com/ev3dev-lang-java/template_project_gradle.git
```
* If Debian Stretch is used, switch to Dev branch
```
git checkout origin/develop
```
* Configure file under gradle/config.gradle
```
remotes {
    ev3dev {
        host = '192.168.1.6'
        user = 'robot'
        password = 'maker'
    }
}
```
* To test
```
./gradlew testConnection
```
* To deploy and then run
```
./gradlew deployAndRun
```
* To run
```
./gradlew remoteRun
```
