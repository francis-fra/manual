### Optimization packages
* SCIP

Download binary from scipopt.org
'''
sudo dpkg -i SCIPOptSuite-8.0.0-Linux-ubuntu.deb 
```
if dependecies are missing
```
sudo apt-get -f install
'''
python wrapper
```
pip install pyscripopt
```
* CVXOPT

```
pip install cvxopt
```
* CBC

install
```
sudo apt-get install  coinor-cbc coinor-libcbc-dev
```
install python wrapper
```
pip install cylp
```

### Julia

Download the lastest version and link
```
wget https://julialang-s3.julialang.org/bin/linux/x64/1.7/julia-1.7.3-linux-x86_64.tar.gz
tar -xvf julia-1.7.3-linux-x86_64.tar.gz
sudo mv julia-1.7.3/ /opt/
sudo ln -s /opt/julia-1.7.3/bin/julia /usr/local/bin/julia
```

setup startup file
to prevent precompile error with system env
```
mkdir ./julia/config
echo 'println("Greetings! 你好!")' >> ~/.julia/config/startup.jl
echo 'ENV["LD_LIBRARY_PATH"] = ""' >> ~/.julia/config/startup.jl

```

### Prolog

add ppa
```
sudo apt-add-repository ppa:swi-prolog/stable
sudo apt-get update
sudo apt-get install swi-prolog
```

### Deno
* system wide install
```
curl -fsSL https://deno.land/x/install/install.sh | sudo DENO_INSTALL=/usr/local sh
```
* upgrade
```
sudo deno upgrade
```

### dotnet 5.0

* install via apt
```
wget https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
sudo apt update
sudo apt-get install -y apt-transport-https 
sudo apt-get install -y dotnet-sdk-5.0
```

check install sdk
```
dotnet --list-sdks
```

### install dotnet 6.0
```
wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
sudo apt-get update
sudo apt-get install -y dotnet-sdk-6.0

```

### dotnet CLI
```
dotnet add package <name>
```

### emscripten
* Download from github
```
git clone https://github.com/emscripten-core/emsdk.git
mv emsdk /opt
cd emsdk
```
* Get the latest tools and set PATH
```
./emsdk install latest
./emsdk activate latest
source ./emsdk_env.sh --build=Release
```
* Verify installation
```
emcc -v

```
* Update the SDK
```
./emsdk update
./emsdk install latest
./emsdk activate latest
source ./emsdk_env.sh
```
* show current config
```
emsdk list
```
Emscripten compiler configuration file:
```
~/.emscripten
```

### cmake

To install the latest cmake:
remove existing:
```
sudo apt remove --purge cmake
```
install via snap
```
sudo snap install cmake --classic
```

### Unity: C Unit Testing Framework
* build using cmake/make
```
git clone https://github.com/ThrowTheSwitch/Unity
cd Unity
mkdir build
cd build
cmake ..
make
```
* install files to /usr/local/lib and /usr/local/include
```
make install
-- Install configuration: ""
-- Installing: /usr/local/lib/libunity.a
-- Installing: /usr/local/include/unity/unity.h
-- Installing: /usr/local/include/unity/unity_internals.h
-- Installing: /usr/local/lib/cmake/unity/unityTargets.cmake
-- Installing: /usr/local/lib/cmake/unity/unityTargets-noconfig.cmake
-- Installing: /usr/local/lib/cmake/unity/unityConfig.cmake
-- Installing: /usr/local/lib/cmake/unity/unityConfigVersion.cmake
```
* set c include path in .bash_profile
```
export C_INCLUDE_PATH=$C_INCLUDE_PATH:/usr/local/include/unity
```

* check
```
ls /usr/local/lib/libunity.a
ls /usr/local/include
```


### gcc

* install gsl
```
sudo apt install pkg-config
sudo apt install libgsl-dev
```
* other blas lib
```
sudo apt install libblas-dev liblapack-dev
```

