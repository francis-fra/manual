### Cinamon Desktop Manager
```
sudo add-apt-repository ppa:embrosyn/cinnamon
sudo apt update && sudo apt install cinnamon
```

After restart, choose cinnamon when login,
but cinnamon-settings won't start, to fix it:
```
sudo emacs /usr/share/cinnamon/cinnamon-settings/modules/cs_desktop.py
```
comment out this line
```
import gi
#gi.require_version('Nemo', '3.0')
```
### Apport
To disable at boot,
edit /etc/default/apport, set
```
enabled=0
```

###### xscreen saver
command:
```
sudo apt-get remove gnome-screensaver
sudo apt-get install xscreensaver xscreensaver-gl-extra xscreensaver-data-extra xscreensaver-screensaver-bsod
```

set up
```
xscreensaver-demo
```

autostart with systemd service (not working - use startup applications)
```
mkdir -p ~/.config/systemd/user/
```
create a new file
```
emacs ~/.config/systemd/user/xscreensaver.service
```
add the following text
```
[Unit]
Description=XScreenSaver
[Service]
ExecStart=/usr/bin/xscreensaver -nosplash
[Install]
WantedBy=default.target
```
enable the service by
```
systemctl --user enable xscreensaver
```

### Chrome
Set PPA repository
```
wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
```
Install
```
sudo apt-get update
sudo apt-get install google-chrome-stable
```

### NVIDIA driver
```
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt-get update
```
find out the latest driver or check from nvidia web
```
sudo apt-get install nvidia-<version>
```
### Exercism
* Downlaod tgz file, then extract by
```
tar -xf exercism-linux-64bit.tgz
```
* copy to /usr/local/bin
* Follow the instructions to set up the token
* Config file is located at
```
$HOME/.config/exercism
```
* Edit the json file to change the workspace if needed

###### swap
check memory usage
```
cat /proc/meminfo
cat /proc/swaps
```

check partition
```
sudo fdisk -l
```

check mount point
```
cat /etc/fstab
```

Set swap manually
```
sudo swapon <swap_partition>
```

To turn on swap according to /etc/fstab
```
sudo swapon -a
```

To check debian release version
```
cat /etc/os-release
```

###### install & upgrade packages:
```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
```

To search packages
```
apt-cache search <package>
```

To list installed packages
```
apt list --installed
```

essentials:
```
apt-get install build-essential python3-dev
apt-get install devscripts curl
apt-get install synaptic
apt install ubuntu-restricted-extras
```

needed for adding PPA
```
sudo apt-get install software-properties-common
sudo apt-get install dirmngr
```

To remove PPA
```
sudo add-apt-repository --remove ppa:whatever/pp
```
To add PPA
```
sudo add-apt-repository ppa:wahtever/pp
```


To find the fastest debian mirror
```
sudo apt-get install netselect-apt
sudo netselect-apt
```

tidy up:
```
echo "Cleaning Up" &&
sudo apt-get -f install &&
sudo apt-get autoremove &&
sudo apt-get -y autoclean &&
sudo apt-get -y clean
```

###### Create symbolic link

syntax: ln -s source_location target_location
```
ln -s /media/fra/OS/FraDir /home/fra/FraDir
ln -s /media/fra/OS/FraDir/learn /home/fra/learn
```

To remove soft links
```
unlink <target location>
```

###### Install terminator
```
sudo apt-get update
sudo apt-get install terminator
```

1. customize via: Preferences -> Layout

2. To auto start at login:
    * Run Startup Applications Apps
    * Add new command:
```
/usr/bin/terminator -m --layout=myLayout
config file:
~/.config/terminator/config
```

###### Install dropbox
Method 1:
```
sudo apt install nautilus-dropbox
```

Method 2:
pre-requisite: apt install libpango1.0-0
if there is an error, fix it with:
```
apt --fix-broken install
```
Download deb file (debian) and install via
```
sudo dpkg -i <deb_file>
sudo apt install -f
```

Method 3:
Install via command line
```
cd ~/Downloads && wget -O - "https://www.dropbox.com/download?plat=lnx.x86_64" | tar xzf -
```
then, run
```
~/.dropbox-dist/dropboxd
```

