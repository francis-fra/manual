### Visual Studio Code
* Installation
```
sudo apt install software-properties-common apt-transport-https wget
wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
sudo apt update
sudo apt install code
```
* Download deb file (deprecated)
```
sudo dpkg -i <file>.deb
sudo apt-get update
sudo apt-get install code
```
* Install plugins, e.g. Excel Viewer, Rust, Code Runner...etc
* Configure Integrated Terminal
```
Preferences -> Keyboard shortcuts
Run Active File at Terminal
```
##### Node.js Setup
* Edit jsconfig.json
```
{
    "compilerOptions": {
        "target": "ES6"
    },
    "exclude": [
        "node_modules",
        "**/node_modules/*"
    ]
}
```

##### TypeScript Project Setup
* Edit tsconfig.json
```
{
    "compilerOptions": {
        "target": "es5",
        "module": "commonjs",
        "sourceMap": true
    }
}
```
* TypeScript build
```
Task -> Run Build Task
```
* Configure Default Build Task
```
Task -> Configure Default Buid Task
```


### Eclipse - Debian
* Download installer for Java Developer
* extract to /opt
* edit desktop entry:
```
sudo gedit /usr/share/applications/eclipse.desktop
```

* create a new symbolic link:
```
sudo ln -s /opt/eclipse/eclipse /usr/local/bin/
sudo ln -s /home/fra/eclipse/latest/eclipse/eclipse /usr/local/bin/
[Desktop Entry]
Name=Eclipse Oxygen
Type=Application
Exec=/usr/local/bin/eclipse
Terminal=false
Icon=/home/fra/eclipse/latest/eclipse/icon.xpm
Comment=Integrated Development Environment
NoDisplay=false
Categories=Development;IDE;
Name[en]=Eclipse Oxygen
```

* install the desktop entry:
```
sudo desktop-file-install /usr/share/applications/eclipse.desktop
```

###### install statET
1. Install STATET
```
Help -> Install new software
```
2. Enter site:
```
http://download.walware.de/eclipse-4.6
```
alternatively, install via eclipse marketplace

3. Set up R run environment
```
Preference -> StatET -> Run/Debug -> R environment
```
4. Auto detect environment
```
The R home should be in : /usr/lib/R
```

5. Set up Run configurations:
```
use Rterm not RJ!!
```

### eclipse - ubuntu
* install via installer (do not use sudo)
```
./eclipse-inst
```

* installation path:
```
/home/fra/eclipse
```

* create a new symbolic link:
```
ln -s /home/fra/eclipse/java-oxygen /home/fra/eclipse/lates
sudo ln -s /home/fra/eclipse/latest/eclipse/eclipse /usr/local/bin/
```
* extract to /opt

* edit desktop entry
```
sudo gedit /usr/share/applications/eclipse.desktop
[Desktop Entry]
Name=Eclipse Oxygen
Type=Application
Exec=/usr/local/bin/eclipse
Terminal=false
Icon=/home/fra/eclipse/latest/eclipse/icon.xpm
Comment=Integrated Development Environment
NoDisplay=false
Categories=Development;IDE;
Name[en]=Eclipse Oxygen
```

* install the desktop entry
```
sudo desktop-file-install /usr/share/applications/eclipse.desktop
```

* edit eclipse.ini and add the following lines
```
--launcher.GTK_version
2
```

###### Install statET
* Edit eclipse.ini by adding the following lines (under the section startup):
```
--launcher.GTK_version
2
```

* Help -> Install new software, enter site:
```
http://download.walware.de/eclipse-4.5
http://download.walware.de/eclipse-4.6
```

* Set up R run environment
* Preference -> StatET -> Run/Debug -> R environment
* Auto detect environment
```
The R home should be in : /usr/lib/R
```

* Set up Run configurations:
```
use Rterm not RJ!!
```

###### pyDev
* Help -> Install new software, enter:
```
http://pydev.org/updates
```

* setup pyDev run envrionment under Preference -> PyDev -> Interpreters -> Python interpreters

###### Eclipse for Lua
```
sudo apt-get install lua
```

update site:
```
http://download.eclipse.org/ldt/releases/milestones/
http://download.eclipse.org/ldt/releases/releases/stable
```

set execution environment, Preferences -> Lua -> Execution Environment

Add torch as default
* Lua Interpreters -> Add
* browse to the executable to luajit

### iTorch
```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install libzmq3-dev libssl-dev python-zmq
```

go to the folder to install iTorch
```
git clone https://github.com/facebook/iTorch.git
cd iTorch
luarocks make
```

check kernel list
```
ipython kernelspec list
```