* to locate lib/include files
```
locate gsl_rng.h
find /usr -name gsl_rng.h
find /usr -name libgsl.so
```

* Linking
1. compile to executable
```
gcc -L/usr/lib/x86_64-linux-gnu gsl_test.c -lgsl -lgslcblas -lm 
```

2. compile to object
```
gcc -L/usr/lib/x86_64-linux-gnu -c gsl_test.c -lgsl -lgslcblas -lm 

```

* system evn
-L path can be omitted if the path is exported to system env
* edit .bash_profile
```
export LIBRARY_PATH=$LIBRARY_PATH:/usr/lib/x86_64-linux-gnu
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/lib/x86_64-linux-gnu

```
* compile statically
```
gcc -static gsl_test.o -lgsl -lgslcblas -lm
```


* supply macro at command line
e.g. define TEST
```
gcc -DTEST <source file>
```
e.g. define NUM as 100
```
gcc -DNUM=100 <source file>
```

#### Compile and link
1. compile preprocess only
```
gcc -E hello.c > hello.i
```
alternatively
```
cpp  hello.c > hello.i
```
2. compile to assembly language
outcome has suffix .s
```
gcc -S hello.i
```
3. generate object file
```
as hello.s -o hello.o
```
4. generate executable file
```
gcc hello.o -o hello
```
5. examine file
```
file hello.i
file hello.s
file hello.o
file hello
```
6. create object dump
```
objdump -D hello.o > hello.txt
```

#### 64-bit register
e.g.
```
(gdb) i r
rax            0x555555555125      93824992235813
rbx            0x0                 0
rcx            0x7ffff7fc3718      140737353889560
rdx            0x7fffffffdd48      140737488346440
rsi            0x7fffffffdd38      140737488346424
rdi            0x1                 1
rbp            0x7fffffffdc40      0x7fffffffdc40
rsp            0x7fffffffdc40      0x7fffffffdc40
r8             0x0                 0
r9             0x7ffff7fe2180      140737354015104
r10            0x3                 3
r11            0x2                 2
r12            0x555555555040      93824992235584
r13            0x0                 0
r14            0x0                 0
r15            0x0                 0
rip            0x555555555129      0x555555555129 <main+4>
eflags         0x246               [ PF ZF IF ]
cs             0x33                51
ss             0x2b                43
ds             0x0                 0
es             0x0                 0
fs             0x0                 0
gs             0x0                 0
```


### g++
check default compiler version
```
g++ -dM -E -x c++  /dev/null | grep -F __cplusplus
```

### Google Test
* Install and build with cmake
```
sudo apt-get install libgtest-dev
cd /usr/src/googletest/googletest
sudo mkdir build
cd build
sudo cmake ..
sudo make
sudo cp -a libgtest*.a /usr/lib/
```
remove build folder (optional)
```
cd ..
sudo rm -rf build
```
create symbolic links
```
sudo mkdir /usr/local/lib/googletest
sudo ln -s /usr/lib/libgtest.a /usr/local/lib/googletest/libgtest.a
sudo ln -s /usr/lib/libgtest_main.a /usr/local/lib/googletest/libgtest_main.a
```


### SDL Development library
```
sudo apt-get install libsdl2-2.0
sudo apt-get install libsdl2-dev
sudo apt-get install libsdl2-image-dev
sudo apt-get install libsdl2-ttf-dev
sudo apt-get install libsdl2-mixer-dev
```

### flex and bison
```
sudo apt install flex bison
```

### Heroku 

Install
```
curl https://cli-assets.heroku.com/install.sh | sh
```

Deployment
```
heroku login
heroku create
```
the remote will be printed at the stdout

```
heroku git:remote -a <remote id>
```
To deploy
```
heroku config:set DISABLE_COLLECTSTATIC=1
git push heroku master
heroku ps:scale web=1
```
to open app
```
heroku open
```

