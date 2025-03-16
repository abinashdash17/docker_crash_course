Docker

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

# port mapping
-p 80:5000
host 80, container 5000
# volume mounting
-v host_dir:container_dir
-v ~/nginx-config:/etc/nginx
## notes
1. individual files can also mounted

# more details
docker inspect cotainer_name
docker logs container_name

# notes

1. docker runs in an non-interactive mode. so if the app expects an input, the container will run without waiting for STDIN.
2. to avoid the above issue, use -i mode. but it's not attached to container's terminal
3. for that use -t to attach to an tty

# keywords
docker host/ docker engine

# reference
https://www.youtube.com/watch?v=fqMOX6JJhGo&t=1022s
