# Docker

- why we need docker:
  - Compatibility/Dependency between programs and os
  - Long setup time
  - Diffrent Dev/Test/Prod enviroment
- what can it do:
  - Containerize applications
  - Run each services whit its own dependencies in seprate containers

* container: completely isolated envirement, have own Proccess, services, network and mounts

## Main Command

- `docker run nginx` -> Run container from image, if not have get (pull) from server

- `docker ps` -> list of running containers

- `docker ps -a` -> list of all containers

- `docker stop 6003` -> stop container with name or id

- `docker start 6003` -> start container

- `docker rm -v 6003` -> remove container [from ps list]

- `docker images` -> image list on your system

- `docker rmi nginx` -> remove image from system, before on remove all container of that

- `docker pull node` -> only get node image frim server

### Run Command

- `docker exec [container] [command]` -> run command on container

### attach/detach mode

- for default docker run in atach mode

- `docker run -d [container]` -> run container in detach mode (run in background)

- `docker attach [container id]` -> attach to detach container

### Tag

- `docker run [container]:[tag]` -> run the special version of image, for default run latest

### STDIN

- `docker run -i [container]` -> run in interactive mode, for standard input

- `docker run -it [container]` -> run in interactive mode and terminal

### Port Mapping

- `docker run -p 80:5000 [container1]` -> connect port 80 of docker hub to port 5000 of container

- `docker run -p 3306:3306 mysql` -> connect port 3306 of docker hub to same port of container

- `docker run -p 8306:3306 mysql` -> run another copy of mysql container in port 8306

### Volume mapping

- to save data outside of container

- `docker run -v /opt/datadir:/var/lib/mysql mysql` -> map '/opt/datadir' of system to '/var/lib/mysql' of container

### Inspect Container

- `docker inspect [container]` -> more information about container

- `docker history [container]` -> build history

### Container Log

- `docker logs [container]` -> see the logs

### Enviroment Variable

- `docker run -e APP_COLOR=blue [container]` -> set the env variable

- you can see the env variable in inspect container, config->env

## Create Image

- make docker file -> `Dockerfile`

- every line of docker file have to side instruction and arguments

```dockerfile
FROM Ubuntu

RUN apt-get update
RUN apt-get install python

RUN pip install flask
RUN pip install flask-mysql

COPY . /opt/source-code

ENTRYPOINT FLASK_APP=/opt/source-code/app.py flask run
```

- start from a base OS or another image

- install all dependency

- copy source code

- especify entrypoint

- `docker build Dockerfile -t mohsen1299/my-custom-app`

- `docker push mohsen1299/my-custom-app`

- docker save the build step and when it failed or run again, docker only build the changed layer

### CMD vs ENTRYPOINT

- `CMD` for run command, `CMD command param1` or `CMD ["command","param1"]`

```dockerfile
FROM Ubuntu

CMD sleep 5
```

- can use `docker run ubuntu-sleeper` for sleep for 5 sec

- can use `docker run ubuntu-sleeper sleep 10` for sleep for 10 sec

- `ENTRYPOINT` for invoke command automatically

```dockerfile
FROM Ubuntu

ENTRYPOINT ["sleep"]
```

- onlu use `docker run ubuntu-sleeper 10` for 10 sec sleep, but we have error if not send argument

```dockerfile
FROM Ubuntu

ENTRYPOINT ["sleep"]

CMD ["5"]
```

- default value is 5 and we can send argument to change it

- to change ENTRYPOINT in run time `docker run --entrypoint sleep2.0 ubuntu-sleeper 10` -> run sleep2.0 10

## Network

- networks

  - Bridge
    - `docker run ubuntu`
    - private, internal every container in docker host connect to it, ip is 172.17.x.x
  - none
    - `docker run ubuntu --network=none`
    - isolate and none atach to any network
  - host
    - `docker run ubuntu --network=host`
    - assosiate to host network directly and use host network

- can make own internal network in docker host with `docker network create --driver bridge --subnet 182.18.0.0/16 custome-isolate-network`

- `docker network ls` -> list all network