### Racket
```
sudo add-apt-repository ppa:plt/racket
sudo apt-get update
sudo apt install racket
```

### ReasonML
```
npm install -g bs-platform
```

### SML
```
sudo apt-get install gcc-multilib
sudo apt-get install smlnj
sudo apt install rlwrap
```
To run sml with arrow key history
```
rlwrap sml
```

### PolyML
```
sudo apt install polyml
```

### Lisp
```
sudo apt install sbcl
```
Install quicklisp
```
sudo apt install cl-quicklisp
```
in REPL:
```
(load "/usr/share/cl-quicklisp/quicklisp.lisp")
(quicklisp-quickstart:install)
To start
```
(load "/usr/share/cl-quicklisp/quicklisp.lisp")
(load "~/quicklisp/setup.lisp")
```
To auto load each time
```
(ql:add-to-init-file)
```

```
Install libraries
```
(ql:quickload "package-name")
```

To load a system, use: (ql:quickload "system-name")
To find systems, use: (ql:system-apropos "term")
To load Quicklisp every time you start Lisp, use: (ql:add-to-init-file)

### Scheme
```
sudo apt install mit-scheme
sudo apt install guile-2.2
```

### R -- Debian - deprecated
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
sudo chmod o+w /usr/local/lib/R/site-libray
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
###### Install R and R Studio
1. add GPG key
```
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
```
2. add repository
```
sudo add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/'
sudo apt update
```

3. Download the latest deb file
'''
sudo apt install gdebi-core
sudo gdebi rstudio-1.2.5019-amd64.deb
'''

4. additional packages for RCurl:
```
sudo apt-get install libcurl4-openssl-dev
sudo apt-get install libxml2-dev
sudo apt-get install libssl-dev
sudo apt-get install libnlopt-dev
```

###### Install R jupyter kernel

install packages and register kernel
```
install.packages('IRkernel')
IRkernel::installspec()
```
###### Install Rstan
Add Michael Rutter's c2d4u4.0 PPA (and rrutter4.0 for CRAN builds too)
```
sudo add-apt-repository ppa:marutter/rrutter4.0
sudo add-apt-repository ppa:c2d4u.team/c2d4u4.0+
sudo apt update
sudo apt install r-cran-rstan
```
Install
```
remove.packages("rstan")
if (file.exists(".RData")) file.remove(".RData")
Sys.setenv(DOWNLOAD_STATIC_LIBV8 = 1) # only necessary for Linux without the nodejs library / headers
install.packages("rstan", repos = "https://cloud.r-project.org/", dependencies = TRUE)
```
To test if ok:
```
example(stan_model, package = "rstan", run.dontrun = TRUE)
```

###### Install jags
```
sudo apt install jags
```


###### Install R -- deprecated
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

### GWT
1. Download the zip file and unzip to /opt
2. Make the script executable
```
ln -s /opt/gwt-2.8.2 /opt/gwt
cd /opt/gwt
chmod u+x webAppCreator
```
3. Add to the source path
4. Test
```
webAppCreator -out MyWebApp com.mycompany.mywebapp.MyWebApp
cd MyWebApp
ant devmode
```
5. Compile and RUn in production mode
```
ant build
```

### Opam + Ocaml
Install
```
add-apt-repository ppa:avsm/ppa
apt update
apt install opam
```
Initialize
```
opam init -y --compiler=4.07.1
```
Update shell environment
```
eval $(opam env)
```
To switch (or install) compiler
```
opam switch create 4.07.1
eval $(opam env)
```
update and upgrade packages
```
opam update -uy
opam upgrade
```
Install basic package
```
opam install base core_kernel ounit utop core
opam install async yojson core_extended core_bench cohttp async_graphics cryptokit menhir
```
list available packages
```
opam list -a
```
list installed packages
```
opam list
```
list available compiler
```
opam switch
```

