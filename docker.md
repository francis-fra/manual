### Docker
* install
```
sudo apt-get remove docker docker-engine docker.io
```

* pre-requisite
```
sudo apt-get install apt-transport-https ca-certificates curl gnupg2 software-properties-common
```

* add official GPG key:
```
curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg | sudo apt-key add -
```

* set up the stable repository
```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") $(lsb_release -cs) stable"
```

* update repository
```
sudo apt-get update
sudo apt-get install docker-ce
```

* verfiy installation
```
docker version
docker -D info
docker run hello-world
```
### Docker Hub
* Build image, prepare a Dockerfile, and run:
```
docker build -t <image_name>
```
* Publish image, login first
```
docker login
```
then publish:
```
docker push <image_name>
```
* Download docker image
```
docker pull <image>
```

* to run
```
sudo docker run busybox echo "hello"
```

### Basic
* Start a container from image
```
docker run <image>
```
* Check docker status
```
service docker status
```
* Check Docker Server and Client Info
```
docker info
```

### Install docker-compose
```
sudo curl -L "https://github.com/docker/compose/releases/download/<version>/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```


### Docker images
* Check available local images
```
docker images
```
* Get image from docker hub
```
docker pull <image>
```
* Search image from docker hub
```
docker search <image>
```
### Containers
* Check running Cointainers
```
docker ps
```
* Show all running or stopped containes
```
docker ps -a
```
* show all stopped containers
```
docker ps -aq -f status=exited
```
* cleaning stopped containers
```
docker rm <id>
```
* one liner
```
docker rm $(docker ps -aq -f status=exited)
```
### attach running container
```
docker attach <id>
```
### Run a command in a running container
* same as docker attach, execute command, and then exit
```
docker exec [option] <id> <command>
```
e.g
```
docker exec -it 7ab /bin/bash

```


### Start / Stop containers
```
docker start <id>
docker stop <id>
```
* image info in json
```
docker inspect <id>
```
* Logs 
```
docker logs <id>
```
Get help
```
docker --help
docker run --help
```
### Running docker
* Run ubuntu
flag i: interactive
flag t: tty (shell)
```
docker run -it ubuntu bash
```
* Clean up containers
```
docker rm `docker ps -aq --no-trunc`
docker rm -v $(docker ps -aq -f status=exited)
docker ps -aq -f status=exited | xargs docker rm
```
* Get previously run container
```
docker ps -q -l
```
* Commit container and save as images
```
docker commit <id> <new_image>
```
* Run with commands
```
docker run <container> <command> <arg>
docker run test/cowsay-dockerfile /usr/games/cowsay "hello"
```

### Clean Up
* Remove image
```
docker rmi Image <image_name>
```
* To make sure dangling images are removed
```
docker images -f dangling=true
```
* Remove dangling images
```
docker images -qf dangling=true | xargs docker rmi
```
* Auto remove containers when exit
```
docker run --rm <id>
```
### Run in background
* flag -d
```
docker run --name myredis -d redis
```
* Launch a new container with cli and connect with the running redis
```
docker run --rm -it --link myredis:redis redis /bin/bash
redis-cli -h redis -p 6379
```
### Miscelleous
* Examine local volume name
* in /var/lib/docker/volumnes by default
```
docker volume ls
```
* show image layers
```
docker history <image>
```

### Container IP
find IP of container
```
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <container_name_or_id>
```
find the host gateway
```
docker inspect <container_name> -f '{{ .NetworkSettings.Gateway }}'
```

### Jupyter notebook
run jupyter noteobook and mount local drive to container
```
docker run --rm -v <absolute-local-path>:/home/jovyan -p 8888:8888 jupyter/all-spark-notebook 
```

### Confluence Kafka 
to start (may need to keep running until all states are up)
```
docker-compose up -d
```
check if all running
```
docker-compose ps
```
web interface
```
http://localhost:9021/clusters
```
Stop
```
docker-compose stop
```

### Airflow
Download
```
curl -LfO 'https://airflow.apache.org/docs/apache-airflow/2.1.1/docker-compose.yaml'
```
set up local environment
```
mkdir ./dags ./logs ./plugins
echo -e "AIRFLOW_UID=$(id -u)\nAIRFLOW_GID=0" > .env
```
initialize (set up database, user account)
```
docker-compose up airflow-init
```
run
```
docker-compose up
```
Download CLI script
```
curl -LfO 'https://airflow.apache.org/docs/apache-airflow/2.1.1/airflow.sh'
chmod +x airflow.sh
```

### jupyter all spark
To connect host postgres, add the following config:
```
from pyspark.conf import SparkConf

conf = SparkConf()  
conf.set("spark.jars", "/home/jovyan/work/jars/postgresql-42.2.23.jar")  # set the spark.jars
conf.set("spark.driver.extraClassPath", "/home/jovyan/work/jars/org.postgresql_postgresql-42.2.23.jar")
```
need to put the jar file in host and link the volume to the container, run docker with:
```
docker run -p 8888:8888 -v "${PWD}":/home/jovyan/work jupyter/all-spark-notebook 
```

### Tensor Flow
Installation
```
docker pull tensorflow/tensorflow:latest-py3-jupyter
docker pull tensorflow/tensorflow:1.15.2-py3-jupyter
```
Run interatively
```
docker run -it tensorflow/tensorflow:latest-py3-jupyter bash
```
Run with command line
```
docker run -it --rm tensorflow/tensorflow:latest-py3-jupyter python3 -c "import tensorflow as tf; print(tf.reduce_sum(tf.random.normal([1000, 1000])))"
```

### Start TensorFlow Jupyter 
```
docker run -d -u $(id -u):$(id -g) -p 8888:8888 -v $PWD:/tf tensorflow/tensorflow:latest-py3-jupyter 
p: port number
v: mount host folder to container folder
```

