### R -- Debian
```
sudo apt-get update
sudo apt-get install r-base r-base-dev
sudo apt-get install libatlas3-base
```

* R default library path
```
/usr/local/lib/R/site-library
```

```
sudo chmod o+w /usr/local/lib/R/site-library
sudo chmod o+w -R /usr/lib/R/site-library
sudo chmod o+w -R /usr/lib/R/library
```

* additional packages for RCurl:
```
sudo apt-get install libcurl4-openssl-dev
sudo apt-get install libxml2-dev
sudo apt-get install libssl-dev
sudo apt-get install libnlopt-dev
```

###### Install R -- Ubuntu
1. To use the CRAN repository:
```
add apt key:
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9
```

    * add this line to the file /etc/apt/source.list
:
```
deb https://cran.csiro.au/bin/linux/ubuntu/xenial/
```

    * also check the source.list section below.

    * Last, at the terminal, type:
```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install r-base
sudo apt-get install r-base-dev
```

2. Set up R library:
    * add write permission to this folder:
```
cd /usr/local/lib/R
sudo chmod o+w site-library
sudo chmod o+w -R /usr/lib/R/site-library
sudo chmod o+w -R /usr/lib/R/library
```

3. additional packages
    * RCurl:
```
sudo apt-get install libcurl4-openssl-dev
sudo apt-get install libxml2-dev
sudo apt-get install libssl-dev
```

    * JAGS for linux
```
sudo apt-get install jags
```

    * update packages inside R with SUDO
```
sudo R
update.packages()
```

### F``#``
1. install Mono

```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
echo "deb http://download.mono-project.com/repo/debian wheezy main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
```
2. additional: mod_mono
```
echo "deb http://download.mono-project.com/repo/debian wheezy-apache24-compat main" | sudo tee -a /etc/apt/sources.list.d/mono-xamarin.list
sudo apt-get update
```

3. install mono and fsharp
```
sudo apt-get install mono-complete mono-devel fsharp referenceassemblies-pcl
```

4. if this is not included
```
sudo apt-get install ca-certificates-mono
```


5. install monodevelop via flatpak
```
sudo add-apt-repository ppa:alexlarsson/flatpak
sudo apt-get update
sudo apt-get install flatpak
```

6. add minimal flatPak repository:
```
flatpak remote-add --user --from gnome https://sdk.gnome.org/gnome.flatpakrepo
```

7. to install MonoDevelop:
```
flatpak install --user --from https://download.mono-project.com/repo/monodevelop.flatpakref
```

8. to start
```
flatpak run com.xamarin.MonoDevelop
```

### F# paket
1. Download the latest paket.exe

2. save the paket.exe in the project sub folder .paket

3. create a file called  paket.dependencies and type:
```
source https://nuget.org/api/v2
nuget Fslab
```

4. run
```
mono paket.exe install
```

### Rust
Download and run install script
```
curl https://sh.rustup.rs -sSf | sh
```

bin files will be place at:
```
$HOME/.cargo/bin
```

* keep update
```
rustup update
rustup self update
```

* check version
```
rustc --version
```

* to uninstall
```
sudo /usr/local/lib/rustlib/uninstall.sh
rustup self uninstall
```

### Clojure
```
curl -O https://download.clojure.org/install/linux-install-1.9.0.358.sh
chmod +x linux-install-1.9.0.358.sh
sudo ./linux-install-1.9.0.358.sh
```

to run:
```
clojure
```

### Leiningen
* Download lein script

* make it executable and place in in /usr/local/bin

* need to unset CLASSPATH first
```
unset CLASSPATH
```

* install:
lein

* reun repl
lein repl

### Atom proto-repl
* key commands
```
startup: ctrl+, l
connect: ctrl+, y
```

* to load dependencies, must start atom from the project level directory

* typical project.clj dependencies:
```
:dependencies [[org.clojure/clojure "1.8.0"]
               [incanter/incanter "1.5.5"]
               [org.clojure/math.numeric-tower "0.0.4"]
               [me.raynes/fs "1.4.6"]
               [proto-repl "0.3.1"]
               [proto-repl-charts "0.3.1"]]
```



### TODO: Vowpal Wabbit
* Get libboost program-options and zlib:
```
apt-get install libboost-program-options-dev zlib1g-dev
```

* Get the python libboost bindings (python subdir) - optional:
```
apt-get install libboost-python-dev
```