opam package install 
```
opam install utop
opam install merlin
opam user-setup install
```

Setting up utop
edit ~/.ocamlinit
```
#use "topfind";;
#thread;;
#require "core.top";;
#require "core.syntax";;
open Base;;
open Core;;
```

### Dune
init project
```
dune init exe <proj_name>
```
Edit dune file, then build project
```
dune build <exe_name>
```
run project
```
dune exec <proj_name>
```

### Ocaml only
Install ocaml
```
apt install ocaml
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

### Rust REPL
Update rust if necessary
```
rustup update
```
Install
```
rustup component add rust-src
cargo install evcxr_repl
```
Run: Evaluator (Ev) Context (cx) for Rust (r)
```
evcxr
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

### Kotlin
* using SDKMAN!
```
sdk install kotlin
```

### Groovy
* using SDKMAN!
```
sdk install groovy
groovy -version
```

* install eclipse plugin (Neon)
```
http://dist.springsource.org/snapshot/GRECLIPSE/e4.6/
```

### Scala (deprecated - use SDKMAN!)
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

* java install (deprecated - use SDKMAN!)
```
sudo apt-get install python-software-properties
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
```
### Java installation
```
sdk install java 11.0.2-open
```

### SDKMAN!
Download
```
curl -s "https://get.sdkman.io" | bash
```
Initialize
```
source "$HOME/.sdkman/bin/sdkman-init.sh"
```
Check
```
sdk version
```
Available java
```
sdk ls java
sdk ls scala
sdk ls gradle
etc...
```
To change anaother installed version
```
sdk use java 11.0.2-open
```
To uninstall
```
sdk uninstall java 8.0.201-oracle
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

### Yarn
Configure repository
```
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
```
Update respository and install
```
sudo apt-get update && sudo apt-get install yarn
```
To check global directory
```
yarn global dir
```


### Ruby
Install package
```
sudo gem install <package>
```
e.g. minitest

### Haskell
1. Haskell platform (including gchi, cabal, stack, etc...)
```
sudo apt-get install haskell-platform
```
ghc only
```
sudo add-apt-repository -y ppa:hvr/ghc
sudo apt-get update
sudo apt-get install -y cabal-install-XXX ghc-YYY
```
2. upgrade stack
```
stack upgrade
```

3. add ~/.cabal/bin to PATH

4. edit config file
```
~/.stack/config.yaml
```


### Haskell Tool Stack
1. Installation
```
curl -sSL https://get.haskellstack.org/ | sh
```
2. Install package via stack
```
stack --version
stack install hlint
```

3. Start new project
```
stack new <my_project>
cd <my_project>
stack setup
stack build
stack exec <my_project_exe>
```
4. run test
```
stack test
```
5. running GHCi
```
stack ghci
```

6. check installed packages
```
stack exec ghc-pkg -- list
```

### Go Lang
1. install via ppa
```
sudo add-apt-repository ppa:longsleep/golang-backports
sudo apt-get update
sudo apt-get install golang-go
```
alternatively,
```
sudo add-apt-repository ppa:ubuntu-lxc/lxd-stable
sudo apt-get update
sudo apt-get install golang
```
Alternatively, download and extract Linux tarballs:
```
sudo tar -C /usr/local -xzf go1.10.3.linux-amd64.tar.gz
```
or
```
wget https://dl.google.com/go/go1.12.2.linux-amd64.tar.gz
sudo tar -xvf go1.12.2.linux-amd64.tar.gz
sudo mv go /usr/local
```

2. create a workspace by
```
mkdir $HOME/Project/GoProj
```

3. add these lines to .profile
```
export GOROOT=/usr/lib/go
export GOPATH=$HOME/Project/GoProj
export PATH=$PATH:$GOPATH/bin:$GOROOT/bin
```

4. GoCliipse
update site:
```
http://goclipse.github.io/releases/
```
choose only Goclipse

5. Download Tools:
these will be installed in $GOPATH/bin
```
gocode:
go get -u github.com/nsf/gocode
goguru:
go get golang.org/x/tools/cmd/guru
godef:
go get github.com/rogpeppe/godef
```

6. Setup
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

##### Gradle
Install via SDKMAN
```
sdk install gradle <version>
```
check version
```
gradle -v
```
Update PATH
```
export PATH=$PATH:/home/fra/.sdkman/candidates/gradle/current/bin
```
To start a gradle build project
```
gradle init --type java-application
```
To run application
```
./gradlew bootRun
```
To build JAR
```
./gradlew build
```

#### Gradle Project
* Create a new project
```
gradle init --type java-application
```
* Configuration file - add to build.gradle
```
apply plugin: 'java'
```
* Compile Java classes
```
gradle compileJava
```
* Build the project
```
gradle build
```
* To run task 'mytask'
```
gradle -q mytask
```
* To run test
```
gradle test
```
* Run the application
```
gradle -q run
```




###### Maven
To create folder structure:
```
mkdir -p src/main/java/hello
```
Project setup file: create a pom.xml in the same folder as src

There are a number of phrases:
* validate
* compile
* test
* package
* integration-test
* verify
* install
* deploy

To compile, the byte code is stored at target/classes
```
mvn compile
```
To build, either
```
mvn install
mvn clean install
```
Maven assembly plugin example
```
<!-- Maven Assembly Plugin -->
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-assembly-plugin</artifactId>
  <version>3.1.0</version>
  <configuration>
	  <!-- get all project dependencies -->
	  <descriptorRefs>
		  <descriptorRef>jar-with-dependencies</descriptorRef>
	  </descriptorRefs>
	  <!-- MainClass in mainfest make a executable jar -->
	  <archive>
	    <manifest>
		  <mainClass>com.mycompany.app.Main</mainClass>
	    </manifest>
	  </archive>

  </configuration>
  <executions>
    <execution>
	  <id>make-assembly</id>
	  <!-- bind to the packaging phase -->
	  <phase>package</phase>
	  <goals>
		  <goal>single</goal>
	  </goals>
    </execution>
  </executions>