Note: python3-gpg needed to be installed to verify binary signatures


### Install emacs with PPA
```
sudo add-apt-repository ppa:ubuntu-elisp/ppa
sudo apt-get update
sudo apt-get install emacs24 emacs24-el emacs24-common-non-dfsg ess
sudo apt-get install emacs25
```

1. emacs config
    * download color-theme-6.6.0.zip
    * download hightlight-current-line

2. install elpa
```
(M-x eval-buffer)
M-x package-install RET auto-complete RET
```

3. Auto mount
Start Disks app -> Edit mount options

```
nosuid,nodev,nofail,x-gvfs-show
/media/fra/OS
```

4. To edit config file: /etc/fstab
```
<file_system> <mount_point> <type> <options> <dump> <pass>
/dev/sda1     /FraDir       auto   defaults  0	    0
```

5. Auto start applications

    * folder:
```
/etc/xdg/autostart/
```

    * user folder (deepin)
```
~/.config/autostart/
```

### Emacs .emacs file
Basic setup:
```
;; BASIC CUSTOMIZATION
;; --------------------------------------

(setq inhibit-startup-message t) ;; hide the startup message
(global-linum-mode t) ;; enable line numbers globally
(column-number-mode t) ;; show column numbers in the stats bar
(require 'ido)
(ido-mode t)

; don't show the menu bar
(menu-bar-mode nil)
; don't show the tool bar
(require 'tool-bar)
(tool-bar-mode nil)

; always use spaces, not tabs, when indenting
(setq indent-tabs-mode nil)
```

###### Package: Highlight current line
Download el file and save it to .emacs.d/hightlight-current-line
Add the following to .emacs
```
; highlight the current line
(require 'highlight-current-line)
(global-hl-line-mode t)
(setq highlight-current-line-globally t)
(setq highlight-current-line-high-faces nil)
(setq highlight-current-line-whole-line nil)
(setq hl-line-face (quote highlight))
```

###### Package: elpy
Prerequisite
```
pip3 install jedi flake8 autopep8 yapf rope importmagic --user
```

Install scrpt:
```
(require 'package)
(add-to-list 'package-archives
             '("melpa-stable" . "https://stable.melpa.org/packages/"))
```

Run at minibuf:
```
M-x package-refresh-contents
M-x package-install RET elpy RET
M-x package-install RET ein RET
M-x package-install RET haskell-mode RET
```

Add the following to .emacs
```
(package-initialize)
(elpy-enable)
```

set python3 as default:
(setq python-shell-interpreter "python3"
      python-shell-interpreter-args "-i")

to check elpy config
```
(elpy-config)
```

To install packages:
```
(setq package-archives
  '(("gnu" . "http://elpa.gnu.org/packages/")
    ("marmalade" . "https://marmalade-repo.org/packages/")
    ("melpa" . "http://melpa.milkbox.net/packages/")))

;; ein
(require 'ein)
(require 'ein-loaddefs)
(require 'ein-notebook)
```

###### Package ESS
```
;; ESS
# download and extract zip file
(add-to-list 'load-path "/path/to/ESS/lisp/")
(load "ess-site")

(require 'package)
(add-to-list 'package-archives
             '("melpa-stable" . "https://stable.melpa.org/packages/") t)

;; package archives
(custom-set-variables
 ;; custom-set-variables was added by Custom.
 ;; If you edit it by hand, you could mess it up, so be careful.
 ;; Your init file should contain only one such instance.
 ;; If there is more than one, they won't work right.
 '(package-archives
   (quote
    (("gnu" . "http://elpa.gnu.org/packages/")
     ("melpa-stable" . "http://stable.melpa.org/packages/")))))

```
Command to start jupyter:
```
M-x ein:jupyter-server-start
```
to stop:
```
M-x ein:jupyter-server-stop
```

###### Create soft links
```
ln -s /home/fra/FraDir/java /usr/local/bin
ln -s /mnt/<src dir>/FraDir /home/fra/FraDir
ln -s /mnt/<src dir>/FraDir/learn /home/fra/learn
```


