### Jupyter
```
pip install jupyter
pip3 install jupyter
```

* check jupyter kernel list:
```
jupyter kernelspec list
```

* to add additional kernel along with python3 (if missing)
```
python2 -m pip install ipykernel
python2 -m ipykernel install --user
```

* edit /.local/share/jupyter/kernels/python2/kernel.json if necessary

* Add R kernel for jupyter, run within R cmd line:
```
install.packages(c('repr', 'IRdisplay', 'crayon', 'pbdZMQ', 'devtools'))
devtools::install_github('IRkernel/IRkernel')
IRkernel::installspec(user=FALSE)  # for all users
IRkernel::installspec()  	   # for current user only
```

* prerequisites
```
sudo apt-get install libcurl4-openssl-dev
sudo apt-get install libssl-dev
```

* installation path
    * Installed kernelspec ir in:
    * /usr/local/share/jupyter/kernels/ir (for all users)
    * /home/fra/.local/share/jupyter/kernels/ir (current user only)
    * optional:
    * IRkernel::installspec(name = 'ir33', displayname = 'R 3.3')

### Jupyter server

Check for the config file in ~/.jupyter, create one if not exists
```
jupyter notebook --generate-config
```
Edit the config file to add:
```
c.NotebookApp.allow_origin = '*'
c.NotebookApp.ip = '0.0.0.0'
```
To set password
```
jupyter notebook password
```

access by hostname or ip, e.g
```
<hostname>.local:8888
```


### Apache Toree

* Installation
```
pip3 install <toree URL> --user
```

* toree URL (example):
```
https://dist.apache.org/repos/dist/dev/incubator/toree/0.2.0/snapshots/dev1/toree-pip/toree-0.2.0.dev1.tar.gz
```

* change write permission if jupyter is installed in global:
```
sudo chmod -R o+w /usr/local/share/jupyter
```

* user location:
```
~/.local/share/jupyter/kernels/
```

* install toree
```
jupyter toree install --spark_home=$SPARK_HOME --user
```

Start spark session
```
import org.apache.spark.sql.SparkSession
val spark = SparkSession.
        builder().
        getOrCreate()
import spark.implicits._
```

###### Running magic
To import JAR files:
```
%AddJar file:///usr/local/lib/java/postgresql-42.2.1.jar
%AddJar file:///usr/local/lib/java/mysql-connector-java-5.1.42-bin.jar
```

###### Dependencies
To import dependencies:
```
%AddDeps au.com.bytecode opencsv 2.4
import au.com.bytecode.opencsv.CSVReader

%AddDeps org.scalanlp breeze_2.11 0.13.2
%AddDeps org.scalanlp breeze-viz_2.11 0.13.2
%AddDeps org.scalanlp breeze-natives_2.11 0.13.2

```

### jupyter-scala

```
git clone https://github.com/jupyter-scala/jupyter-scala
```

edit & run scipt:
```
./jupyter-scala
```

###### Adding dependencies
```
import $ivy.`com.typesafe.slick::slick:3.2.1`
import $ivy.`org.vegas-viz::vegas:0.3.12`
```

```
import $ivy.`org.scalanlp::breeze-natives:0.13.2`
import $ivy.`org.scalanlp::breeze-viz:0.13.2`
import $ivy.`org.scalanlp::breeze:0.13.2`
import $ivy.`org.scalanlp::breeze:0.13.2`
```


### Jupyter Node JS
```
git clone https://github.com/notablemind/jupyter-nodejs.git
cd jupyter-nodejs
mkdir -p ~/.ipython/kernels/nodejs/
npm install && node install.js
npm run build
npm run build-ext
jupyter console --kernel nodejs
```

### iTypescript
* Install kernel locally
```
npm install -g itypescript
its --ts-install=local
```

### Jupyter + pyspark
* edit /.local/share/jupyter/kernels/python2/kernel.json

* add these to the file
```
 "env": {
     "PYSPARK_PYTHON": "python",
     "PYSPARK_DRIVER_PYTHON": "python",
     "SPARK_CONF_DIR": "/usr/lib/spark/conf"
 }
```

### iRuby
* Install dependencies
```
sudo apt install libtool libffi-dev ruby ruby-dev make
sudo apt install libzmq3-dev libczmq-dev
```
* Instal Ruby gem
```
sudo gem install cztop iruby
iruby regestier --force
```
* gem library location:
```
/var/lib/gems/2.3.0
```


### Haskell jupyter
```
sudo apt-get install -y python3-pip git libtinfo-dev libzmq3-dev libcairo2-dev libpango1.0-dev libmagic-dev libblas-dev liblapack-dev
```
To start
```
curl -sSL https://get.haskellstack.org/ | sh
git clone https://github.com/gibiansky/IHaskell
cd IHaskell
pip3 install -r requirements.txt --user
stack install gtk2hs-buildtools
stack install --fast
ihaskell install --stack
```

### Ruby jupyter
```
gem install cztop
gem install iruby
iruby register --force
```
* For windows, install Msys2, then install packages
```
pacman -Syu
pacman -Su
pacman -S --needed base-devel mingw-w64-i686-toolchain mingw-w64-x86_64-toolchain
pacman -S --needed git subversion mercurial mingw-w64-i686-cmake mingw-w64-x86_64-cmake
pacman -S --needed mingw-w64-x86_64-zeromq
```


### Clojure jupyter
```
git clone https://github.com/clojupyter/clojupyter
cd clojupyter
make
make install
```

### BeakerX
* Pip Install
```
pip install beakerx --user
```
* If local jupyter repository is used, need to create link to local:
```
sudo ln -s /home/fra/.local/share/jupyter/ /usr/share/jupyter
sudo ln -s /home/fra/.local/etc/jupyter/ /usr/etc/jupyter
sudo ln -s /home/fra/.local/etc/ipython/ /usr/etc/ipython
```
* run install:
```
beakerx install
```

### Pixel Dust
* python 2 only
```
pip install pixiedust
pip install pixiedust_node
jupyter pixiedust install
```

* Answer the following:

```
Step 1: PIXIEDUST_HOME: /home/fra/pixiedust
	Keep y/n [y]?
Step 2: SPARK_HOME: /usr/lib/spark
	Keep y/n [y]?
downloaded spark cloudant jar: /home/fra/pixiedust/bin/cloudant-spark-v2.0.0-185.jar
Step 3: SCALA_HOME: /usr/share/scala/
	Keep y/n [y]?
A different version of Scala (2, 12) is already installed in this directory.
Step 3: SCALA_HOME: /usr/share/scala/
	Keep y/n [y]? n
Step 3: Please enter a SCALA_HOME location: /home/fra/scala
Directory /home/fra/scala does not exist
	Create y/n [y]? y
SCALA_HOME will be set to /home/fra/scala/scala-2.11.8
Downloading Scala 2.11
Extracting Scala 2.11 to /home/fra/scala
Step 4: Kernel Name: Python with Pixiedust (Spark 2.2)
```

* Edit kernel.json file, e.g.
```
/home/fra/.local/share/jupyter/kernels/pythonwithpixiedustspark22
```
make sure python2 (/usr/bin/python) is used to run node

### IJavascript

* global: does not work: access denied
* local: does not work: jp-kernel not found
* need to copy ijsinstall, ijskernel to executable bin path
