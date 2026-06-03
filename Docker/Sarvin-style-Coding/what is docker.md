### introduction

![[Pasted image 20260603145956.png]]
[Playlist - Youtube](https://www.youtube.com/playlist?list=PLMbK063QE0JYpb2oFfj7KT868kp5QKSqr)
![[Pasted image 20260603150111.png]]
it helps us to make a single package including all software components, packages, configurations and tools for development and deployment on server.
![[Pasted image 20260603150245.png]]
this package is then called container.

### why docker is important?
how docker make our work faster and easier?
1. imagine someone join our team without docker
2. he takes hours to setup his machine for the required environment. such as installing databases, software's, packages etc...

![[Pasted image 20260603150923.png]] ![[Pasted image 20260603151034.png]]

### mange containers like a pro
* choosing lightweight image
* how to pull image into local machine
* how to run it, and convert it into container
* how to run, manage and delete container
* how to debug container

![[Pasted image 20260603151916.png]]
![[Pasted image 20260603151933.png]]
![[Pasted image 20260603150245.png]]
![[Pasted image 20260603152107.png]]
so, where we get those images such as database, OS, webserver, MySQL instances. We will use GitHub like repository manger called [Docker Hub](https://hub.docker.com/). It is basically an app store for Docker images.

#### Checks whether docker client and server is running properly
```bash
docker version
```
#### Pull latest image from Docker Hub
```bash
docker pull nginx:latest
```
#### List all locally stored Images
```bash
docker images
```
#### Run locally downloaded image as container
it will run the **image inside a container**. we can see container name, id inside the docker desktop app.
```bash
docker run nginx;latet
```
to run container in the **detached mode**, where it do not show logs on the screen. it is recommended to run images in **detached mode**
```bash
docker run -d nginx:latest
```
every time we run an images, docker always create a new container with new identity, but if don't want to do so
```bash
docker start id_of_the_stopped_container
```
#### Show list of all running  or stopped containers
```bash
docker ps -a
```
#### Stop container from running - Docker Desktop - Terminal - detached
1. we can open docker desktop app
2. Click container in the left side
3. press **Stop** on the right side of container in the **Actions** 
```bash
ctrl+c
```
4. if container is running in detached mode, then to stop it, do this:
```bash
docker stop id_of_the_container
```
