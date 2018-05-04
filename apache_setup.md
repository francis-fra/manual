### Zookeeper
Download and extract binary into:
```
/usr/local
```

Create soft link
```
sudo ln -s zookeeper-xxx /usr/local/zookeeper
```

Create config file conf/zoo.cfg
```
tickTime=2000
dataDir=/var/zookeeper
clientPort=2181
```

Create data directory
```
mkdir /var/zookeeper
```

To change ownership
```
chown fra:hdgrp /var/zookeeper
```

To start
```
bin/zkServer.sh start
```

To check (are you ok)
```
telnet localhost 2181
ruok
```

To start CLI
```
bin/zkCli.sh
```

To stop server
```
bin/zkServer.sh stop
```

### Hive
Download and extract binary

copy to:
```
/usr/local/
```

create soft link
```
sudo ln -s /usr/local/hive-xxxx /usr/local/hive
sudo chown -R fra:hdgrp /usr/local/hive
```

edit .bashrc
```
export HIVE_HOME="/usr/local/hive" 
export PATH=$PATH:$HIVE_HOME/bin

export CLASSPATH=$CLASSPATH:/usr/local/hadoop/lib/*:.
export CLASSPATH=$CLASSPATH:/usr/local/hive/lib/*:.
```
For spark / hive connectivity
```
export CLASSPATH=$CLASSPATH:/usr/local/hive/conf/*:.
```

start Hadoop
```
sbin/start-dfs.sh
sbin/start-yarn.sh
```

Create Hive warehouse directory 
```
hadoop fs -mkdir /tmp
hadoop fs -mkdir /user/hive
hadoop fs -mkdir /user/hive/warehouse
hadoop fs -chmod g+w /tmp
hadoop fs -chmod g+w /user/hive/warehouse
```

###### hive-env.sh
edit hive-env.sh (configure Hive)
```
cd $HIVE_HOME/conf
```

copy environment file
```
sudo cp hive-env.sh.template hive-env.sh
```

add this line
```
export HADOOP_HOME=/usr/local/hadoop
export HADOOP_HEAPSIZE=512
```

Optional: multiple SLF4J exists 
```
rm lib/log4j-slf4j-impl-*.jar
```

Hive CLI (deprecated)
```
$HIVE_HOME/bin/hive
```

FIXME: HiveServer2 and Beeline

###### Install Derby
```
wget http://apache.mirror.digitalpacific.com.au//db/derby/db-derby-10.14.1.0/db-derby-10.14.1.0-bin.tar.gz
sudo tar xvzf db-derby-10.14.1.0-bin.tar.gz -C /usr/local
```
1. Create soft link
```
sudo ln -s /usr/local/db-derby-xxx /usr/local/derby
```

2. Edit .bashrc
```
export DERBY_HOME=/usr/local/derby
export PATH=$PATH:$DERBY_HOME/bin
export CLASSPATH=$CLASSPATH:$DERBY_HOME/lib/derby.jar:$DERBY_HOME/lib/derbytools.jar
```

3. Check derby status
```
java org.apache.derby.tools.sysinfo
```

Sample Output:
```
--------- Derby Information --------
[/usr/local/db-derby-10.14.1.0-bin/lib/derby.jar] 10.14.1.0 - (1808820)
[/usr/local/db-derby-10.14.1.0-bin/lib/derbytools.jar] 10.14.1.0 - (1808820)
[/usr/local/apache-hive-2.3.2-bin/lib/derbynet-10.11.1.1.jar] 10.11.1.1 - (1616546)
[/usr/local/apache-hive-2.3.2-bin/lib/derbyclient-10.11.1.1.jar] 10.11.1.1 - (1616546)
[/usr/local/apache-hive-2.3.2-bin/lib/derby-10.10.2.0.jar] 10.10.2.0 - (1582446)
```

4. create metastore data
```
mdir $DERBY_HOME/data
```

5. set default database as Derby
```
schematool -initSchema -dbType derby
```
Sample output:
```
SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/usr/local/apache-hive-2.3.2-bin/lib/log4j-slf4j-impl-2.6.2.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/usr/local/hadoop/share/hadoop/common/lib/slf4j-log4j12-1.7.10.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
SLF4J: Actual binding is of type [org.apache.logging.slf4j.Log4jLoggerFactory]
Metastore connection URL:	 jdbc:derby:;databaseName=metastore_db;create=true
Metastore Connection Driver :	 org.apache.derby.jdbc.EmbeddedDriver
Metastore connection User:	 APP
Starting metastore schema initialization to 2.3.0
Initialization script hive-schema-2.3.0.derby.sql
Initialization script completed
schemaTool completed
```