* Get the vw source:
```
git clone git://github.com/JohnLangford/vowpal_wabbit.git
```

* Build:
```
cd vowpal_wabbit
make
make test       # (optional)
make install
```

### Groovy
* using SDKMAN!
```
curl -s get.sdkman.io | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
sdk install groovy
groovy -version
```

* install eclipse plugin (Neon)
```
http://dist.springsource.org/snapshot/GRECLIPSE/e4.6/
```

### Scala
* Download deb file
```
wget www.scala-lang.org/files/archive/scala-2.11.7.deb
sudo dpkg -i scala-2.11.7.deb
or
sudo apt-get update
sudo apt-get install scala
```

* sbt installation
```
echo "deb https://dl.bintray.com/sbt/debian /" | sudo tee -a /etc/apt/sources.list.d/sbt.list
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823
sudo apt-get update
sudo apt-get install sbt
```
* upgrade sbt version
```
sbt sbtVersion
```


* java install
```
sudo apt-get install python-software-properties
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
```

* git install
```
sudo apt-get install git
```

###### Scala test
add these to build.sbt
```
libraryDependencies += "org.scalactic" %% "scalactic" % "3.0.5"
libraryDependencies += "org.scalatest" %% "scalatest" % "3.0.5" % "test"
```

Add this to global - does not work in plugins.sbt!! (e.g.  ~/.sbt/0.13/global.sbt)
```
resolvers += "Artima Maven Repository" at "http://repo.artima.com/releases"
```

Add these to plugins.sbt
```
addSbtPlugin("com.artima.supersafe" % "sbtplugin" % "1.1.3")
```

To test source files should be stored in src/test/scala, run:
```
sbt test
```

TODO: emacs scala
```
(use-package ensime
  :ensure t
  :pin melpa-stable)

sbt.version=0.13.16
libraryDependencies  ++= Seq(
   "org.ensime" % "sbt-ensime" % "2.4.0"
)
```

###### Scala compilation
project structure:
```
src/main/scala/com/fra/*.scala
```

to complie:
```
scalac src/main/scala/com/fra/*.scala
```

to execute: (package com.fra) at the top of project, run:
```
src/main/scala$ scala com.fra.main
```

###### Simple sbt / spark project
To create project structure:
```
sbt
```
It will generate the following structure:
```
./build.sbt
./src
./src/main
./src/main/scala
```

To create source file: SimpleApp.scala
```
./src/main/scala/SimpleApp.scala
```

Sample scala source file:
```
/* SimpleApp.scala */
import org.apache.spark.sql.SparkSession

object SimpleApp {
  def main(args: Array[String]) {
    val logFile = "YOUR_SPARK_HOME/README.md" // Should be some file on your system
    val spark = SparkSession.builder.appName("Simple Application").getOrCreate()
    val logData = spark.read.textFile(logFile).cache()
    val numAs = logData.filter(line => line.contains("a")).count()
    val numBs = logData.filter(line => line.contains("b")).count()
    println(s"Lines with a: $numAs, Lines with b: $numBs")
    spark.stop()
  }
}
```

Sample build.sbt
```
name := "Simple Project"
version := "1.0"
scalaVersion := "2.11.8"
libraryDependencies += "org.apache.spark" %% "spark-sql" % "2.2.0"
```

Specify sbt version, inside project/build.properties:
```
sbt.version=1.1.0
or
sbt.version=0.13.16
```

To package jars, change directory to the project level
```
sbt package
```

To run
```
spark-submit --class "SimpleApp" --master local[4] target/scala-2.11/simple-project_2.11-1.0.jar
```

### SBT
###### Installation
Example: Hello world template
```
sbt new sbt/scala-seed.g8
cd <project folder>
```

start sbt shell
```
sbt
```
To compile / package / run:
```
sbt [compile|package|run]
```

To quit shell:
```
exit (Ctrl-D)
```

Build definition file:
```
build.sbt
```

To create doc (at target/scala-xxx/api/)
```
sbt doc
```

Use run-main where there are multiple main
```
sbt "run-main ai.fra.Foo"
```

alternatively, add a line in build.sbt
```
mainClass in (Compile, run) := Some("ai.fra.Foo")
```

To set log level: build.sbt
```
set logLevel := Level.Debug | Level.Info | Level.Warning | Level.Error
```

###### install breeze
* edit build.sbt:

