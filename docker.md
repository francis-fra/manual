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