6. if failed, run the following and try running schematool again
```
mv metastore_db metastore_db.tmp
```

7. start up ij (interative SQL)
```
java org.apache.derby.tools.ij
```

###### hive-site.xml
Create local database location
```
mkdir /home/fra/bdw
```

Copy from template, location: $HIVE_HOME/conf
```
sudo cp hive-default.xml.template hive-site.xml
```

Edit config file: (hive-site.xml)
```
 <property>
    <name>javax.jdo.option.ConnectionURL</name>
    <value>jdbc:derby:;databaseName=/home/fra/bdw/metastore_db;create=true</value>
    <description>
      JDBC connect string for a JDBC metastore.
      To use SSL to encrypt/authenticate the connection, provide database-specific SSL flag in the connection URL.
      For example, jdbc:postgresql://myhost/db?ssl=true for postgres database.
    </description>
  </property>
  
  <property>
    <name>hive.downloaded.resources.dir</name>
    <!-- <value>${system:java.io.tmpdir}/${hive.session.id}_resources</value> -->
    <value>/tmp/${hive.session.id}_resources</value>
    <description>Temporary local directory for added resources in the remote file system.</description>
  </property>

  <property>
    <name>hive.exec.local.scratchdir</name>
    <!-- <value>${system:java.io.tmpdir}/${system:user.name}</value> -->
    <!-- <value>/tmp/${system:user.name}</value> -->
    <value>/tmp/fra</value>
    <description>Local scratch space for Hive jobs</description>
  </property>

```

Create a file named jpox.properties:

```
javax.jdo.PersistenceManagerFactoryClass =

org.jpox.PersistenceManagerFactoryImpl
org.jpox.autoCreateSchema = false
org.jpox.validateTables = false
org.jpox.validateColumns = false
org.jpox.validateConstraints = false
org.jpox.storeManagerType = rdbms
org.jpox.autoCreateSchema = true
org.jpox.autoStartMechanismMode = checked
org.jpox.transactionIsolation = read_committed
javax.jdo.option.DetachAllOnCommit = true
javax.jdo.option.NontransactionalRead = true
javax.jdo.option.ConnectionDriverName = org.apache.derby.jdbc.ClientDriver
javax.jdo.option.ConnectionURL = jdbc:derby://hadoop1:1527/metastore_db;create = true
javax.jdo.option.ConnectionUserName = APP
javax.jdo.option.ConnectionPassword = mine
```

###### FIXME: HiveServer
FIXME: to run HiveServer2
```
hiveserver2
or
hive --service hiveserver2
```
check
```
nestat -nl | grep 10000
```

start beeline
```
beeline
```

check if hiveserver2 has been started (nothing)
```
sudo service hive-server2 status

$ $HIVE_HOME/bin/hiveserver2
$ $HIVE_HOME/bin/beeline -u jdbc:hive2://$HS2_HOST:$HS2_PORT/usr/lib
```

FIXME: not responding??
```
$HIVE_HOME/bin/hiveserver2
$HIVE_HOME/bin/beeline -u jdbc:hive2://localhost:10000
```

HCatalog server (need to install HCatalog first)
```
$HIVE_HOME/hcatalog/sbin/hcat_server.sh start
$HIVE_HOME/hcatalog/sbin/hcat_server.sh stop
```

FIXME: error
```
$HIVE_HOME/hcatalog/bin/hcat
```

Some python database package
```
pip3 install pyhive --user
pip3 install psycopg2 --user
pip3 install mysqlclient --user
```

### Druid
Download and extract tar gzip file
```
curl -O http://static.druid.io/artifacts/releases/druid-0.11.0-bin.tar.gz
tar -xzf druid-0.11.0-bin.tar.gz
sudo mv druid-xxx /usr/local

sudo ln -s /usr/local/druid-xxx /usr/local/drid
sudo chown -R fra:hdgrp /usr/local/hive
```

Start up zookeper
```
/usr/local/zookeeper/bin/zkServer.sh start
```
Start up Druid services
```
bin/init
```