```
organization := "com.example"
name := "xxx"
scalaVersion := "2.12.3"

libraryDependencies ++= Seq(
"org.scalanlp" %% "breeze" % "0.13.2",
"org.scalanlp" %% "breeze-natives" % "0.13.2"
)
```

* pre-requisite
sudo apt-get install libatlas3-base libopenblas-base


###### conscript + giter8
* edit .bashrc
```
export CONSCRIPT_HOME="$HOME/.conscript"
export CONSCRIPT_OPTS="-XX:MaxPermSize=512M -Dfile.encoding=UTF-8"
export PATH=$CONSCRIPT_HOME/bin:$PATH
```

* install conscript
```
curl https://raw.githubusercontent.com/foundweekends/conscript/master/setup.sh | sh
```

* install / upgrade giter8
```
cs foundweekends/giter8
```


### SBT: spark project with giter8
giter8 can be called from sbt, e.g.
```
sbt new eed3si9n/hello.g8
```

Example: g8 spark Project Template
```
sbt new holdenk/sparkProjectTemplate.g8
```

update:
```
./project/plugins.sbt
./project/build.properties
build.sbt
```

For testing:
```
sbt "run inputFile.txt outputFile.txt"
```

Run Spark using submit command:
```
spark-submit \
  --class com.example.sparkgiter.CountingLocalApp \
  ./target/scala-2.11/sparkgiter_2.11-0.0.1.jar \
  ./alice_wonderland.txt ./output
```

### sbt + spark
###### log4j
* create src/main/resources
* copy log4j.properties to this folder

Add these lines to build.sbt
```
javaOptions in run ++= Seq("-Dlog4j.configuration=log4j.properties")
fork := true,
showSuccess := false,
logLevel in run := Level.Warn
```

log4j control in code:
```
import org.apache.log4j.{Level, Logger, LogManager}
LogManager.getRootLogger.setLevel(Level.OFF)
```

alternatively,
```
val rootLogger = Logger.getRootLogger()
rootLogger.setLevel(Level.ERROR)
LogManager.getRootLogger.setLevel(Level.OFF)
```

###### build.sbt
```
sparkVersion := "2.2.0",
sparkComponents := Seq(),
```

Additional libraries
```
libraryDependencies ++= Seq(
"org.apache.spark" %% "spark-streaming" % "2.2.0" % "provided",
"org.apache.spark" %% "spark-sql" % "2.2.0" % "provided",
"org.rogach" %% "scallop" % "3.1.1"
),
```

must have:
```
run in Compile := Defaults.runTask(fullClasspath in Compile, mainClass in (Compile, run), runner in (Compile, run)).evaluated,
```

suppress log output:
```
fork := true,
showSuccess := false
```

### Scala deployment
to show multiple main classes
```
sbt
show discoveredMainClasses
```

To package jars
```
sbt package
```

To list
```
jar tvf target/scala-2.10/basic_2.10-1.0.jar
```

To run by scala
```
scala target/scala-2.10/basic_2.10-1.0.jar
```

For java to run
```
java -cp "${CLASSPATH}:${SCALA_HOME}/lib/scala-library.jar:target/scala-2.10/basic_2.10-1.0.jar" foo.bar.baz.Main
```

###### Assemble all jar
add this line to plugin.sbt:
```
addSbtPlugin("com.eed3si9n" % "sbt-assembly" % "0.14.5")
```

add these two lines to build.sbt
```
import AssemblyKeys._
assemblySettings
```

Asseble all class by running:
```
sbt assembly
```

To run jars in scala:
```
scala target/scala-xxx/xxxx.jar
```

To run jars in java, scala-library.jar is required:
```
java -cp "${CLASSPATH}:${SCALA_HOME}/lib/scala-library.jar:target/scala-xxxx/xxxx.jar" ai.fra.Main
```


### Haskell
1. Install
```
sudo apt-get install haskell-platform
```

2. install ide for atom
```
cabal update
cabal install ghc-mod
```

3. add ~/.cabal/bin to PATH

4. inside atom, install
```
haskell-ghc-mod
ide-haskell
ide-haskell-cabal
language-haskell
autocomplete-haskell
```

### Go Lang
1. install via ppa
```
sudo add-apt-repository ppa:longsleep/golang-backports
sudo apt-get update
sudo apt-get install golang-go
```
alternatively
```
sudo add-apt-repository ppa:ubuntu-lxc/lxd-stable
sudo apt-get update
sudo apt-get install golang
```