### source.list
Location:
```
/etc/apt/sources.list
```

Uncomment the deb-src lines and add the following to the file:

```
deb http://au.archive.ubuntu.com/ubuntu/ trusty-backports main restricted universe multiverse
deb-src http://au.archive.ubuntu.com/ubuntu/ trusty-backports main restricted universe multiverse

deb http://security.ubuntu.com/ubuntu trusty-security main restricted
deb-src http://security.ubuntu.com/ubuntu trusty-security main restricted
deb http://security.ubuntu.com/ubuntu trusty-security universe
deb-src http://security.ubuntu.com/ubuntu trusty-security universe
deb http://security.ubuntu.com/ubuntu trusty-security multiverse
deb-src http://security.ubuntu.com/ubuntu trusty-security multiverse
```

To find the fastest mirror
```
sudo apt-get instal netwelect-apt
sudo netselect-apt
```

In deepin
```
deb [by-hash=force] http://mirrors.ustc.edu.cn/deepin unstable main contrib non-free
```

### Git
```
sudo apt-get install git-all
```

1. configure git
```
git config --global user.name "fra"
git config --global user.email "fcnchan@yahoo.com"
```

2. config file location:
```
~/.gitconfig
```

3. check current config
```
git config --list
```

### Other apps

###### ibus (chinese input)
To install ibus-cangjie & other input packages and to install chinese input method:
```
ibus-setup
```
update to take effect:
```
ibus restart
```

###### others
```
sudo apt-get install calibre
sudo apt-get install variety
```


###### xscreen saver
command:
```
sudo apt-get remove gnome-screensaver
sudo apt-get install xscreensaver xscreensaver-gl-extra xscreensaver-data-extra xscreensaver-screensaver-bsod
```

To set up
```
xscreensaver-demo
```

###### wine
* install via package manager, alternatively,
* wine stable version
```
sudo dpkg --add-architecture i386
sudo add-apt-repository ppa:ubuntu-wine/ppa
sudo apt-get update
sudo apt-get install wine
```

* to configure wine
```
winecfg
```
* config file in ~/.wine

###### vmware player
* download the installer from
```
sudo ./VMware-Player*.bundle
```

###### FFMPEG
```
sudo apt-get install ffmpeg
```

######  flash player
```
sudo apt-get install flashplugin-installer
```

###### VLC
```
sudo apt-get install vlc
```

###### putty
```
sudo apt-get install putty
```

###### splint
```
sudo apt-get install splint
```

libraries:
```
libeditline-dev
```


### arduino
```
sudo apt-get instal arduino
sudo usermod -a -G dialout <username>
```
### Vagrant
Download debian package
```
sudo dpkg -i <deb file>
```

### Docker
Remove existing packages
```
sudo apt-get remove docker docker-engine docker.io containerd runc
```

Set up repository
```
sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
```

Add Docker's official GPG
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

Verify the fingerprint 9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88
```
sudo apt-key fingerprint 0EBFCD88
```
Update repository
```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```
Install Docker CE
```
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io

```
Verify
```
sudo docker run hello-world

```
Add name to docker group
```
sudo usermod -aG docker <username>
```
To confirm
```
id -nG
```
### Docker Compose
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
Make executable
```
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```


### Code::block
install via ppa:
```
sudo apt-add-repository ppa:damien-moore/codeblocks-stable
sudo apt-get update
sudo apt-get install codeblocks
```

###### Virtual Environment
* installation
```
sudo pip install virtualenv
sudo pip3 install virtualenv
sudo pip install virtualenvwrapper
sudo pip3 install virtualenvwrapper
```

* to make a folder
```
mkdir vrt_env
```

* to create virtual environment inside
```
virtualenv vrt_env/vt1
```

option: without existing packages
```
virtualenv vrt_env/vt2 --no-site-packages
```

* to activate a virtual environment
```
source vrt_env/vt1/bin/activate
```

* to switch off
```
deactivate
```

### h2o
* prerequisite
```
pip install requests
pip install tabulate
pip install scikit-learn
pip install colorama
pip install future
```