</plugin>

```
Maven jar plugin example
```
<plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-jar-plugin</artifactId>
      <version>3.1.0</version>
      <configuration>
	  <archive>
	  <manifest>
	      <addClasspath>true</addClasspath>
	      <mainClass>com.mycompany.app.Main</mainClass>
	  </manifest>
	  </archive>
    </configuration>
</plugin>
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
To view contents of the fiel inside JAR
```
unzip -p <file.jar> <file_to_view>

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

### Setting MANIFEST file
* MANIFEST.MF example:
note that a new line must be present at the end of file
```
Main-Class: com.mycompany.app.Main
Class-Path: ../lib/commons-lang3-3.1.jar
```
* run at ./build
```
java com.mycompany.app.Main
```
* Create a MANIFESTMF file and then package into a jar file
```
jar cvmf ../dist/MANIFEST.MF ../dist/example.jar  com/mycompany/app/Main.class
```
* run jar file at ./dist
```
java -jar example.jar
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

* Show GC info
```
java -XX:+UseSerialGC -XX:+PrintGCDetails -version
java -XshowSettings:vm -version
```

* Set heap size
e.g. 120MB
```
java -Xmx120m -XshowSettings:vm -version
```


### Bash Automated Testing System
installation
```
sudo apt install bats
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
python3 -m pip install --upgrade pip
```
* To list/freeze from different path
```
pip3 list --path xxxx/lib/python3.6/site-packages/

```
* install from requirements
```
pip freeze > requirements.txt
pip install -r requirements.txt
```
* remove requirements.txt without version
```
sed -i 's/=.*//' requirements.txt
```

* to check sys.path:
```
python -m site
```


