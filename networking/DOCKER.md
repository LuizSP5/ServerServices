# Docker

## Installation

- Installing from script (newer version)
```
  sudo wget -qO- https://get.docker.com/ | sh
```

or  

- Installing from repositories
```
  sudo apt-get install docker.io
```

- Test Installation
```
  sudo docker run hello-world
```

## Commands

#### Services
```
  sudo service docker start
  sudo service docker status
  sudo service docker stop
```
#### Enter inside a container
Enter and dont stop the execution of container
```
  docker exec -it <containerName> bash
```
Enter and stop the execution
```
docker attach <containerName>
```

#### Docker images  
Search for a Image
```
  docker search <name>
```
Download a image
```
  docker pull <name>
```
Listing Images
```
  sudo docker images
```
Inspecting a image
```
  sudo docker image inspect <name>
```

#### Show running containers
```
  docker ps
  docker ps -a  //show all containers
```

#### Start a new container
- i - Allow interactions with the container
- t - Calls the tty
- p 8080:80 - Binds the host's port 8080 to the port 80 of the container
- <image_id> - Name or id of the desired image 
- bin/bash - What will be executed on the container
  
```
docker run -it --name <name> <-p 8080:80> <image_id> /bin/bash
```

```
attach Attach to a running container
build Build a container from a Dockerfile
commit Create a new image from a container's changes
cp Copy files/folders from the containers filesystem to the host path
diff Inspect changes on a container's filesystem
events Get real time events from the server
export Stream the contents of a container as a tar archive
history Show the history of an image
images List images
import Create a new filesystem image from the contents of a tarball
info Display system-wide information
insert Insert a file in an image
inspect Return low-level information on a container
kill Kill a running container
load Load an image from a tar archive
login Register or Login to the docker registry server
logs Fetch the logs of a container
port Lookup the public-facing port which is NAT-ed to PRIVATE_PORT

pull Pull an image or a repository from the docker registry server
push Push an image or a repository to the docker registry server
restart Restart a running container
rm Remove one or more containers
rmi Remove one or more images
run Run a command in a new container
save Save an image to a tar archive

start Start a stopped container
stop Stop a running container
tag Tag an image into a repository
top Lookup the running processes of a container
version Show the docker version information
wait Block until a container stops, then print its exit code  
```
run Run a command in a new container
Parameters for command **#run**
```
  -d run in background
  -i Iterative mode. Mantém o STDIN aberto mesmo sem console anexado
  -t Aloca uma pseudo TTY (TeleTypewriter)
  -rm Removes the container after the exection
  --name Name the container
  -v Volume mapping
  -p Port mapping
  -m Memory usage limit
```
## Docker Hub
Login in terminal
```
sudo docker login
```
Saving changes in a image
```
sudo docker commit <Container ID> <Name:tag><ImageName>

ex: sudo docker commit 8dbd9e392a96 my_img:webserve
```
obs: Don't create images with uppercase characters, docker doesn't allow it.

## Sharing the image (push)
```
sudo docker push <user/imageName>
ex: sudo docker push my_username/my_first_image
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