- find network information of container in inspect, NetworkSetting->Networks->bridge

- container can connect with their names

## Layer Architecture

- Image layer is Read only

- Container Layer can read/write, change happen here, and remove after

- Copy-on-write change fie only in container layer and happen after build

### Volums

- `docker volume create [volum_name]` to make volume folder in docker lib

- `docker volume ls` , `docker volume inspect [volum_name]`

- volume: `docker run -v [volum_name]:/var/lib/mysql mysql` mount the docker volume folder -> '/var/lib/docker/volumes/'

- bind: for other path for volume -> `docker run -v /data/mysql:/var/lib/mysql mysql`

- can use `mount` instead of `v` and data as json -> `docker run --mount type=bind,source=/data/mysql,target=/var/lib/mysql mysql`

- storage driver to enable layered architecture, choose base on OS
  - AUFS
  - ZFS
  - BTRFS
  - Devise Mapper
  - Overlay
  - Overlay2

## Docker Compose

- need to set up complex application, running multiple services, better to use docer compose, in `docker-compose.yml`

```yml
services:
  web:
    image: "mmumshad/simple-webapp"
  database:
    images: "mongodb"
  messaging:
    image: "redis:alphine"
  orchestration:
    image: "ansible"
```

- use `docker-compose up`

### Link

- connect container: `docker run -d --name=vote -p 5000:80 --link redis:redis voting-app`, in docker compose file:

```yml
services:
  vote:
    image: "voting-app"
    ports:
      - 5000:80
    links:
      - redis
```

- in docker compose file: `redis:redis` = `redis`

- can write build location instead of image name `image: voting-app` -> `build: ./vote`

### Docker Compose versions

- default version is 1 and save versions.

```yml
vote:
  image: "voting-app"
  ports:
    - 5000:80
  links:
    - redis
```

- save links for other version and you can remove that for next versions

- `depend` container run before the this container

```yml
version: 2
services:
  vote:
    image: "voting-app"
    ports:
      - 5000:80
    depens_on:
      - redis
```

- can seprate the network for containers

```yml
services:
  redis:
    image: redis
    networks:
      - back-end
  db:
    image: postgres:9.4
    networks:
      - back-end
  vote:
    images: voting-app
    networks:
      - front-app
      - back-end
  result:
    images: result
    networks:
      - front-app
      - back-end
networks:
  front-end:
  back-end:
```

## Docker Registry

- image name: [User Account]/[Image Repository]

- `image:nginx` -> `image: nginx/nginx`

- location -> assume in docker hub ->`image:nginx` -> `image: docker.io/nginx/nginx`

- google registry, a lote of kubernetes: `gcr.io/kubernetes-e2e-test-images/dnsutils`

### Private Registry

- cloud private registry like aws, azure, gcp

- need login `docker login private-registry.io`

- after that `docker run private-registry.io/apps/internal-app`

### Deploy Private Registry

- its application and make docker in docker

- `docker run -d -p 5000:5000 --name registry registry2`

- tag image: `docker image tag my-image localhost:500/my-image`

- push image from localhost: `docker push localhost:500/my-image`

- push image from network: `docker push 192.168.56.100:500/my-image`

## Docker Engine

- in linux need: `Docker CLI`, `REST API`, `Docker Deamon`

- `Docker CLI` can work with remote engine `docker -H=remote-docker-engine:2375` like as `docker -H=10.123.2.1:2375 run nginx`

### name space

- docker use namespase to isolate workspace like: Proccess ID, Unix Timesharing, Mount, Network, InterProccess

### cgroups

- docker cgroup to control using of cpu by containers

- `docker run --cpus=.5 ubuntu`

- `docker run --memory=100m ubuntu`

## on Windeows

- two option for using docker in windows: `Docker Toolbox` or `Docker Desktop`

  - can install virtual software like 'virtual machin' or 'virtual box', deploy linux vm on it like ubuntu or debian, install docker on it - `Docker Desktop`: Oracle Virtualbox, Docker Engine, Docker Machine, Docker Compose, Kitematic GUI

  - `Docker Desktop`: use Microsoft Hyper-v in windows10 - default use linux container but you can choose window container

