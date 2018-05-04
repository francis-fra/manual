Preparation
=====
```
yum install git
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

###### Install scala
Download and extract scala tgz file
```
tar xvf scala-2.11.7.tgz
```
either rename or create a soft link
```
sudo mv scala-2.11.7 /usr/lib/
or
mv /usr/lib/scala-2.11.7 /usr/lib/scala
```
Change ownership
```
chown hduser:hdgrp /user/lib/scala
```
create soft link
```
sudo ln -s /usr/lib/scala-2.11.7 /usr/lib/scala
```

edit .bashrc
```
export SCALA_HOME=/usr/lib/scala/
export PATH=$SCALA_HOME/bin:$PATH
```

check
```
scala -version
```

###### install sbt (optional)
```
curl https://bintray.com/sbt/rpm/rpm > bintray-sbt-rpm.repo
sudo mv bintray-sbt-rpm.repo /etc/yum.repos.d/
sudo yum install sbt
```

Install Spark
=====
###### Method 1: download prebuilt spark
```
https://spark.apache.org/downloads.html
```

###### Method 2: command line download
```
wget http://d3kbcqa49mib13.cloudfront.net/spark-1.6.0-bin-hadoop2.6.tgz
```

To extract codes
```
tar xvf spark-1.6.0-bin-hadoop2.6.tgz
sudo mv spark-1.6.0-bin-hadoop2.6 /usr/lib/
```

To create a link to the latest spark
```
ln -s /usr/lib/spark-1.6.0-bin-hadoop2.6 /usr/lib/spark
```

To change the ownership of the folder and its element
```
sudo chown -R hduser:hdgrp /usr/lib/spark-1.6.0-bin-hadoop2.6
```

Optional: Spark R

To enable java to support R
```
sudo R CMD javareconf
```

The config file is stored at:
```
/usr/lib64/R/etc/Makeconf
```

Edit the config file if something is missing or wrong, examples:

```
  JAR = /usr/bin/jar
  JAVA = /usr/bin/java
  JAVAC = /usr/bin/javac
  JAVAH = /usr/java/latest/bin/javah
  ## JAVA_HOME might be used in the next three.  
  ## They are for packages 'JavaGD' and 'rJava'
  JAVA_HOME = /usr/java/latest
  JAVA_CPPFLAGS = -I$(JAVA_HOME)/include -I$(JAVA_HOME)/include/linux
  JAVA_LIBS = -L$(JAVA_HOME)/jre/lib/amd64/server -ljvm
  JAVA_LD_LIBRARY_PATH = $(JAVA_HOME)/jre/lib/amd64/server

```

At the command line (important)
```
unset JAVA_HOME
```
then start R and install package
```
install.packages("rJava")
install.packages(c("rmarkdown", "ggplot2", "pipeR", "whisker", "data.table", "reshape2"))
```

To start sparkR, where lib.loc is the path of spark
```
library(SparkR, lib.loc="/usr/lib/spark/R/lib")
```

###### Edit .bashrc
```
export SPARK_HOME=/usr/lib/spark
export PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin
```
optional:
```
export PATH=$PATH:$JAVA_HOME/bin  
export PATH=$PATH:$SBT_HOME/bin
export SBT_HOME=/usr/share/sbt-launcher-packaging/bin/sbt-launch.jar  
```

create log and pid directories
```
sudo mkdir /var/log/spark
sudo chown hduser:hdgrp /var/log/spark
sudo -u hduser mkdir $SPARK_HOME/run
```

optional:
```
export SPARK_EXAMPLES_JAR=/usr/local/spark-0.9.1-bin-hadoop2/examples/target/scala-2.10/spark-examples_2.10-assembly-0.9.1.jar
```

###### Edit spark-env.sh
```
cd /usr/lib/spark/conf/
cp spark-env.sh.template spark-env.sh
```

Edit $SPARK_HOME/conf/spark-env.sh
```
export SPARK_MASTER_IP=127.0.0.1 
export SPARK_WORKER_CORES=1 
export SPARK_WORKER_MEMORY=500mb 
export SPARK_WORKER_INSTANCES=2
export SPARK_LOG_DIR=/var/log/spark
export SPARK_PID_DIR=${SPARK_HOME}/run
```
if using python3 (default is python 2.7)
```
export PYSPARK_PYTHON=python3
```

###### conf/log4j.properties
To change the verbosity level
```
cp conf/log4j.properties.template conf/log4j.properties
```

change the line
```
log4j.rootCategory=INFO, console
to:
log4j.rootCategory=ERROR, console
```

Optional: Python executable
add to .bashrc:
```
export PYTHONPATH=$SPARK_HOME/python:$PYTHONPATH
```

Optional: edit spark-defaults.conf
Edit $SPARK_HOME/conf/spark-defaults.conf
```
spark.master            spark://master.localhost:7077
spark.serializer        org.apache.spark.serializer.KryoSerializer
```

Edit slaves config
```
sudo cp /usr/local/spark/conf/slaves.template /usr/local/spark/conf/slaves
```

###### Examples
Calculate Pi by running:
```
/usr/lib/spark/run-example org.spache.spark.examples.SparkPi
```

###### Spark daemon
Edit sbin/spark-daemon.sh
```
replace
ssh with ssh -p 2882
```

###### Edit sbin/load-spark-env.sh
```
export SPARK_SSH_OPTS="-p 2882"
```

###### start spark 
```
sbin/start-all.sh
sbin/stop-all.sh
```

###### Web UI
```
http://localhost:8080/
```

# Multi Node only
Edit /etc/hosts
```
# lists the slave nodes
127.0.0.0.1 localhost
192.168.1.10 spark.slave01.com
192.168.1.11 spark.slave02.com
```


Edit /usr/local/spark/conf/slaves
Append hostnames of all the salve nodes in $SPARK_HOME/conf/slaves file
e.g.
```
master.backtobazics.com
slave1.backtobazics.com
```

Do the same on for each slave machine

###### Starting spark
```
/opt/spark-latest/sbin/start-master.sh
```
You can monitor Spark using Web GUI
```
http://192.168.1.8:4040
#http://192.168.1.xx:8080
```

###### spark shell
```
scala> val textFile = sc.textFile("README.md")
scala> textFile.count()
```

###### Testing
```
cd $SPARK_HOME/bin
./run-example SparkPi 10
```

###### spark python
```
pyspark
```

Reference: Spark Cluster
```
http://spark.apache.org/docs/latest/spark-standalone.html
```

Master Node IP
```
http://spark.master.com:8080
```

Create home directory for spark user in HDFS??
```
sudo -u hdfs hadoop fs -mkdir -p /user/hduser
sudo -u hdfs hadoop fs -chown -R hduser:hdgrp /user/spark
```

Hive config??
```
sudo -u hive hadoop fs -mkdir /user/hive/warehouse
sudo -u hdfs hadoop fs -chmod -R 777 /user/hive/warehouse
```