* Uninstall and reinstall
```
pip uninstall h2o
sudo pip install h2o
```
* pip install
```
pip install http://h2o-release.s3.amazonaws.com/h2o/rel-weierstrass/3/Python/h2o-3.14.0.3-py2.py3-none-any.whl
```

### sparking water
1. Download and unzip file

2. create soft link
```
sudo ln -s /usr/local/sparkling-xxxx /usr/local/sparkling-water
```

3. change ownership
```
sudo chown -R fra:hdgrp /usr/local/sparkling-water
```

4. run sparkling shell
```
cd sparkling-water-2.2.0
bin/sparkling-shell --conf "spark.executor.memory=1g"
```

example:
```
import org.apache.spark.h2o._
val h2oContext = H2OContext.getOrCreate(spark)
import h2oContext._
```

5. edit bashrc
```
export PATH=$PATH:/usr/local/sparkling-water/bin
```

### pysparking
* for spark version 2.2:
```
pip install h2o_pysparkling_2.2
```

* initialize
```
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName("SparklingWaterApp").getOrCreate()
from pysparkling import *
hc = H2OContext.getOrCreate(spark)
```

### xgboost
```
git clone --recursive https://github.com/dmlc/xgboost
cd xgboost; make -j4
```
* if successfully built to install system wide
```
cd python-package; sudo python setup.py install
```

* to check the current blas version:
```
python -c 'import scipy; scipy.show_config()'
```

### Repast
* install eclipse committers version
* need to install groovy plugin first
* choose groovy compilters, grovy-eclipse and uncategorized
```
http://dist.springsource.org/snapshot/GRECLIPSE/e4.6/
```
* then, install eclipse plugin:
```
https://repo.anl-external.org/repos/repast/
```
* install the desktop entry:
```
sudo desktop-file-install /usr/share/applications/eclipse-committers.desktop
```
* create a new symbolic link:
```
sudo ln -s /opt/eclipse/java-neon/eclipse-committers/eclipse /usr/local/bin/eclipse-committers
```

### julia
* Installation:
```
sudo add-apt-repository ppa:staticfloat/juliareleases
sudo add-apt-repository ppa:staticfloat/julia-deps
sudo apt-get update
sudo apt-get install julia
```

* install Julia packages
Reference: https://github.com/JuliaIDE/Juno-LT/blob/master/tutorial.jl
```
Pkg.update()
Pkg.add("Gadfly")
Pkg.add("Jewel")
Pkg.add("PyPlot")
Pkg.add("PyCall")
Pkg.add("Calendar")
Pkg.add("Match")
Pkg.add("LightXML")
Pkg.add("StatsBase")
Pkg.add("Pandas")
Pkg.add("DSP")
Pkg.add("SunDials")
Pkg.adad("Roots")
Pkg.add("JMP")
Pkg.add("NLPot")
Pkg.add("PGFPlots")
Pkg.add("Compose")
Pkg.add("ImageView")
```

* install Jupyter for Julia
```
Pkg.add("IJulia")
```

* to start Jupyter inside Julia:
```
using IJulia
notebook()
```

* start at terminal
```
jupyter notebook
```

### Atom
Download from github
```
sudo dpkg --install atom-amd64.deb
```

###### Juno
```
http://junolab.org/
sudo add-apt-repository ppa:webupd8team/atom
sudo apt-get update
sudo apt-get install atom
```

install Juno
```
apm insall uber-juno
```

reference:
```
https://github.com/JunoLab/uber-juno/blob/master/setup.md
https://github.com/atom/apm
http://discuss.junolab.org/t/not-able-to-install-juno-via-atom/562/6
```

To update the lastest package:
```
apm install https://github.com/JunoLab/atom-ink
apm install https://github.com/JunoLab/atom-julia-client
```

if atom and code tools are not installed
```
Pkg.clone("http://github.com/JunoLab/Atom.jl")
Pkg.clone("http://github.com/JunoLab/CodeTools.jl")
```

to pull from github
```
Pkg.checkout("Atom")
Pkg.checkout("CodeTools")
```

if problems exists
```
Pkg.free("Atom")
```