* Open ai gym
```
sudo apt-get install -y python-dev cmake zlib1g-dev libjpeg-dev xvfb libav-tools xorg-dev python-opengl libboost-all-dev libsdl2-dev swig
pip3 install gym
pip3 install gym[atari]
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

* virtualenv:
Installation
```
pip3 install virtualenv
```
Create a virtual env
```
python3 -m venv <virtual_env_name>
```
Activation
```
source <vitual_env_name>/bin/activate
```
Deativate
```
deactivate
```

* pipenv
Install
```
pip3 install pipenv
```

### pyenv
install
```
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
```
place these lines in .profile (before sourcing .bashrc)
```
export PYENV_ROOT=$HOME/.pyenv
export PATH=$PYENV_ROOT/bin:$PATH
```
and then place this line at the end of .profile
```
eval "$(pyenv init --path)"
```
check available versions
```
pyenv install --list
```
check installed versions
```
pyenv versions
```
check current python path
```
pyenv which python
```

### pyenv-virtualenv
Download plugin
```
git clone https://github.com/pyenv/pyenv-virtualenv.git $(pyenv root)/plugins/pyenv-virtualenv
```
put this line in .bashrc
```
eval "$(pyenv virtualenv-init -)"
```
To create virtual environment  
```
pyenv virtualenv <python_verson> <environment_name>
```
Make the current folder using the environment
```
pyenv local <environment_name>
```
unset local version
```
pyenv local --unset
```
remove a virtual environment
```
pyenv uninstall <environment_name>
```
list virtual env
```
pyenv virtualenvs
```


### python libraries
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

* Use sudo to pip install globally (not recomended)
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

* python 3
```
sudo apt-get install python3-numpy python3-scipy python3-matplotlib ipython3 ipython3-notebook python3-pandas python3-sympy python3-nose

pip install numpy scipy matplotlib pandas sympy nose
```

* install python3 libraries
```
pip install jupyterlab
pip install -U scikit-learn
pip install -U matplotlib
pip install pandas
pip install csvkit
pip install autograd
```

* Open ai gym
```
apt-get install -y python-dev cmake zlib1g-dev libjpeg-dev xvfb libav-tools xorg-dev python-opengl libboost-all-dev libsdl2-dev swig
```

* Deep Learning libraries
```
pip install Theano
pip install keras
pip install tensorflow
```


### MIT-Scheme
```
sudo apt-get install mit-scheme
```
to run in emacs
```
M-x run-scheme
```
### Erlang (deb)
Set up apt repository
```
wget https://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb
dpkg -i erlang-solutions_1.0_all.deb
```
Install
```
sudo apt update
```

### Erlang (Ubuntu)
Import repository GPG
```
wget -O- https://packages.erlang-solutions.com/ubuntu/erlang_solutions.asc | sudo apt-key add -
```
Add Erlang Repository
```
echo "deb https://packages.erlang-solutions.com/ubuntu bionic contrib" | sudo tee /etc/apt/sources.list.d/rabbitmq.list
```


### Erlang (Debian)
Set up apt repository, create repository file at:
```
/etc/apt/sources.list.d/erlang-solutions.erlang.list
```
Type the following in the file:
```
deb https://packages.erlang-solutions.com/debian stretch contrib
```
Add signing key
```
wget https://packages.erlang-solutions.com/debian/erlang_solutions.asc
sudo apt-key add erlang_solutions.asc
```

### Install Erlang
```
sudo apt-get update
sudo apt-get install esl-erlang
```

### Elixir
Make sure Erlang is installed first
```
sudo apt-get install elixir
```


### Erlang (bintray repository)
Add signing Key
```
wget -O - 'https://dl.bintray.com/rabbitmq/Keys/rabbitmq-release-signing-key.asc' | sudo apt-key add -
```
Set up apt repository, create repository file at:
```
/etc/apt/sources.list.d/bintray.erlang.list
```
Type the following in the file:
```
deb http://dl.bintray.com/rabbitmq/debian stretch erlang
```
Install Erlang packages
```
sudo apt-get update
sudo apt-get install erlang-nox
```

### RabbitMQ
Add signing Key
```
wget -O - 'https://dl.bintray.com/rabbitmq/Keys/rabbitmq-release-signing-key.asc' | sudo apt-key add -
```
Set up apt repository, create repository file at:
```
/etc/apt/sources.list.d/bintray.rabbitmq.list
```
Type the following in the file:
```
deb http://dl.bintray.com/rabbitmq/debian stretch main
```
Install RabbitMQ packages
```
sudo apt-get update
sudo apt-get install rabbitmq-server
```

Download Java client library (jar)
```
amqp-client-5.30.jar
``
copy to the CLASSPATH
```

### LLVM (Ubuntu)
Default packages
```
apt install clang-format clang-tidy clang-tools clang clangd libc++-dev libc++1 libc++abi-dev libc++abi1 libclang-dev libclang1 liblldb-dev libllvm-ocaml-dev libomp-dev libomp5 lld lldb llvm-dev llvm-runtime llvm python3-clang
```
check
```
clang --version
clang++ --version
```

### NIM
```
sudo apt-get install nim
```

### SFML
Install via apt-get
```
sudo apt-get install libsfml-dev
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

