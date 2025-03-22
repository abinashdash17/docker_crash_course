Docker
source : https://www.youtube.com/watch?v=fqMOX6JJhGo
redis vs memcached

# container

1. process
2. N/W
3. Mounts

uses lxc
docker is high level tool

OS
1. OS kernel
2. software above it

windows container can't be run on the linux kernel
docker is not meant for virtualize different OS
purpose is to run containerized application

# container vs VM
VM has its own OS. in GB . good isolation
container shares same OS . in MB . less isolation
use VM + docker

# image vs container
image - a template, a plan, create custom image with app + config as Dockerfile

# commumity vs enterprise edition
mac/windows - docker desktop
linux - docker

# docker commands
docker run
docker ps -a
docker stop container_id/docker_name
docker rm
docker images
docker rmi nginx
docker pull nginx

docker run - runs the container, exits immediately
container runs as long as the process is running. once the process exits, the container stops

docker run ubuntu sleep 5
docker exec -> run command in running container
docker run container -> attached mode
docker run -d container
docker attach -> attach to stdin/stdout
docker run redis:tag

# docker run
## notes
1. docker runs in an non-interactive mode. so if the app expects an input, the container will run without waiting for STDIN.
2. to avoid the above issue, use -i mode. but it's not attached to container's terminal
3. for that use -t to attach to an tty

## port mapping
-p 80:5000 \
host 80, container 5000 \
## volume mounting
-v host_dir:container_dir \
-v ~/nginx-config:/etc/nginx
### notes
1. individual files can also mounted

# more details
`docker inspect cotainer_name` \
`docker logs container_name`

# environment variable
docker run -e APP_COLOR=blue containter_name
to check - docker inspect

# how to create a new image
Dockerfile
docker build -t
FROM, RUN, COPY, ENTRYPOINT
docker history image_name

# CMD vs Entry point
CMD -> specifies command which runs when container starts
docker run ubuntu sleep 5

ENTRYPOINT ["sleep"]
docker run ubuntu-sleeper 10

CMD -> commands are replaced
ENTRYPOINT -> command line params get appended

How to provide default value

FROM Ubuntu
ENTRYPOINT ["sleep"]
CMD ["5"]

docker run --entrypoint custom_entrypoint_command

# docker networking
bridge(default), none , host
--network=none
## bridge
need to expose ports
172.17.0.2
## host
will be exposed to real world
will not be possible to run multiple web server on the same port
no network isolation
## none
no network at all

## custom network
docker network create --driver bridge --subnet 182.18.0.0/16 custom-isolated-network
docker network ls
docker inspect container_name

## embedded DNS in docker
docker maintains a internal DNS
use the container name 'blissful_dog'
internal DNS server - 127.0.0.11
docker uses network namespaces + virtual ethernet

# docker storage
/var/lib/docker
generated image layers are cached
image layers are read-only
when the cotainer is running, docker creates another "writable" layer.
the image layers are shared by multiple images
Copy-on-write - COW


## volume
docker volume create data_volume
-v data_volume:/var/lib/mysql -> volume mount
-v /data/volume:/var/lib/mysql -> bind mount
new command
--mount type=bind,source=/path/to/mount,target=/var/lib/mysql

## storage driver:
aufs,zfs,btrfs,device mapper, overlay,overlay2

# compose
single docker host

--link redis:redis
--link db:db

--link -> deprecated
docker compose up

build paramter supports building image on the fly
## example
vote:
    build: ./vote
    ports:
        - 5000:80
    links:
        - redis

note: ./vote can contain source code and a docker file to build the image.

## versions

### v1

### v2
services:
    redis:
versions 2 uses a new network by default.
so no need to create links
depends_on : image name

### v3
supports docker swarm

## docker compose network
need to use at least v2
root level entry "networks"


### example
services:
    redis:
        image: redis
        networks:
            - front-end
            - back-end

networks:
    front-end:
    back-end:

# registry
user_account/user_account
nginx means nginx/nginx
default registry:docker.io
image: docker.io/nginx/nginx

## private registry
docker login private-registry.io


# Docker Engine
3 components
Docker CLI, REST API, Docker Deamon

Docker CLI <-> REST API <-> Docker Daemon

Docker -H=ip_addr:2375

restrict resource usage
--cpu=0.5 --memory=100m

# windows container
window server core
nano server

## support 
windows server 2016, nano server, enterprise edition

# docker orchestration
why? manage multiple container
Docker Swarm, kubernetes, Mesos

# docker swarm
Swarm Manger and  Workers

## command
docker service crate --replicas=3 my-web-server

# Kubernetes
kubectl 
rolling-update, rollback
Nodes
Cluster - set of nodes
Master - Kubernetes main node




# keywords
docker host/ docker engine
layered architecture
copy-on-write - COW
no mac container for now


# reference
https://www.youtube.com/watch?v=fqMOX6JJhGo&t=1022s
access docker container without port mapping
https://se7entyse7en.dev/posts/accessing-an-unpublished-port-of-a-running-docker-container/

# Question
redis?