rebuild - install cmake
```
sudo apt-get install cmake
```
inside julia
```
Pkg.checkout("MbedTLS")
Pkg.build("MbedTLS")
Pkg.build("Atom")
```

packages
```
uber-juno
minimap
monokai (theme)
project-manager
linter
autocomplete-modules
file-icons
atomic-emacs
term2
atom-html-preview
hightlight line
script
```

### Brackets
```
sudo add-apt-repository ppa:webupd8team/brackets
sudo apt-get update
sudo apt-get install brackets
```

### Android Studio
method 1: PPA (ubuntu)
```
sudo add-apt-repository ppa:paolorotolo/android-studio
sudo apt-get update
sudo apt-get install android-studio
```

method 2: other linux platform
* Download zip file and  move the extracted folder to /opt

To start
```
run android.sh
```

create a new symbolic link:
```
sudo ln -s /opt/android-studio/bin/studio.sh /usr/local/bin/
```

Install 32 bit libraries:
```
sudo apt-get install lib32z1 lib32ncurses5 lib32bz2-1.0 lib32stdc++6
```

check if cpu virtualization is supported
```
egrep -c '(vmx|svm)' /proc/cpuinfo
```

install kvm
```
apt-get install qemu-kvm libvirt-bin libvirt-daemon
sudo apt-get install virt-manager
```

add user to manage virtual machines (optional)
```
adduser <youruser> kvm
adduser <youruser> libvirt
virsh list --all
```


### Tex
* install texMaker
* install missing style
```
sudo apt-get install texliv-science
```

* for math_nltk generation
```
sudo pip install CherryPy
sudo pip install dnspython
```

* Edit Path (if python was installed without root permission)
* To add additional run path
* python local library
```
export PATH=$PATH:/home/fra/.local/bin
```

### CUDA
1. pre-installation actions
To verify the GPU is CUDA-capable
```
lspci | grep -i nvidia
```

2. determine the distribution
```
uname -m && cat /etc/*release
example:
uname -r
4.4.0-28-generic
```

3. check the gcc version
```
gcc --version
```

4. install the kernel headers and dev packages
```
sudo apt-get install linux-headers-$(uname -r)
```

5. ubuntu package
```
sudo dpkg -i cuda-repo-<distro>_<version>_<architecture>.deb
sudo apt-get update
sudo apt-get install cuda
```

### Others
* Download GETDEB & PLAYDEB:

```
echo "Deleting Downloads" &&
rm -f getdeb-repository_0.1-1~getdeb1_all.deb &&
rm -f playdeb_0.3-1~getdeb1_all.deb
```

### Install deb package:
to install a package
```
sudo dpkg -i <DEB_PACKAGE>
```
run this to resolve dependencies:
```
sudo dpkg -i <DEB_PACKAGE>
apt-get install -f
```

### CUDA for Ubuntu 18.04
```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-ubuntu1804.pin
sudo mv cuda-ubuntu1804.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget http://developer.download.nvidia.com/compute/cuda/10.2/Prod/local_installers/cuda-repo-ubuntu1804-10-2-local-10.2.89-440.33.01_1.0-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu1804-10-2-local-10.2.89-440.33.01_1.0-1_amd64.deb
sudo apt-key add /var/cuda-repo-10-2-local-10.2.89-440.33.01/7fa2af80.pub
sudo apt-get update
sudo apt-get -y install cuda
```

### Virtual machines
* Horton Work sandbox
address:
```
http://192.168.169.129/
```

* Kali Linux
defulat login
```
username: root
pwd: toor
```

* shutdown command
```
shutdown -r now
sudo poweroff
```

* cloudera 5.5
defulat login
```
username: cloudera
password: cloudera
```

* yahoo vm
defulat login
```
usernname: hadoop-user
password: hadoop
```

### Docker
To start
```
docker run -h <host_name> -it <docker_image>
```

To check image
```
docker inspect <image_name>
```

To check running docker
```
docker ps
docker ps -a
```

To remove docker image from local
```
docker rm <image_name>
```

To log
```
docker logs <image_name>
```

To save image
```
docker commit cowsay test/cowsayimage
```