2. alternative ppa:
```
sudo add-apt-repository ppa:longsleep/golang-backports
sudo apt-get update
sudo apt-get install golang-go
```

3. create a workspace by
```
mkdir $HOME/work
```

4. add these lines to .profile
```
export GOPATH=$HOME/Project/GoProj
export PATH=$PATH:$GOPATH/bin
```

5. GoCliipse
update site:
```
http://goclipse.github.io/releases/
```
choose only Goclipse

6. Download Tools:
these will be installed in $GOPATH/bin
```
gocode:
go get -u github.com/nsf/gocode
goguru:
go get golang.org/x/tools/cmd/guru
godef:
go get github.com/rogpeppe/godef
```

7. Setup
    * Under preferences, enter the path for gofmt as: /usr/bin/gofmt
    * set the GOROOT as: /usr/
    * Run configurations, set environment -> select -> check GOPATH


### JAVA

### Debian -- install oracle java:
1. debian repository
```
sudo apt-get install software-properties-common dirmngr
sudo add-apt-repository "deb http://ppa.launchpad.net/webupd8team/java/ubuntu yakkety main"
sudo apt update
```
2. we will see that error missing in the above update, so run:
```
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys C2518248EEA14886
sudo apt-get install oracle-java8-installer
```

3. To create soft link
```
sudo mkdir /usr/java
sudo ln -s /usr/lib/jvm/java-8-oracle /usr/java/latest
```
4. set up java path by editing .bashrc
```
export JAVA_HOME=/usr/java/latest
export JRE_HOME=$JAVA_HOME/jre
sudo mkdir /usr/local/lib/java
```
5. export CLASSPATH
```
export CLASSPATH=./:/usr/local/lib/java
```

###### Ubuntu -- install oracle java
For debian:
```
sudo apt-get install software-properties-common dirmngr
sudo add-apt-repository "deb http://ppa.launchpad.net/webupd8team/java/ubuntu yakkety main"
sudo apt update
```
we will see that error missing in the above update, so run:
```
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys C2518248EEA14886
sudo apt-get install oracle-java8-installer
```

For ubuntu:
```
sudo add-apt-repository ppa:webupd8team/java
sudo apt update
sudo apt install oracle-java8-installer
```

Check java version
```
java -version
```

Set up java path by editing /etc/profile:
```
JAVA_HOME=<path to oracle java>
JRE_HOME=$JAVA_HOME/jre
export JAVA_HOME
export JRE_HOME
PATH=$JAVA_HOME/bin:$JRE_HOME/bin:/usr/local/go/bin:$PATH
```

To add this line to /etc/apt/sources.list
```
deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main
```

To add GPG key
```
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886
```

###### javac
On Unix, we would do this: (in colon)
```
javac -classpath dir1:dir2:dir3 ...
```

To check class path
```
echo $CLASSPATH
```

To specify the class out directory
```
javac -d <class_out_dir>
```

######  NOTE:
if specifying -cp in command line, this would override the CLASSPATH setting!


###### Running java
use -cp to specific path (if not in the global class path)
example 1
```
current path:
~/FraDir/learn/introcs/out/production/introcs$

To run:
java -cp ./:/home/fra/FraDir/learn/introcs/stdlib-package.jar exercise.FindMinMax
(where the java class is under exercise/FindMinMax.class the package is called exercise)
```

example 2
```
to compile:
javac -cp ../stdlib.jar RandomSeq.java

to run: (need to add the current path)
java -cp ./:../stdlib.jar RandomSeq 10
```

###### Maven
To create folder structure:
```
mkdir -p src/main/java/hello
```

Project setup file: create a pom.xml in the same folder as src

compile
```
mvn compile
```

install
```
mvn clean install
```

Package structure
If the java class is part of a package
For example in Precedence.java, it begins with the package keyword followed by the structure

package com.operators;

```
[parent]
	[com]
		[operators]
```
in this case, run this command at the parent folder
```
java com.operators.Precedence
```

###### javadoc
To create html documentation
```
Usage: javadoc [options] [packagenames] [sourcefiles] [@files]
```

###### introcs
set up classpath set in .bashrc
Run java at /home/fra/FraDir/learn/introcs/src

e.g. Newton.java is part of the package introcs
```
javac introcs/Newton.java
java introcs.Newton
```