###### Testing: load batch data test
```
java `cat conf-quickstart/druid/historical/jvm.config | xargs` -cp "conf-quickstart/druid/_common:conf-quickstart/druid/historical:lib/*" io.druid.cli.Main server historical
java `cat conf-quickstart/druid/broker/jvm.config | xargs` -cp "conf-quickstart/druid/_common:conf-quickstart/druid/broker:lib/*" io.druid.cli.Main server broker
java `cat conf-quickstart/druid/coordinator/jvm.config | xargs` -cp "conf-quickstart/druid/_common:conf-quickstart/druid/coordinator:lib/*" io.druid.cli.Main server coordinator
java `cat conf-quickstart/druid/overlord/jvm.config | xargs` -cp "conf-quickstart/druid/_common:conf-quickstart/druid/overlord:lib/*" io.druid.cli.Main server overlord
java `cat conf-quickstart/druid/middleManager/jvm.config | xargs` -cp "conf-quickstart/druid/_common:conf-quickstart/druid/middleManager:lib/*" io.druid.cli.Main server middleManager
```
Submit a task
```
curl -X 'POST' -H 'Content-Type:application/json' -d @quickstart/wikiticker-index.json localhost:8090/druid/indexer/v1/task
```

###### Testing: load streaming data test
```
Download tranquility library
curl -O http://static.druid.io/tranquility/releases/tranquility-distribution-0.8.0.tgz
tar -xzf tranquility-distribution-0.8.0.tgz
cd tranquility-distribution-0.8.0
```

move to /usr/local
```
bin/tranquility server -configFile /usr/local/druid/conf-quickstart/tranquility/server.json

bin/generate-example-metrics | curl -XPOST -H'Content-Type: application/json' --data-binary @- http://localhost:8200/v1/post/metrics
```

Duid console
```
http://localhost:8090/console.html.
```

### Superset
prerequisite
```
sudo apt-get install build-essential libssl-dev libffi-dev python-dev python-pip libsasl2-dev libldap2-dev

pip3 install superset --user
```

create credential
```
fabmanager create-admin --app superset
```

initialize database
```
superset db upgrade
```

Load some data to play with
```
superset load_examples
```

Create default roles and permissions
```
superset init
```

Start the web server on port 8088, use -p to bind to another port
```
superset runserver -p 8099
```

add databases:
```
postgresql:
postgresql+psycopg2://username@/db

mysql:
mysql://username:password@localhost
```

postgresql config
```
/etc/postgresql/9.6/main//pg_hba.conf
```

###### Metabase
```
java -jar metabase.jar

```
Location
```
http://localhost:3000 
```


### FIXME: Ambari
Download and extract tarballs

compile the source
```
cd apache-ambari-2.6.0-src
mvn versions:set -DnewVersion=2.6.0.0.0

pushd ambari-metrics
mvn versions:set -DnewVersion=2.6.0.0.0
popd

mvn -B clean install package jdeb:jdeb -DnewVersion=2.6.0.0.0 -DskipTests -Dpython.ver="python >= 2.6"
```

To fix compile error: change version number from storm-1.1.0-SNAPSHOT to storm-1.1.0 in pom.xml

Add these to pom.xml if errors are found:
```
+      <plugin>
+        <groupId>org.vafer</groupId>
+        <artifactId>jdeb</artifactId>
+        <version>1.0.1</version>
+        <executions>
+          <execution>
+            <!--Stub execution on direct plugin call - workaround for ambari deb build process-->
+            <id>stub-execution</id>
+            <phase>none</phase>
+            <goals>
+              <goal>jdeb</goal>
+            </goals>
+          </execution>
+        </executions>
+        <configuration>
+          <skip>true</skip>
+          <attach>false</attach>
+          <submodules>false</submodules>
+          <controlDir>${project.basedir}/../src/main/package/deb/control</controlDir>
+        </configuration>
+      </plugin>
```

Install ambari server
```
cd ./ambari-server/target
sudo apt-get install ./ambari-server*.deb
```

Login as root
```
su
export buildNumber=2.6.0.0
ambari-server setup
ambari-server start
```

Install ambari agent
```
cd ./ambari-agent/target
sudo apt-get install ./ambari-agent*.deb
```

Edit /etc/ambari-agent/ambari.ini
```
[server]
hostname=localhost

ambari-agent start
```

web UI:
```
localhost:8080.
```

start ambari agent
```
ambari-agent start
```

Default login / password: admin

### HBase
1. Download and extract tarballs

```
sudo ln -s /usr/local/hbase-xxx /usr/local/hbase
sudo chown fra:hdgrp -R /usr/local/hbase
```

