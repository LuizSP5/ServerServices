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
  Remove a container
```
  docker rm <nameOrId>
```
  Create and run a new container from an image
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

  Start a stopped container
```
  docker start <nameOrId>
```
  Stop a running container
```
  docker stop <nameOrId>
```
  Restart a running container
```
  docker restart <nameOrId>
```
  Kill a running container
```
  docker kill <nameOrId>
```
  Gives an optional identifier used to specify a particular version or variant of the image. If no tag is provided, Docker defaults to latest
```
  docker tag <nameOrId> <imageLocal:TAG1.0>
```
  Lookup the running processes of a container
```
  docker top 
```
  Show the docker version information
```
  docker version
```
  Block until a container stops, then print its exit code
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

A Dockerfile allows to build custom enviroments automatically by using a file with the desired modifications, creating custom images and making the task of replicating it very easy. 

Example of Dockerfile content
```
FROM ubuntu:24.04
MAINTAINER Fulano da silva <fulano@redes.com>
RUN apt-get update && apt-get install apache2 -y
COPY script.sh /usr/local/script.sh
EXPOSE 8080
RUN bash "/usr/local/script.sh"
CMD bash
```

FROM - Indicates what image will be used as a base
RUN - Indicates what commands will be executed in the environments shell
COPY - Copy files located on the station that is running the creation of the image
CMD - Indicates what command will be executed in the start of a container
EXPOSE - Allows to expose the port of use by the service
WORKDIR - Defines the directory where the container will be started.

After building the Dockerfile, run this command:
```
sudo docker build -t meu_user/apache_server:latest .
```
-t - indicates the name of the image to be created
'.'- The . at the end of the command indicates that all the files located on the current directory are allowed for the Dockerfile manipulations.

After building, just run the container normally (ex:sudo docker run -it --name apache_my_server meulinux:apache_server /bin/bash)

## Docker-compose


## Docker Networks


## Docker Swarm