### Node.js (nvm)
Install nvm
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
source ~/.bashrc
```
To check installed version
```
nvm list
```
To Install
```
nvm install <version>
```
Upgrade npm
```
nvm install-latest-npm
```


### Node.js (Ubuntu)
Install LTS version
```
sudo apt-get install curl python-software-properties
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt install nodejs
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

* Upgrade node
```
sudo npm cache clean -f
sudo npm install -g n
sudo n stable
```

### npm
1. install package (global)
```
npm install <pacakge> -g
```

2. install package (local)
```
npm install <package>
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
npm list [-g]
```

6. alternatively:
```
sudo apt-get nodejs-legacy npm
```

7. Install latest npm
```
npm install npm@latest -g
```

### npm global package lib
Either one of these two:
```
/usr/lib/node_modules
/usr/local/lib/node_modules
```

### npm config
* To list all config settings:
```
npm config ls -l
```
* To get key
```
npm config get prefix
```
* To set different prefix:
```
mkdir ~/.npm-packages
npm config set prefix ~/.npm-packages
```
* The user config file will be located at:
```
~/.npmrc
```
check it by:
```
npm config get userconfig
```


### npm package
* check updated version
```
npm outdated -g
```
* update
```
npm update <package name>
```
* Show global packages
```
npm list -g --depth=0
```
* common Packages
```
lodash
underscore
async
babel-core
express
```


### npm project
* Set up project
```
npm init -y
```
* package.json file is created


### TypeScript
To Install
```
npm install -g typescript
npm install -g ts-node
```
Check version
```
tsc --version
```

### npm config (package.json)
* To use global package at local
```
npm link <package>
e.g. npm link @types/node
```
* Babel 7 + jest + gulp package.json
```
{
  "private": true,
  "version": "0.0.0",
  "name": "example-babel-7",
  "devDependencies": {
    "@babel/core": "*",
    "@babel/preset-env": "*",
    "babel-core": "7.0.0-bridge.0",
    "babel-jest": "*",
    "gulp": "^4.0.0",
    "gulp-babel": "*",
    "gulp-uglify": "*",
    "gulp-rename": "*",
    "jest": "*"
  },
  "babel": {
    "presets": [
      "@babel/preset-env"
    ]
  },
  "scripts": {
    "test": "jest ./test/*"
  }
}
```
* To use babel 7, put these in package.json
```
"babel": {
  "presets": [
    "@babel/preset-env",
    "@babel/preset-react"
  ]
},
"devDependencies": {
  "@babel/core": "7.0.0",
  "@babel/preset-react": "7.0.0",
  "@babel/cli": "7.0.0"
}
```
* common devDependencies
```
"devDependencies": {
  "babel-eslint": "^10.0.1",
  "babel-jest": "^21.2.0",
  "babel-plugin-transform-builtin-extend": "^1.1.2",
  "babel-preset-env": "^1.7.0",
  "eslint": "^5.6.0",
  "eslint-config-airbnb-base": "^13.1.0",
  "eslint-plugin-import": "^2.14.0",
  "jest": "^23.6.0"
},
```
* scripts command
```
"scripts": {
  "test": "jest --no-cache ./*",
  "watch": "jest --no-cache --watch ./*",
  "lint": "eslint .",
  "lint-test": "eslint . && jest --no-cache ./* "
},
```
* Packages for Gulp task automation and test runner
```
npm install -g gulp-cli
npm install -g tslint
npm install -g gulp-typescript
npm install -g mocha chai
npm install -g @types/mocha @types/chai
```