2. Edit .bashrc
```
export HBASE_HOME=/usr/local/hbase
export PATH=$PATH:$HBASE_HOME/bin
```

3. Edit /usr/local/hbase/conf/hbase-env.sh
```
export JAVA_HOME=/usr/java/latest
export HBASE_SSH_OPTS="-p 2882"
```

4. Edit hbase-site.xml
* the port 8088 must be matched with the hadoop hdfs port

```
<configuration>

     <property>
      <name>hbase.rootdir</name>
      <value>hdfs://localhost:9000/hbase</value>
     </property>

     <property>
       <name>hbase.cluster.distributed</name>
       <value>true</value>
     </property>

</configuration>
```

5. starting hbase
```
/usr/local/Hbase/bin/start-hbase.sh
```

6. stop hbase
```
bin/stop-hbase.sh
```

7. start hadoop and hbase
```
start-dfs.sh
start-yarn.sh
start-hbase.sh
```

Check directory
```
hdfs dfs -ls /hbase
```

Must start zookeeper first
```
zkServer.sh start
```

shell CLI
```
hbase shell
```

Default UI??
```
http://localhost:16010/
```


### Kafka
1. Download and extract tarzip

2. Create soft link
```
sudo ln -s kafka_2.12-0.11.0.1/ /usr/local/kafka
sudo chown -R fra:hdgrp kafka
```

3. Config kafka server
    * edit ~/kafka/config/server.properties:
    * uncomment the following:
```
delete.topic.enable=true
```

4. Start kafka server
```
kafka-server-start.sh ~/kafka/config/server.properties
nohup ~/kafka/bin/kafka-server-start.sh ~/kafka/config/server.properties
```
    * to check
```
netstat -nlpt
jps
```
    * to stop
```
../bin/kafka-server-stop.sh config/server.properties
```

5. Create topic
```
./bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test
```
    * check 
```
./bin/kafka-topics.sh --list --zookeeper localhost:2181
```
    * send some message
```
./bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test
(type some message)
```

    * start a consumer
```
./bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --from-beginning
```

    * to send
```
echo "Hello, World" | ~/kafka/bin/kafka-console-producer.sh --broker-list localhost:9092 --topic TutorialTopic > /dev/null
```
    * to receive
```
./bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic TutorialTopic --from-beginning
```

    * kafka python
```
sudo pip install kafka-python
```

### TODO: Cassandra
1. Install debian package

2. Add repository
```
echo "deb http://www.apache.org/dist/cassandra/debian 311x main" | sudo tee -a /etc/apt/sources.list.d/cassandra.sources.list
```
3. add repository key
```
curl https://www.apache.org/dist/cassandra/KEYS | sudo apt-key add -
```
4. update
```
sudo apt-get update
```
5. add public key is there is an error
```
sudo apt-key adv --keyserver pool.sks-keyservers.net --recv-key A278B781FE4B2BDA
```

6. install
```
sudo apt-get install cassandra
```

7. check cassandra
```
sudo service cassandra status
nodetool status
```

8. location:
```
/etc/cassandra
```

### TODO: Avro


### TODO: Phoenix

### Pig
1. Download and extract tar zip file

2. create soft link
```
sudo ln -s /usr/local/pig-xxxx /usr/local/pig
```

3. change ownership
```
sudo chown -R fra:hdgrp /usr/local/pig
```


4. edit .bashrc
```
export PIG_HOME=/usr/local/pig
export PATH=$PATH:/usr/local/pig/bin
export PIG_CLASSPATH=$HADOOP_HOME/etc/hadoop
```

5. run command
```
pig -version
```

6. local mode
```
pig -x local
pig
```


### Zeppelin
1. Download and extract binary into:

2. Create soft link
```
sudo ln -s zeppelin-0.7.3-bin-netinst/ /usr/local/zeppelin
```

3. Change ownership
```
sudo chown -R fra:hdgrp /usr/local/zeppelin
```

4. To start
```
sudo bin/zeppelin-daemon.sh start
```

5. Edit server port in conf/zeppelin-site.xml
    * default port is 8080, but it is same as spark
```
<property>
  <name>zeppelin.server.port</name>
  <value>9001</value>
  <description>Server port.</description>
</property>
```

    * link:
```
http://localhost:9001/
```

    * start
```
bin/zeppelin-daemon.sh start
```

    * stop 
```
bin/zeppelin-daemon.sh start
```

6. List all interpreters:
```
./bin/install-interpreter.sh --list
```