### Visual Code
Download the deb file, and run install
```
sudo dpkg -i <file>.deb
sudo apt-get update
sudo apt-get install code
```

### Android
1. Download zip file from android website
2. Extract and copy to /opt/
3. Link it with
```
sudo ln -s /opt/android-studio/bin/studio.sh /usr/local/bin/
```
4. Install the pre-requisite package
```
sudo apt-get install libc6:i386 libncurses5:i386 libstdc++6:i386 lib32z1 libbz2-1.0:i386
```

### Intellij

###### Installation
1. Download and extract from tar zip
```
tar xvf <downloaded-file>
sudo mv idea-IC-171.4694.23/ /opt
```

2. create symbolic link
```
sudo ln -s /opt/idea-IC-171.4694.23/bin/idea.sh /usr/local/bin
```

3. ubuntu make
```
sudo add-apt-repository ppa:ubuntu-desktop/ubuntu-make
sudo apt-get update
sudo apt-get install ubuntu-make
umake ide idea
```

4. to uninstall
```
umake -r ide idea
```

5. alternatively
```
sudo apt-add-repository ppa:mmk2410/intellij-idea-community
sudo apt-get update
sudo apt-get install intellij-idea-community
```

6. to remove
```
sudo apt-get remove intellij-idea-community
sudo add-apt-repository --remove ppa:mmk2410/intellij-idea-community
```

###### Example: introcs algo
```
javac -cp "C:\Users\m038402\Documents\myWork\Codes\algs4-master\src\main\java" .\edu\princeton\cs\algs4\ThreeSum.java
```

###### Example: standford NLP Core
```
java -cp "*" -Xmx1g edu.stanford.nlp.pipeline.StanfordCoreNLP -annotators tokenize,ssplit,pos,lemma,ner,parse,dcoref -file input.txt

java -mx1g -cp "*" edu.stanford.nlp.pipeline.StanfordCoreNLPServer
http://localhost:9000/
```
###### Example: Think in Java
For additional libraries, e.g. javaassist and xom, place them under a lib folder (e.g. IdeaProjects/ThinkinJava/lib)

1. To import the libraries, put the lib folder in the Modeules->dependencies

2. 2. To get rid of java 1.5 warning, add to pom.xml

```
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.6.1</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                    <encoding>${project.build.sourceEncoding}</encoding>
                </configuration>
            </plugin>
        </plugins>
    </build>
```

3. In settings -> Build, Execution, Deployment -> Compiler -> Java Compiler

4. Make sure target bytecode version is 1.8


###### Intellij project setup
Project structure
```
Ctrl-ALt_Shift-S
```
Project:
* Check SDK : oracle
* Project level : default

SDK
* setup SDK to the desired java version

Modules
* setup project structure

Modules -> Dependencies
* add external libraries here

### Intellij scala / spark project setup

###### Create new scala project (sbt)

Project structure:
* files xxx.sc are scala worksheet files
* plugins.sbt
```
example: sbt-assembly
   addSbtPlugin("com.eed3si9n" % "sbt-assembly" % "0.14.6")
```
* build.sbt
```
Example: spark dependencies
name := "LearnSpark"
version := "0.1"
scalaVersion := "2.11.8"
```
```
libraryDependencies ++= Seq(
"org.apache.spark" % "spark-core_2.11" % "2.2.0",
"org.apache.spark" % "spark-sql_2.11" % "2.2.0"
)
```
To import dependencies:
* proejct structure -> Module -> Dependencies

* turn off run worksheet in the compiler process
```
@ Settings -> languages / Frameworks -> scala worksheet
```

* send command to scala console
```
Ctrl-Shift-X
```

### Cursive
* registration:
```
Help -> register Cursive
```

* create leinegen project
```
Settings -> keymap -> cursive -> Send form before caret to REPL
```

* set up REPL
```
run/debug configuration -> Clojure REPL
```

### Code:Blocks
* add the following lines in file:
/etc/apt/sources.list/code-blocks.list
```
deb [arch=amd64] https://apt.jenslody.de/stable stretch main
deb-src https://apt.jenslody.de/stable stretch main
```
* update
```
sudo apt-get update
sudo apt-get install jens-lody-debian-keyring
sudo apt-get install codeblocks
```

### Atom
Add Atom PPA
```
curl -sL https://packagecloud.io/AtomEditor/atom/gpgkey | sudo apt-key add -
sudo sh -c 'echo "deb [arch=amd64] https://packagecloud.io/AtomEditor/atom/any/ any main" > /etc/apt/sources.list.d/atom.list'
```
Install
```
sudo apt-get update
sudo apt-get install atom
```