###### JAR package
To view contents a JAR file
```
jar tf <jar file>
```

to extract contents a JAR file
```
jar xf <jar file>
```

to create a JAR file
```
jar cf <jar file> <input files>
```

Bundle multiple files for deployment
```
jar cf <file.jar> <files...>
e.g.
jar cf test.jar package/*.class
```

To set main class in jar
```
jar xfe <file.jar> MainClass <file.class> ...
e.g.
jar cvfe package/Hello.jar pacakge.HelloWorld package/HelloWorld.class
```


### java tools
* To generate documentation of codes
```
javadoc <file.java>
e.g
javap <file.class>
```

* To display info of a class
```
e.g.
javap java.lang.String
```

* jcmd
To send diagnostic commands to a specified JVM

* jdb
Java debugger


### Mongodb
1. add key
```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
```

2. create sources.list
```
echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
```

3. install
```
sudo apt-get update
sudo apt-get install -y mongodb-org
```

4. For 16.04 only
Create a new file at /lib/systemd/system/mongod.service with the following contents:

```
[Unit]
Description=High-performance, schema-free document-oriented database
After=network.target
Documentation=https://docs.mongodb.org/manual

[Service]
User=mongodb
Group=mongodb
ExecStart=/usr/bin/mongod --quiet --config /etc/mongod.conf

[Install]
WantedBy=multi-user.target

```

5. Administration
    * manually start mongodb
```
sudo service mongod start
```
    * to manual stop
```
sudo service mongod stop
```
    * to manual restart
```
sudo service mongod restart
```

    * to check if mongo is running
```
service mongod status
```
    * check the log
```
/var/log/mongodb/mongod.log
```

    * mongo shell
```
mongo
```

    * create a user inside shell
    * to create root user
```
use admin
db.createUser({user:"admin", pwd:"admin123", roles:[{role:"root", db:"admin"}]
```

    * to login with root
```
mongo -u admin -p admin123 --authenticationDatabase admin
```

### Python
* pip
```
sudo apt-get install python-pip python3-pip
sudo apt-get install python-dev python3-dev
```

* To upgrade:
```
pip install --upgrade pip
pip3 install --upgrade pip
```

* to check sys.path:
```
python -m site
```

* python 2 scipy stack:
```
apt-get install python-numpy python-scipy python-matplotlib ipython ipython-notebook python-pandas python-sympy python-nose
```
* for python 3
```
apt-get install python3-numpy python3-scipy python3-matplotlib ipython3 ipython3-notebook python3-pandas python3-sympy python3-nose
```

* machine learning libraries
```
pip install numpy scipy matplotlib pandas sympy nose scikit-learn --user
pip3 install numpy scipy matplotlib pandas sympy nose scikit-learn --user
```

* Open ai gym
```
sudo apt-get install -y python-dev cmake zlib1g-dev libjpeg-dev xvfb libav-tools xorg-dev python-opengl libboost-all-dev libsdl2-dev swig
pip3 install gym
pip3 install gym[atari]
```

* install python3 libraries
```
pip install csvkit
pip install bokeh
pip install autograd
```

* spacy installation
    * download the gz file first
```
pip3 install en_core_web_sm-1.2.0.tar.gz --user
```
    * link the model as en
```
python3 -m spacy link en_core_web_sm en
```
    * other models:
```
python3 -m spacy link en_core_web_md en_default
```

* tkinter
```
sudo apt-get install python3-tk
```

* high numerical precision
```
sudo apt-get install libmpfr-dev
pip3 install bigfloat --user
```

* mysql (mariadb)
```
sudo apt-get install libmariadbclient-dev
pip3 install mysqlclient
```
* postgresql
```
pip3 install psycopg2
```
* SparkSQL
```
pip3 install pyhive
```

* mysql connector
download deb from MySQL
```
dpkg -i <package.db>
```


* python jupyter
To show pip package details
```
pip show jupyter
```

* TODO: virtualenv:
```
pip install virtualenv
pip3 install virtualenv
```

### python library
* PIP:
```
sudo apt-get install python-pip python3-pip
sudo apt-get install python-dev python3-dev
```

* to get a list of installed python packages:
```
import pip
installed_packages = pip.get_installed_distributions()
installed_packages_list = sorted(["%s==%s" % (i.key, i.version)
     for i in installed_packages])
print(installed_packages_list)
```

