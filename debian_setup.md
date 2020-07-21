### Common Applications

###### Check installed packages:
```
dpkg --get-selections | grep -v deinstall | less
```

###### Add sudoer
login as root
```
visudo
```
then edit the /etc/sudoers file

###### Add debian repository
add this line to /etc/apt/sources.list
```
deb http://mirror.amaze.com.au/debian/ stable main contrib
```

###### find the fastest mirror
```
sudo apt-get instal netwelect-apt
sudo netselect-apt
```

###### Essential packages
needed for adding PPA
```
sudo apt-get install software-properties-common dirmngr
```

essentials packages:
```
sudo apt-get install build-essential python3-dev
sudo apt-get install devscripts
```

###### Git
```
sudo apt-get install git-all
```

configure git
```
git config --global user.name "fra"
git config --global user.email "fcnchan@yahoo.com"
```

config file location:
```
~/.gitconfig
```

check current config
```
git config --list
```
###### Startup Applications
* terminator
```
sudo apt-get install terminator
```

* customize via:

    * Preferences -> Layout
    * Auto start at login -> Run Startup Applications Apps
    * Add new command:
```
/usr/bin/terminator -m --layout=myLayout
config file:
~/.config/terminator/config
```

* emacs
```
sudo apt-get install emacs25
```

###### Install Dropbox
* Download deb file from dropbox

