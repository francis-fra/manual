Hadoop single node setup
======
```
sudo apt-get install rsync (ubuntu)
```

1. install java 8
```
java -version
```
2. check java home
```
readlink -f /usr/bin/java
```

3. install nmap (optional)
```
sudo yum install nmap
```

Install java on CentOS
======

1. Remove open java
```
yum remove java-1.7.0-openjdk
```

2. Download oracle jdk8
```
sudo rpm -Uvh jdk-8uxxx-linux-x64.rpm
```
or
```
sudo yum localinstall jdk-8uxxx-linux-x64.rpm
```
```
sudo alternatives --install /usr/bin/java java /usr/java/latest/bin/java
```
3. Config soft link to the default java
```
sudo alternatives --config java
```
```
sudo alternatives --install /usr/bin/javac javac /usr/java/latest/bin/javac
```

4. Config soft link to the default javac
```
sudo alternatives --config javac
```

5. Create Hadoop user group
```
sudo addgroup hdgrp
sudo groupadd hdgrp
```

6. Create new user
```
sudo adduser --ingroup hdgrp hduser
sudo adduser -g hdgrp hduser
passwd hduser
```

7. To check
```
groups hduser
```

Setup ssh
======
See also linux_admin manual

1. Install ssh
```
sudo apt-get install openssh-server
```

2. edit /etc/sshd_config, change the following fields:
```
PORT
PasswordAuthentication
```

3. Restart the daemon
```
sudo service ssh restart
```

4. First login with hduser
```
sudo su hduser
```

5. Generate ssh key for hduser account
```
ssh-keygen -t rsa
```

6. Test ssh to the same machine, and then append its id_rsa.pub to the authorized keys of hduser
The public key is saved to its own authorized keys:
```
cat $HOME/.ssh/id_rsa.pub >> $HOME/.ssh/authorized_keys
```

7. authomirzed_keys allow users of other machines to login
```
chmod 600 authorized_keys
```

To login to other machine, distribute the public key and store in those machines

###### optional
Disable ipv6 and update the file /etc/sysctl.conf by adding:
```
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1
```

to check...
```
ssh localhost
```

# check if hduser is in sudo group
```
sudo -v
```

# add hduser to become a sudoer
```
visudo
```

Download Hadoop
======

1. Download from source
```
wget http://apache.claz.org/hadoop/common/stable/hadoop-2.7.3.tar.gz
```

2. Extract Hadoop
```
sudo tar -xzvf hadoop-2.7.3.tar.gz
sudo mkdir -p /usr/local/hadoop
sudo mv hadoop-2.7.3 /usr/local/hadoop
```

3. Assign ownership of this folder to Hadoop user
```
sudo chown hduser:hdgrp -R /usr/local/hadoop
```

Config .bashrc
======
###### Update $HOME/.bashrc

1. Create linked directory: /usr/java/latest

Update hduser configuration file by appending the following environment variables at the end of this file.

2. Update $HOME/.bash_profile or .bashrc:
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

3. check the softlink
```
readlink -f /usr/bin/javac
which javac
```

4. update the settings
```
source .bashrc
```

5. Create Hadoop temp directories for Namenode and Datanode
```
sudo mkdir -p /usr/local/hadoop_tmp/hdfs/namenode
sudo mkdir -p /usr/local/hadoop_tmp/hdfs/datanode
```

6. Again assign ownership of this Hadoop temp folder to Hadoop user
```
sudo chown hduser:hdgrp -R /usr/local/hadoop_tmp/
```

Edit Hadoop-env.sh
======

1. Change SSH port number under
```
/usr/local/hadoop/etc/hadoop/
```
```
export HADOOP_SSH_OPTS="-p <port_num>"
```

2. In case there is an error message saying that JAVA_HOME is not found, need to hard-coded as:
```
Change
export JAVA_HOME=${JAVA_HOME}
to
export JAVA_HOME=/usr/java/latest
```

Pseudo Distribution Mode
======

1. Check the host name, and edit /etc/hosts
```
hostname
```

2. Make sure 127.0.0.1 contains the 'hostname' (and also localhost)

###### Edit XML files under
```
/usr/local/hadoop/etc/hadoop
```

Config XMLs : core-site.xml
======

Create Hadoop tmp directories (to be added in core-site.xml)
```
sudo mkdir -p /app/hadoop/tmp
sudo chown hduser:hdgrp /app/hadoop/tmp
```

optional:
```
<property>
  <name>hadoop.tmp.dir</name>
  <value>/app/hadoop/tmp</value>
  <description>A base for other temporary directories.</description>
</property>
```

Edit core-site.xml file
```
/usr/local/hadoop/etc/hadoop/core-site.xml
```
Paste these lines into <configuration> tag
```
<property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
</property>
```

Config XMLs : hdfs-site.xml
======

To edit file
```
/usr/local/hadoop/etc/hadoop/hdfs-site.xml
```

Paste these lines into <configuration> tag
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

