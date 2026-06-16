# DOCKER 


## Installation

  Installing from script (newer version) 
```
  sudo wget -qO- https://get.docker.com/ | sh 
```

## Images

  Search for images
```
  docker search <name>
```
  Download a image
```
  docker pull <name>
```
  List docker images
```
  docker images
```
  Remove Image
```
  docker rmi <nameOrId>
```
  Inspecting a image
```
  docker image inspect <nameOrId>
```
  Show the history of a image
```
  docker history
```

## Containers

  Show containers
```
  docker ps       //show running containers
```
```
  docker ps -a    //show all containers
```
  Starting a container

    - i - Allow interactions with the container
    - t - Calls the tty
    - p 8080:80 - Binds the host's port 8080 to the port 80 of the container
    - <image_id> - Name or id of the desired image 
    - bin/bash - What will be executed on the container

```
  docker run -it --name <name> <-p 8080:80> <imageID> /bin/bash
```

  Inspect changes on the containers filesystem
```
  docker diff
```
  remove a container
```
  docker rm <nameOrId>
```

```
  docker run <nameOrId>
```
Parameters for docker run:
 - -d : run in background
 - -i : Iterative mode. Mantém o STDIN aberto mesmo sem console anexado
 - -t : Allocates a pseudo TTY (TeleTypewriter)
 - -rm : Removes the container after the exection
 - --name : Name the container
 - -v : Volume mapping
 - -p : Port mapping
 - -m : Memory usage limit

```
  docker start <nameOrId>
```

```
  docker stop <nameOrId>
```

```
  docker restart <nameOrId>
```

```
  docker kill <nameOrId>
```
An optional identifier used to specify a particular version or variant of the image. If no tag is provided, Docker defaults to latest
```
  docker tag <nameOrId> <imageLocal:TAG1.0>
```

```
  docker top 
```

```
  docker version
```

```
  docker wait
```


## Dockerhub

Login in terminal
```
  docker login
```
Saving changes in a image
```
  docker commit <containerID> <name/tag><imageName>

  ex: sudo docker commit 8dbd9e392a96 my_img:webserve
```
  Pull an image or a repository from the docker registry server
```
  docker pull
```
  Push an image or a repository to the docker registry server
```
  docker push <yourUser>/<imageName>
```

## Dockerfiles


## Docker-compose


## Docker Networks


## Docker Swarm



