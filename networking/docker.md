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

- Services
```
  sudo service docker start
  sudo service docker status
  sudo service docker stop
```
- Enter inside a container
```
  docker exec -it <containerName> bash 
```

- Search images  
```
  docker search <name>
```

- Show running containers
```
  docker ps
```
- Show all containers: -a  

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

Parameters for command **#run**
```
  -d Execução do container em background
  -i Modo interativo. Mantém o STDIN aberto mesmo sem console anexado
  -t Aloca uma pseudo TTY (TeleTypewriter)
  -rm Automaticamente remove o container após finalização
  --name Nomear o container
  -v Mapeamento de volume
  -p Mapeamento de porta
  -m Limite de uso de memória
```
