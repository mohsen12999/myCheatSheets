# Docker

## some command

`docker images` -> image list on your system

`docker ps` -> running container

`docker ps -a` -> all container

`docker pull node` -> get node image

`docker start 6003` -> start container

`docker stop 6003` -> stop container

`docker rm -v 6003` -> remove container

## on Windeows

* check install  `docker info`

* switch betwin windows and linux containers -> right click on docker in system try -> switch to Linux containers

* windows -> run -> `Virtmgmt.msc`: see MobiLinuxVm

`docker run hello-world` -> run hello-world image

`docker run -p 80:80 nginx` -> run nginx on porr input:80 output:80

* for search 'docs' in images-> `docker search docs`

`docker run -it alpine sh`

* -it -> run in foreground and stop when not see
* alpine -> very light linux distro
* sh -> run sh shell

### share hard

right click -> setting -> shared drives

`docker run --rm -v c:/Users:/data alpine ls /data`

* --rm: remove container after work
* -v: volume mount
* c:/Users:/data -> mapped c:\user to /data in image
* in end see data files with ls

`docker run --rm -it -v c:/Users/vahid/iis.tar:/data alpine sh`

* iis.tar info in /data and use sh
* if we change something in shell, its only on image and do'nt change in windows

### convert with docker

* use ffmpeg image for conver

`docker run --rm --volume ${pwd}:/output jrottenberg/ffmpeg -i http://site.com/file.mp4 /output/file.gif`

* ${pwd} current path

### Mapepd static site

#### shared file system

`docker run --rm -it -p 8080:80 -v c:\users\mohsen\mysite:/usr/share/nginx/html nginx`

see site in http://localhost:8080

#### copy file to container

`docker run -d -p 8080:80 --name nginx nginx`

* -d: run in background

`docker cp c:\users\vahid\mysite nginx:/usr/share/nginx/html`

* copy site to container

`docker exec -it nginx bash`

* for change with bash

`docker exec nginx ls /usr/share/nginx/html`

* see list of file

see site in http://localhost:8080

#### custome image

`docker commit nginx mysite:nginx`

* make snapshot from running container

`docker run -d -p 8090:80 --name mysite mysite:nginx`

see in http://localhost:8090

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

* add tag to image

`docker tag mysite:nginx-df my_user_name/some_name:new_tag_name`

* login with `docker login` and push to server

`docker push my_user_name/some_name:new_tag_name`

### Sql server

`docker pull microsoft/mssql-server-windows-express` -> 7GB

* for run

`docker run -d -p 1433:1433 -e sa_password=<SA_PASSWORD> -e ACCEPT_EULA=Y microsoft/mssql-server-windows-express`

* -d: in background
* 1433: standard port for sql server
* -e: local setting

`docker logs id` -> see status of container if see `password validation failed` its for not enough good password

* see container port with `ipconfig` and can connect to it

### mySql

`docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql`

for run

`docker ps` -> find id
`docker exec -it id mysql --user=root --password=my-secret-pw`