### Node config
Show configuration
```
npm config ls -l
```
Default user config
```
$HOME/.npmrc
```

### yarn
Check global installation path
```
yarn global dir
```
Add global after yarn for global operations
```
yarn global <add/bin/list/remove/upgrade>
```

### Gulp.js
* Prepare Gulp file: gulpfile.js or gulfile.ts
* To run:
```
gulp <task name>
```

### Babel
Install packages:
```
npm install babel-cli -g
npm install babel-core -g
npm install babel-preset-env -g
```
Create a file called .babelrc, and add:
```
{
  "presets": ["env"]
}
```
* To run es6 javascript, make sure to local link:
```
npm link babel-cli
npm link babel-preset-env
```
* Run the file by:
```
babel-node file.js
```
* Compile using babel
```
npx babel file.js -o out.js
```

### Webpack-dev-server
To resolve the issues preventing HMR:

To make it temporary
```
echo 100000 | sudo tee /proc/sys/fs/inotify/max_user_watches
```
alternatively,
```
sudo sysctl fs.inotify.max_user_watches=524288
sudo sysctl -p
```

To make it permanent
```
echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf
sudo sysctl -p

```


### React.js
* Installation
```
npm install -g create-react-app
```
* upgrade
```
npm install @babel/plugin-transform-react-jsx -g
npm install @babel/core @babel/cli @babel/preset-react @babel/preset-env -g
npx babel-upgrade
```
* Transpile JSX to JS
```
babel --plugins @babel/plugin-transform-react-jsx xxx.js
```
* In browser transpiler
```
TODO
```

### Boost library
```
sudo apt-get install libboost-all-dev
```

### GSL & GNUPlot library
```
sudo apt-get install gsl-bin libgsl-dbg libgsl-dev libgsl2
sudo apt-get install gnuplot
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

### Erlang (deprecated)
```
sudo apt-get install erlang
```

### Crystal
* Auto add repository and update
```
curl https://dist.crystal-lang.org/apt/setup.sh | sudo bash
```
* Manual configuration
```
curl -sL "https://keybase.io/crystal/pgp_keys.asc" | sudo apt-key add -
echo "deb https://dist.crystal-lang.org/apt crystal main" | sudo tee /etc/apt/sources.list.d/crystal.list
sudo apt-get update
```
* Configure repository (old)
```
apt-key adv --keyserver keys.gnupg.net --recv-keys 09617FD37CC06B54
echo "deb https://dist.crystal-lang.org/apt crystal main" > /etc/apt/sources.list.d/crystal.list
apt-get update
```
* Install
```
sudo apt-get install crystal
```
* optional lib
```
sudo apt install libssl-dev libxml2-dev libyaml-dev libgmp-dev libreadline-dev libz-dev

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

* copy these jar to /usr/local/lib/java
```
slf4j-log4j12-1.7.25.jar
slf4j-jdk14-1.7.25.jar
```