7. Install interpreters:
```
sudo ./bin/install-interpreter.sh --name shell,python
```

8. Edit conf/shiro.ini 

    * login/password
```
cp conf/shiro.ini.template shiro.ini
```

    * make sure this line is commented to prevent anonymous login
```
#/** = anon
```

    * login and passwords are listed in [users] section with default:
```
admin = password1, admin
user1 = password2, role1, role2
user2 = password3, role3
user3 = password4, role2
```

9. FIXME: jars conflict issue

    * if daemon start failed, check the ./log folder:
```
org.eclipse.jetty.util.resource.Resource.getAlias()Ljava/net/URL;
java.lang.NoSuchMethodError: org.eclipse.jetty.util.resource.Resource.getAlias()Ljava/net/URL;
```

    * to avoid jars conflict, reset the CLASSPATH in zeppelin, copy startup shell script:
```
cp zeppelin-daemon.sh zeppelin-dumb-dameon.sh
```

    * replace this line
```
CLASSPATH+=":${ZEPPELIN_CLASSPATH}"
with
CLASSPATH=":${ZEPPELIN_CLASSPATH}"
```

    * root out:
```
ZEPPELIN_CLASSPATH: ::/usr/local/zeppelin-0.7.3-bin-netinst/lib/interpreter/*:/usr/local/zeppelin-0.7.3-bin-netinst/lib/*:/usr/local/zeppelin-0.7.3-bin-netinst/*::/usr/local/zeppelin-0.7.3-bin-netinst/conf
```

    * fra '=' replace
```
ZEPPELIN_CLASSPATH: ::/usr/local/zeppelin/lib/interpreter/*:/usr/local/zeppelin/lib/*:/usr/local/zeppelin/*::/usr/local/zeppelin/conf
```

    * fra
```
ZEPPELIN_CLASSPATH: :./:/usr/local/lib/java:/home/fra/FraDir/learn/introcs/src/stdlib-package.jar:/home/fra/FraDir/learn/introcs/src/stdlib.jar:/home/fra/FraDir/learn/LearnJava/simsimplified/pj2.jar:/usr/local/hadoop/lib/*:/usr/local/hive/lib/*:/usr/local/hive/conf/*:/usr/local/derby/lib/*:/usr/local/zeppelin/lib/interpreter/*:/usr/local/zeppelin/lib/*:/usr/local/zeppelin/*::/usr/local/zeppelin/conf
```
    * fra re-arranged
```
ZEPPELIN_CLASSPATH: :/usr/local/zeppelin/lib/interpreter/*:/usr/local/zeppelin/lib/*:/usr/local/zeppelin/*::/usr/local/zeppelin/conf:./:/usr/local/lib/java:/home/fra/FraDir/learn/introcs/src/stdlib-package.jar:/home/fra/FraDir/learn/introcs/src/stdlib.jar:/home/fra/FraDir/learn/LearnJava/simsimplified/pj2.jar:/usr/local/hadoop/lib/*:/usr/local/hive/lib/*:/usr/local/hive/conf/*:/usr/local/derby/lib/*
```

###### optional: create new file /etc/init/zeppelin.conf
```
description "zeppelin"
start on (local-filesystems and net-device-up IFACE!=lo)
stop on shutdown
```

Respawn the process on unexpected termination
```
respawn
```

Respawn the job up to 7 times within a 5 second period.
If the job exceeds these values, it will be stopped and marked as failed.
```
respawn limit 7 5
```

zeppelin was installed in /usr/local/zeppelin in this example
```
chdir /usr/local/zeppelin
exec bin/zeppelin-daemon.sh upstart
```

### Storm
1. Download and extract tar ball

2. Create soft link
```
sudo ln -s /usr/local/apache-storm-xxxx /usr/local/storm
```

3. Create data directory
```
mkdir /var/storm
```

4. Change ownership
```
chown fra:hdgrp /var/storm
```

5. Edit conf/storm.yaml
```
storm.zookeeper.servers:
 - "localhost"
storm.local.dir: “/var/storm”
nimbus.host: "localhost"
supervisor.slots.ports:
 - 6700
 - 6701
 - 6702
 - 6703
```

6. start zookeeper
```
/usr/local/zookeeper/bin/zkServer.sh start
```

7. start nimbus
```
bin/storm nimbus
```

8. start supervisor
```
bin/storm supervisor
```

9. start UI
```
/bin/storm ui
http://localhost:8080
```