* Use sudo to pip install globally
```
system lib folder:
/usr/local/lib/
local lib folder:
~/.local/lib
local bin folder:
~/.local/bin
```

* To upgrade:
```
pip install --upgrade pip
```

* python 2 scipy stack:
```
sudo apt-get install python-numpy python-scipy python-matplotlib ipython ipython-notebook python-pandas python-sympy python-nose
```
* python 3
```
sudo apt-get install python3-numpy python3-scipy python3-matplotlib ipython3 ipython3-notebook python3-pandas python3-sympy python3-nose
pip install -U scikit-learn
pip install numpy scipy matplotlib pandas sympy nose
```

* install python3 libraries
```
pip install csvkit
pip install bokeh
pip install autograd
```

* Open ai gym
```
apt-get install -y python-dev cmake zlib1g-dev libjpeg-dev xvfb libav-tools xorg-dev python-opengl libboost-all-dev libsdl2-dev swig
```

TODO: install pyqt

* theano
```
pip install Theano
```

TODO: cntk
TODO: tensorflow


### MIT-Scheme
```
sudo apt-get install mit-scheme
```
to run in emacs
```
M-x run-scheme
```


### Lua Torch
Install LuaJIT + Torch
1. in a terminal, run the commands WITHOUT sudo and download the installer codes to temporary folder
```
git clone https://github.com/torch/distro.git ~/torch --recursive
```

2. start the installation to install LuaJIT and LuaRocks
```
cd ~/torch; bash install-deps;
./install.sh
```

3. add torch to the path
source ~/.profile

4. install packages
run luarocks WITHOUT sudo
```
luarocks install image
luarocks list
```

5. torch will be installed at ~/torch
The path is specified in
```
~/torch/install/bin/torch-activate
```

6. If using Lua instead (not recommended)
Install Lua5.2 + Torch
```
git clone https://github.com/torch/distro.git ~/torch --recursive
cd ~/torch
./clean.sh
TORCH_LUA_VERSION=LUA52 ./install.sh
```
other method:
```
curl -s https://raw.github.com/clementfarabet/torchinstall/master/install-all | bash
```


### Node.js (Debian)
```
curl -sL https://deb.nodesource.com/setup_8.x | sudo bash -
```
alternatively,
```
sudo apt-get install nodejs
```

* check version
```
node -v
npm -v
```

* testing install:
Run the following javascript:
```
var http = require('http');
http.createServer(function (req, res) {
  res.writeHead(200, {'Content-Type': 'text/plain'});
  res.end('Hello World\n');
}).listen(3000, "127.0.0.1");
console.log('Server running at http://127.0.0.1:3000/');
```

### npm
1. install package (global)
```
npm install <pacakge> -g
```

2. install package (local)
```
npm install <pacakge>
```

3. update
```
npm update
```

4. remove
```
npm uninstall <package>
```

5. list package
```
npm list
```

6. alternatively:
```
sudo apt-get nodejs-legacy npm
```


### Node packages
* FIXME:
```
npm install dstools -g
```
* jquery
```
npm install jquery
```

### nodejs - ubuntu
```
sudo add-apt-repository ppa:chris-lea/node.js
sudo apt-get install nodejs
```

* alternatively, install node.js v6.x
```
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
```

* or node js setup (ppa)
```
curl -sL https://deb.nodesource.com/setup_6.x -o nodesource_setup.sh
sudo bash nodesource_setup.sh
sudo apt-get install nodejs
```

### Erlang
```
sudo apt-get install erlang
```


### Mahout
* git clone from source

* edit .bashrc
```
export MAHOUT_HOME=/home/fra/Project/javaProj/mahout
export MAHOUT_LOCAL=true
export MASTER=local[*]
```
* to point to a cluster with spark running
```
export MASTER=spark://localhost:7077
```

* to build
```
mvn -DskipTest clean install
```

* to test
```
mvn test
```

* to set up IDE for each project, create a POM file, then
```
mvn eclipse:eclipse
mvn idea:idea
```

* run mahout's spark shell
```
mahout spark-shell
```

### DL4J project
* create new project (Maven)
    * choose achetype: quick start

* Download looging library from:
```
https://www.slf4j.org/index.html
```

* copy these jar
```
slf4j-log4j12-1.7.25.jar
slf4j-jdk14-1.7.25.jar
```
to /usr/local/lib/java