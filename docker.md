### Docker
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
sudo docker version
sudo docker -D info
sudo docker run hello-world
```

* TODO: Download docker image
```
sudo docker pull <image>, e.g. sudo docker pull busybox
```

* to run
```
sudo docker run busybox echo "hello"
```

### Basic
Start a container from image
```
docker run <image>
```
Check docker status
```
service docker status
```
Check available images
```
docker images
```
Get image from docker hub
```
docker pull <image>
```
Search image from docker hub
```
docker search <image>

```
Check running image
```
docker ps
```
Show all running or stopped containes
```
docker ps -a
```
Run ubuntu
```
docker run -it ubuntu bash
```
Clean up containers
```
docker rm `docker ps -aq --no-trunc`
docker rm -v $(docker ps -aq -f status=exited)
docker ps -aq -f status=exited | xargs docker rm
```
Get previously run container
```
docker ps -q -l
```
Continue stopped container
```
docker start `docker ps -ql`
docker attach `docker ps -ql`
```
Information
```
docker info
```
Commit container and save as images
```
docker commit <id> <new_image>
```
Logs / inspect
```
docker logs <id>
docker inspect <id>
```
Version
```
docker version
```
Run with commands
```
docker run <container> <command> <arg>
docker run test/cowsay-dockerfile /usr/games/cowsay "hello"
```

Remove image
```
docker rmi Image <image_name>
```
To make sure dangling images are removed
```
docker images -f dangling=true
```

Build image, prepare a Dockerfile, and run:
```
docker build -t <image_name>
```

Publish image, login first
```
docker login
```
then publish:
```
docker push <image_name>
```

Remove dangling images
```
docker images -qf dangling=true | xargs docker rmi
```

Example:
Run in the background (-d)
```
docker run --name myredis -d redis
```
Launch a new container with cli and connect with the running redis
We rename myredis as redis when connected:
```
docker run --rm -it --link myredis:redis redis /bin/bash
redis-cli -h redis -p 6379
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