- 2 kind of container for window: windows server or Hyper-V isolation

  - windows server: share one kernel

  - Hyper-V isolation: seprate kernel for each

- 2 kind of image: windows server core or Nano server

  - windows server core: bigger image than nano server

  - Nano server: headless deployment, little size image like alphin in linux

- support windows server 2016, Nano server, Windows10 Professional and Enterprise (only on Hyper-V isolation container)

- can use Virtualbox and Hyper-V at sametime in windows

- check install `docker info`

- switch betwin windows and linux containers -> right click on docker in system try -> switch to Linux containers

- windows -> run -> `Virtmgmt.msc`: see MobiLinuxVm

`docker run hello-world` -> run hello-world image

`docker run -p 80:80 nginx` -> run nginx on porr input:80 output:80

- for search 'docs' in images-> `docker search docs`

`docker run -it alpine sh`

- -it -> run in foreground and stop when not see
- alpine -> very light linux distro
- sh -> run sh shell

### share hard

right click -> setting -> shared drives

`docker run --rm -v c:/Users:/data alpine ls /data`

- --rm: remove container after work
- -v: volume mount
- c:/Users:/data -> mapped c:\user to /data in image
- in end see data files with ls

`docker run --rm -it -v c:/Users/vahid/iis.tar:/data alpine sh`

- iis.tar info in /data and use sh
- if we change something in shell, its only on image and do'nt change in windows

### convert with docker

- use ffmpeg image for conver

`docker run --rm --volume ${pwd}:/output jrottenberg/ffmpeg -i http://site.com/file.mp4 /output/file.gif`

- \${pwd} current path

### Mapepd static site

#### shared file system

`docker run --rm -it -p 8080:80 -v c:\users\mohsen\mysite:/usr/share/nginx/html nginx`

see site in [local host port 8080](http://localhost:8080)

#### copy file to container

`docker run -d -p 8080:80 --name nginx nginx`

- -d: run in background

`docker cp c:\users\vahid\mysite nginx:/usr/share/nginx/html`

- copy site to container

`docker exec -it nginx bash`

- for change with bash

`docker exec nginx ls /usr/share/nginx/html`

- see list of file

see site in [local host port 8080](http://localhost:8080)

#### custome image

`docker commit nginx mysite:nginx`

- make snapshot from running container

`docker run -d -p 8090:80 --name mysite mysite:nginx`

see in [local host port 8090](http://localhost:8090)

`docker exec mysite ls /usr/share/nginx/html`

### Docker File

[Dockerfile refrense](https://docs.docker.com/engine/reference/builder/)

```sh
docker run -d -p 8080:80 --name nginx nginx
docker cp c:\users\vahid\mysite nginx:/usr/share/nginx/html
docker commit nginx mysite:nginx
```

in Dockerfile next to mysite folder

```Dockerfile
FROM nginx
COPY mysite /usr/share/nginx/html
```

for run
`docker build -f Dockerfile -t mysite:nginx-df .`

### Share images in Docker Hub

- add tag to image

`docker tag mysite:nginx-df my_user_name/some_name:new_tag_name`

- login with `docker login` and push to server

`docker push my_user_name/some_name:new_tag_name`

### Sql server

`docker pull microsoft/mssql-server-windows-express` -> 7GB

- for run

`docker run -d -p 1433:1433 -e sa_password=<SA_PASSWORD> -e ACCEPT_EULA=Y microsoft/mssql-server-windows-express`

- -d: in background
- 1433: standard port for sql server
- -e: local setting

`docker logs id` -> see status of container if see `password validation failed` its for not enough good password

- see container port with `ipconfig` and can connect to it

### mySql

`docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql`

for run

`docker ps` -> find id
`docker exec -it id mysql --user=root --password=my-secret-pw`

## Refrence

- Free Code Camp: Docker Tutorial for Beginners - Run applications in containers

- for test the [docker lab](http://kodekloude.com/p/docker-labs)
