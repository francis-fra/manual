### Basic
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
Get image
```
docker pull <image>
```
Search image
```
docker search <image>

```
Check running image
```
docker ps
```
Show all previously run images
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
Commit stopped images
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