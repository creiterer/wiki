<!-- TITLE: Docker -->
<!-- SUBTITLE: Tips & Tricks for Docker -->

# Docker Commands
## List Images
`docker images`

## List Containers
* running containers: `docker ps`
* all containers: `docker ps -a`

## Execute Command on Running Container
`docker exec -it <container name> <command>`

For instance, to get a terminal (bash) of a running container use:
`docker exec -it <container name> /bin/bash`

## Build Docker Image
`docker build -t <tag> --build-arg <argName=argValue> .`

## Kill Running Containers
* single container: `docker kill <container>`
* all containers: `docker kill $(docker ps -q)`

## Delete All Stopped Containers
`docker rm $(docker ps -a -q)`

## Delete Image
`docker rmi <image>`

## Copy Files to/from Running Docker Containers
* general: `docker cp <source> <dest>`
* from host to container: `docker cp foo.txt mycontainer:/foo.txt`
* from container to host: `docker cp mycontainer:/foo.txt foo.txt`