* install via
```
sudo dpkg -i <deb_file>
sudo ap-get install -f
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


### SSH server
```
sudo apt-get install openssh-server
sudo apt-get install openssh-client
```

* config file stored at
```
/etc/ssh/sshd_config
```

* edit port number different from 22, e.g.
```
Port xxxx
PasswordAuthenatication yes
```

* welcome message, edit
```
/etc/issue.net
```
* and then add this line to sshd_config file
```
Banner /etc/issue.net
```

* restart
```
sudo service ssh restart
sudo systemctl reload sshd (RH)
```

* check if sshd is active
```
netstat -plant
```

* to connect
```
e.g.
ssh -p <port_number> fra@192.168.0.1
```

### SSH client
###### Generate RSA keys
* LOCAL: SSH key generation
```
ssh-keygen -t rsa
```

* LOCAL: default public key stored in
```
~/.ssh/id_rsa.pub
```

* LOCAL: default private key
```
~/.ssh/id_rsa
```

* make the key pairs private
```
chmod 700 .ssh
chmod 600 .ssh/id_rsa*
```

###### Authentication
* send the public key from host A to B (machine intended to log into)

* copy via scp (if password authentication allowed)
```
scp -P <port_number> ~/.ssh/id_rsa.pub fra@192.1.168.1:/home/fra/Downloads
```

* at the backup
```
cp ~/.ssh/authorized_keys ~/.ssh/authorized_keys_copy
```
* append
```
cat ~/id_rsa.pub >> ~/.ssh/authorized_keys
```

### Rsync
* sync files locally
```
rsync -zvh <source_file> <target_directory>
e.g.
rsync -zvh backup.tar /tmp/backups
```

* sync directory locally
```
rsync -avzh <source_directory> <target_directory>
e.g.
rsync -avzh /home/fra/Documents /tmp/backups/Documents
```

* sync from local to remote
```
rsync -avz <local_source> <remote_target>
e.g.
rsync -avz /home/fra/Documents fra@192.168.1.10:/home/fra/
```

### SCP
add -r to copy recursively
```
scp -P <port_number> -r folder fra@192.1.168.1:/home/fra/Downloads
```

### VIM
```
sudo apt-get install vim
```

install plugin from:
```
https://github.com/amix/vimrc
```

### Heroku
run:
```
wget -qO- https://cli-assets.heroku.com/install-ubuntu.sh | sh
```

### Atom
Install Atom
```
sudo dpkg -i atom-amd64.deb
```
Install Atom's dependencies if they are missing
```
sudo apt-get -f install
```

### Virtual Box
1. add to /etc/apt/sources.list
```
deb https://download.virtualbox.org/virtualbox/debian stretch contrib
```

2. download public key from web page

3. add these keys with:
```
sudo apt-key add oracle_vbox_2016.asc
```

4. install:
```
sudo apt-get update
sudo apt-get install virtualbox-5.2
sudo apt-get install dkms
```

### Vagrant
```
sudo dpkg -i xxx.deb
sudo apt-get update
sudo apt-get install vagrant
```
### Emscripten
* Download from github
```
git clone https://github.com/juj/emsdk.git
```
* Copy the folder to:
```
sudo mv emsdk /opt
```
* Run
```
./emsdk install latest
./emsdk activate latest
```
* setup environment variables by:
'''
source ./emsdk_env.sh
'''
* To make it permanently modifying .bashrc:
'''
# EMSDK
export EMSDK=/opt/emsdk
export EM_CONFIG=/home/fra/.emscripten
export LLVM_ROOT=/opt/emsdk/clang/e1.38.10_64bit
export EMSCRIPTEN_NATIVE_OPTIMIZER=/opt/emsdk/clang/e1.38.10_64bit/optimizer
export BINARYEN_ROOT=/opt/emsdk/clang/e1.38.10_64bit/binaryen
export EMSDK_NODE=/opt/emsdk/node/8.9.1_64bit/bin/node
export EMSCRIPTEN=/opt/emsdk/emscripten/1.38.10

export PATH=$PATH:$EMSDK
export PATH=$PATH:$EMSDK/clang/e1.38.10_64bit
export PATH=$PATH:$EMSDK/node/8.9.1_64bit/bin
export PATH=$PATH:$EMSDK/emscripten/1.38.10
'''

### key applications
* FFMPEG
```
sudo apt-get install ffmpeg
```

* flash player
auto install:
```
sudo apt-get install flashplugin-installer
```
manual install:
Download and extract tar.gz file from Adobe

For firefox:
copy the extracted file to these locations:
```
sudo cp libflashplayer.so /usr/lib/mozilla/plugins/
sudo cp -r usr/* /usr
```

* VLC
```
sudo apt-get install vlc
```

* putty
```
sudo apt-get install putty
```

* splint
```
sudo apt-get install splint
```

### h2o (java)
* Download and extract tar ball
```
sudo mv h2o-3.xxx /usr/local/lib/java
sudo ln -s /usr/local/lib/java/h2o-3.xxx /usr/local/lib/java/h2o
```
* Run jar library
```
java -jar /usr/local/lib/java/h2o/h2o.jar
```

### h2o - python
* prerequisite
```
pip3 install requests
pip3 install tabulate
pip3 install scikit-learn
pip3 install colorama
pip3 install future
pip3 uninstall h2o
pip3 install h2o
```

* pip install
```
pip3 install http://h2o-release.s3.amazonaws.com/h2o/rel-weierstrass/3/Python/h2o-3.14.0.3-py2.py3-none-any.whl
```

### sparking water
Download and unzip file

* create soft link
```
sudo ln -s /usr/local/sparkling-xxxx /usr/local/sparkling-water
```

* change ownership
```
sudo chown -R fra:hdgrp /usr/local/sparkling-water
```

* run sparkling shell
```
cd sparkling-water-2.2.0
bin/sparkling-shell --conf "spark.executor.memory=1g"
```
* example:
```
import org.apache.spark.h2o._
val h2oContext = H2OContext.getOrCreate(spark)
import h2oContext._
```

* edit bashrc
```
export PATH=$PATH:/usr/local/sparkling-water/bin
```

### pysparking
for spark version 2.2:
```
pip install h2o_pysparkling_2.2 --user
```
Initialization
```
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName("SparklingWaterApp").getOrCreate()

from pysparkling import *
hc = H2OContext.getOrCreate(spark)
```

### Steam
* Download and extract steam tar balls
```
sudo mv steam-1.1.6-linux-amd64 /usr/local
```

* start jetty server
```
cd <steam_folder>
java -jar var/master/assets/jetty-runner.jar var/master/assets/ROOT.war
```

* run steam
```
./steam serve master --admin-name=admin --admin-password=admin
```

* web UI
```
localhost:9000
```



### PsuedoNode Hadoop
1. add new group
```
sudo addgroup hdgrp
```
2. add existing user to an existing group
```
sudo usermod -a -G hdgrp fra
```

to check
```
groups hduser
```

3. ssh setup
the public key is saved to its own authorized keys
```
cat $HOME/.ssh/id_rsa.pub >> $HOME/.ssh/authorized_keys
```

4. authomirzed_keys allow users of other machines to login
```
chmod 600 authorized_keys
```

5. check if ssh to own is ok
```
ssh -p <port number> localhost
ssh -p <port number> <hostname>
```

6. check hostname
```
hostname
```

7. Download from source
```
wget http://apache.claz.org/hadoop/common/stable/hadoop-xxx.tar.gz
tar -xzvf hadoop-xxx.tar.gz
sudo mv hadoop-xxx /usr/local/hadoop
```

8. Assign ownership of this folder to Hadoop user
```
sudo chown fra:hdgrp -R /usr/local/hadoop
```

###### Create Hadoop temp directories for Namenode and Datanode
```
sudo mkdir -p /usr/local/hadoop_tmp/hdfs/namenode
sudo mkdir -p /usr/local/hadoop_tmp/hdfs/datanode
```

Again assign ownership of this Hadoop temp folder to Hadoop user
```
sudo chown fra:hdgrp -R /usr/local/hadoop_tmp/
```

###### Edit hadoop-env.sh
Under /usr/local/hadoop/etc/hadoop, hard coded JAVA HOME
```
export JAVA_HOME=/usr/java/latest
```
change SSH port number
```
export HADOOP_SSH_OPTS="-p <port_num>"
```

###### config .bashrc
* Update $HOME/.bashrc

* Update hduser configuration file by appending the following environment variables at the end of this file.

* Update $HOME/.bash_profile or .bashrc
```
# -- HADOOP ENVIRONMENT VARIABLES START -- #
export JAVA_HOME=/usr/java/latest
export HADOOP_HOME=/usr/local/hadoop
export PATH=$PATH:$JAVA_HOME/bin
export PATH=$PATH:$HADOOP_HOME/bin
export PATH=$PATH:$HADOOP_HOME/sbin
export HADOOP_MAPRED_HOME=$HADOOP_HOME
export HADOOP_COMMON_HOME=$HADOOP_HOME
export HADOOP_HDFS_HOME=$HADOOP_HOME
export YARN_HOME=$HADOOP_HOME
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib"
# -- HADOOP ENVIRONMENT VARIABLES END -- #
```

###### edit /etc/hosts
* check the host name:
```
hostname
```
* make sure 127.0.0.1 contains the '$hostname' (and also localhost)

* to check the softlink
```
readlink -f /usr/bin/javac
which javac
```

### Edit XML files
Under /usr/local/hadoop/etc/hadoop

###### config XMLs : core-site.xml
* /usr/local/hadoop/etc/hadoop/core-site.xml

* Paste these lines into <configuration> tag
```
<property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
</property>
```

###### config XMLs : hdfs-site.xml

* To edit file
```
/usr/local/hadoop/etc/hadoop/hdfs-site.xml
```

* Paste these lines into <configuration> tag
```
 <property>
      <name>dfs.replication</name>
      <value>1</value>
 </property>

 <property>
      <name>dfs.namenode.name.dir</name>
      <value>file:/usr/local/hadoop_tmp/hdfs/namenode</value>
 </property>

 <property>
      <name>dfs.datanode.data.dir</name>
      <value>file:/usr/local/hadoop_tmp/hdfs/datanode</value>
 </property>
```

###### config XMLs : yarn-site.xml
* To edit file
```
/usr/local/hadoop/etc/hadoop/yarn-site.xml
```

* Paste these lines into <configuration> tag
```
  <property>
      <name>yarn.nodemanager.aux-services</name>
      <value>mapreduce_shuffle</value>
  </property>
  <property>
      <name>yarn.nodemanager.aux-services.mapreduce.shuffle.class</name>
      <value>org.apache.hadoop.mapred.ShuffleHandler</value>
  </property>
```

* important: default = -1 (hadoop 2.7.4)
```
  <property>
	<name>yarn.nodemanager.resource.memory-mb</name>
	<value>8192</value>
  </property>
  <property>
	<name>yarn.nodemanager.resource.cpu-vcores</name>
    	<value>8</value>
  </property>
```
* optional
```
  <property>
	<name>yarn.scheduler.minimum-allocation-mb</name>
   	<value>2048</value>
  </property>
  <property>
	<name>yarn.nodemanager.vmem-pmem-ratio</name>
	<value>2.1</value>
  </property>
```

###### config XMLs : mapred-site.xml
* Make a copy of the template mapred-site.xml.template
```
cp /usr/local/hadoop/etc/hadoop/mapred-site.xml.template  /usr/local/hadoop/etc/hadoop/mapred-site.xml
```

* Paste these lines into <configuration> tag
```
<property>
      <name>mapreduce.framework.name</name>
      <value>yarn</value>
</property>
```

* optional
```
<property>
	<name>mapreduce.job.tracker</name>
	<value>HadoopMaster:5431</value>
</property>
<property>
    <name>mapreduce.jobhistory.webapp.address</name>
    <value>http://localhost:19888</value>
</property>
```

###### Format Name Node
* Do it only once
```
hdfs namenode -format
```

* check hadoop version
```
hadoop version
```

###### Start daemons
* start daemons (/usr/local/hadoop)
```
start-dfs.sh
start-yarn.sh
```

* check
```
jps
```

* examples:
```
12162 Jps
11798 NodeManager
11464 SecondaryNameNode
11196 DataNode
11037 NameNode
11663 ResourceManager
```

* web UI
```
http://localhost:8088/cluster
```

* make sure the ClusterID are the same, check the datanode and namenode VERSION file in:
```
cat /usr/local/hadoop_tmp/hdfs/datanode/current/VERSION
cat /usr/local/hadoop_tmp/hdfs/namenode/current/VERSION
```

###### Create user folder
* create directory at hdfs
```
hdfs dfs -mkdir /user
hdfs dfs -mkdir /user/<username>
```

###### Testing
```
hdfs dfs -mkdir /user/fra/input
```

* transfer some files for testing
```
hdfs dfs -put /usr/local/hadoop/etc/hadoop input
```

* copy files to hdfs
```
hdfs dfs -put <src_file> <destination>
```

* example
```
hadoop jar /usr/local/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.4.jar grep input/hadoop output 'dfs[a-z.]+'
```

* check the contents in data node
```
hdfs dfs -ls /user/hduser/input/hadoop
```
* this will be created by the mapreduce task
```
hdfs dfs -ls /user/hduser/output
```

###### Web UI
* Name node
```
http://localhost:50070/
```

* resource manager
```
http://localhost:8088
```

### Spark
* download prebuilt spark
```
https://spark.apache.org/downloads.html
```

* extract codes
```
tar xvf spark-1.6.0-bin-hadoop2.6.tgz
sudo mv spark-1.6.0-bin-hadoop2.6 /usr/lib/
```

* create a link to the latest spark
```
sudo ln -s /usr/lib/spark-1.6.0-bin-hadoop2.6 /usr/lib/spark
```

* change the ownership of the folder and its element
```
sudo chown -R fra:hdgrp /usr/lib/spark-1.6.0-bin-hadoop2.6
```

* edit .bashrc
```
export SPARK_HOME=/usr/lib/spark
export PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin
#export PYTHONPATH=$SPARK_HOME/python:$PYTHONPATH
export PYTHONPATH=$SPARK_HOME/python/lib/pyspark.zip:$SPARK_HOME/python/lib/py4j-0.10.4-src.zip:$PYTHONPATH
# same as spark-env.sh
export PYSPARK_PYTHON=python3
export PYSPARK_DRIVER_PYTHON=python3
```

* create log and pid directories
```
sudo mkdir /var/log/spark
sudo chown fra:hdgrp /var/log/spark
sudo -u fra mkdir $SPARK_HOME/run
```

* eclipse preferences
```
under python environment:
SPARK_HOME=/usr/lib/spark
PYSPARK_SUBMIT_ARGS=--master local[*] --queue PyDevSpark pyspark-shell
SPARK_CONF_DIR=/usr/lib/spark/conf
PYSPARK_PYTHON=python3
```

###### spark-env.sh
```
cd /usr/lib/spark/conf/
cp spark-env.sh.template spark-env.sh
```

* edit $SPARK_HOME/conf/spark-env.sh
```
export SPARK_MASTER_IP=127.0.0.1
export SPARK_WORKER_CORES=2
export SPARK_WORKER_MEMORY=2g
export SPARK_WORKER_INSTANCES=2
export SPARK_LOG_DIR=/var/log/spark
export SPARK_PID_DIR=${SPARK_HOME}/run
```
* if using python3 (default is python 2.7)
```
export PYSPARK_PYTHON=python3
export PYSPARK_DRIVER_PYTHON=python3
```

###### conf/log4j.properties
* to change the verbosity level
```
cp conf/log4j.properties.template conf/log4j.properties
```

* change the line
```
log4j.rootCategory=INFO, console
to
log4j.rootCategory=ERROR, console
```

###### Starting spark
* this must be started before runing spark-shell
```
/opt/spark-latest/sbin/start-master.sh
```

* You can monitor Spark using Web GUI
```
localhost:4040/jobs
localhost:8080
```

###### Spark daemon
* edit sbin/spark-daemon.sh
```
replace ssh with ssh -p 2882
```

* optinal: edit sbin/load-spark-env.sh
```
export SPARK_SSH_OPTS="-p 2882"
```

* start spark master
```
sbin/start-all.sh
```

* start slave
```
sbin/start-slave.sh spark://localhost:7077
```

* stop master
```
sbin/stop-master.sh
sbin/stop-slave.sh
```

* start all
```
sbin/start-all.sh
```

* stop all
```
sbin/stop-all.sh
```

* web UI
```
http://localhost:8080/
```

### h2o
* prerequisite
```
pip install requests
pip install tabulate
pip install scikit-learn
pip install colorama
pip install future
pip uninstall h2o
```

* pip install
```
pip3 install https://h2o-release.s3.amazonaws.com/h2o/rel-weierstrass/4/Python/h2o-3.14.0.4-py2.py3-none-any.whl --user
```

### sparking water
* Download and unzip file

* create soft link
```
sudo ln -s /usr/local/sparkling-xxxx /usr/local/sparkling-water
```

* change ownership
```
sudo chown -R fra:hdgrp /usr/local/sparkling-water
```

* run sparkling shell (spark daemon must be started)
```
bin/sparkling-shell --conf "spark.executor.memory=1g"
```

* example:
```
import org.apache.spark.h2o._
val h2oContext = H2OContext.getOrCreate(spark)
import h2oContext._
```

* edit bashrc
```
export PATH=$PATH:/usr/local/sparkling-water/bin
```

### pysparking
* for spark version 2.2:
```
pip install h2o_pysparkling_2.2
```
Start the session:
```
from pyspark.sql import SparkSession
from pysparkling import *
hc = H2OContext.getOrCreate(spark)
```

### Zookeeper
* download and extract binary into:
```
/usr/lib
```

* create soft link
```
sudo ln -s zookeeper-xxx /usr/lib/zookeeper
```

* create config file conf/zoo.cfg
```
tickTime=2000
dataDir=/var/zookeeper
clientPort=2181
```

* create data directory
```
mkdir /var/zookeeper
```

* change ownership
```
chown fra:hdgrp /var/zookeeper
```

* to start
```
bin/zkServer.sh start
```

* to check (are you ok)
```
telnet localhost 2181
ruok
```

### Deep learning
* theano
```
sudo apt-get install python-dev python3-nose g++ libopenblas-dev git
pip3 install nose2 nose-parameterized --user
pip3 install Theano --user
```

* tensor flow (gpu only)
```
sudo apt-get install libcupti-dev
```

* need pip version 8.1 or later
```
pip3 install tensorflow
```
To test
```
$ import tensorflow as tf
$ sess = tf.InteractiveSession()
$ sess.close()
$ a = tf.constant(10)
$ b = tf.constant(32)
$ print(sess.run(a + b))
```

* Keras
```
pip3 install keras --user
```

* CNTK
pre-requisite
```
sudo apt-get install openmpi-bin
```

* install
```
pip3 install https://cntk.ai/PythonWheel/CPU-Only/cntk-2.2-cp35-cp35m-linux_x86_64.whl --user
```

### Text Mining
```
sudo apt-get install opencc
pip3 install jieba --user
```

* Code location:
```
/home/fra/FraDir/learn/Learnpy/Mypy/text_mining/text_training
```

###### train chinese wiki:

1. extract text fro bzip file
```
python3 process_wiki.py <bz2 file> wiki.zh.text
```

2. convert traditional to simplified chinese
```
opencc -i wiki.zh.text -o wiki_cn_text.txt -c t2s.json
```

3. remove ascii (english) text
```
python3 clean_assii.py < wiki_cn_text.txt > wiki_cn_clean.txt
```

4. segment sentences
```
python -m jieba wiki_cn_clean.txt > wiki_cn_clean_seg.txt -d ' '
```

5. train word2vec model
```
python train_word2vec_model.py wiki_cn_clean_seg.txt wiki_cn.model wiki_cn_text.vector
```

###### train japanese wiki:

1. mecab for japanese segment
```
sudo apt-get install mecab libmecab-dev mecab-ipadic
sudo apt-get install mecab-ipadic-utf8
pip3 install mecab-python3 --user
```

2. extract text from bzip file
```
python process_wiki.py jawiki-latest-pages-articles.xml.bz2 wiki.ja.text
```

3. remove ascii text??
```
python3 clean_ascii.py < wiki_ja_text.txt > wiki_ja_clean.txt
```

4. segment text
```
mecab -O wakati wiki_ja_clean.txt -o wiki_ja_seg.txt -b 10000000
```

5. train word2vec model
need: intput:- segment words output:- model output and vector output
```
python3 train_word2vec.py wiki_ja_seg.txt wiki_ja_text.model wiki_ja_text.vector
```

#### Chinese Input
Install Chinese language and input methods
```
sudo apt install ibus
apt install ibus-table-chinese
sudo apt install ibus-table-chinese
sudo apt install ibus-table-cangjie5
sudo apt install ibus-cangjie
ibus-setup
```