Config XMLs : yarn-site.xml
======

To edit file
```
/usr/local/hadoop/etc/hadoop/yarn-site.xml
```

Paste these lines into <configuration> tag:
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

Optinal:
```
<property>
      <name>yarn.resourcemanager.hostname</name>
      <value>localhost</value>
</property>
```

Config XMLs : mapred-site.xml
======

Make a copy of the template mapred-site.xml.template
```
cp /usr/local/hadoop/etc/hadoop/mapred-site.xml.template  /usr/local/hadoop/etc/hadoop/mapred-site.xml
```
Edit file
```
/usr/local/hadoop/etc/hadoop/mapred-site.xml
```
Paste these lines into <configuration> tag
```
<property>
      <name>mapreduce.framework.name</name>
      <value>yarn</value>
</property>

<property>
  <name>mapred.job.tracker</name>
  <value>localhost:54311</value>
  <description>The host and port that the MapReduce job tracker runs
  at.  If "local", then jobs are run in-process as a single map
  and reduce task.
  </description>
</property>
```

###### Format Name Node
do it only once:
```
hdfs namenode -format
```

Start daemons
======

Start daemons (/usr/local/hadoop)
```
start-dfs.sh
start-yarn.sh
```
optional:
```
mr-jobhistory-daemon.sh start historyserver
```

To verify:
```
jps

Sample output:
12162 Jps
11798 NodeManager
11464 SecondaryNameNode
11196 DataNode
11037 NameNode
11663 ResourceManager
```

Troubleshoot
======
Find out config value:
```
hdfs getconf -confKey fs.defaultFS
e.g.
hdfs://localhost:9000
```

```
netstat -plten | grep java
```
To check if port is opened
```
nmap -p <port_num> localhost
nmap localhost
hadoop dfsadmin -report
```

Testing
```
hadoop version
```

Make sure the ClusterID are the same, check the datanode and namenode VERSION file in:
```
/usr/local/hadoop_tmp/hdfs/datanode/current
/usr/local/hadoop_tmp/hdfs/namenode/current
```

Delete all the contents of datanode if the clusterID are different

Create directory at hdfs
```
hdfs dfs -mkdir /user
hdfs dfs -mkdir /user/<username>
```

Testing
======
Make testing directory:
```
hdfs dfs -mkdir /user/hduser/input
hdfs dfs -mkdir /user/hduser/output
```

Transfer some files for testing
```
hdfs dfs -put /usr/local/hadoop/etc/hadoop input
```

Copy files to hdfs
```
hdfs dfs -put <src_file> <destination>
```

Examples
```
hadoop jar /usr/local/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.3.jar grep input/hadoop output 'dfs[a-z.]+'
```

Check the contents in data node
```
hdfs dfs -ls /user/hduser/input/hadoop
hdfs dfs -ls /user/hduser/output
```

To transfer results to local system
```
hdfs dfs -get output ~/Downloads/output
cat output/*
```

Basic Commands
======
Check the hdfs file structure
```
hdfs dfs -ls \
```
Copy files from local -> hdfs
```
hadoop fs -copyFromLocal <fileName>
```
same as
```
hdfs dfs -copyFromLocal <fileName>
```
Copy files from hdfs -> local
```
hdfs dfs -copyToLocal <fileName>
```

Web UI address
======
###### Name node
http://localhost:50070/

###### Resource manager
http://localhost:8088

###### Node Manager
http://localhost:8042/


###### Default port
NameNode - http://centos-vm:50070/

DataNode - http://centos-vm:50075/

JobTracker - http://centos-vm:50030/

###### Stop Hadoop
```
mr-jobhistory-daemon.sh stop historyserver
stop-yarn.sh
stop-dfs.sh
```

### Hadoop / Map Reduce
Edit bashrc:
```
export HADOOP_CLASSPATH=$JAVA_HOME/lib/tools.jar
```

To compile map reduce files
```
hadoop com.sun.tools.javac.Main <java_src_files>
```

Create jar file
```
jar cf <output.jar> <compiled.class>
```

Start hadoop
```
start-dfs.sh
start-yarn.sh
```

Start spark daemon
```
$SPARK_HOME/sbin/start-all.sh
```

###### Example: running wordcount on hadoop

To compile
```
hadoop com.sun.tools.javac.Main WordCount.java WordMapper.java SumReducer.java
```
To pack into jar file
```
jar cf wc.jar *.class
```
To copy source file to hdfs
```
hdfs dfs -copyFromLocal shakespeare.txt /user/fra/shakespeare.txt
```
To submit map reduce job
```
hadoop jar wc.jar WordCount shakespeare.txt wordcounts
```

###### Example: Run map reduce using python:
```
hadoop jar $HADOOP_HOME/share/hadoop/tools/lib/hadoop-streaming-*.jar \
  -input /user/fra/flights.csv \
  -output average_delay \
  -mapper mapper.py \
  -reducer reducer.py \
  -file mapper.py \
  -file reducer.py
```
