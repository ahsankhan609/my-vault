### introduction
[Playlist - Youtube](https://www.youtube.com/playlist?list=PLMbK063QE0JYpb2oFfj7KT868kp5QKSqr)

![Pasted image 20260603145956.png](../../Attachments/Pasted%20image%2020260603145956.png)

![Pasted image 20260603150111.png](../../Attachments/Pasted%20image%2020260603150111.png)

it helps us to make a single package including all software components, packages, configurations and tools for development and deployment on server.

![Pasted image 20260603150245.png](../../Attachments/Pasted%20image%2020260603150245.png)

this package is then called container.

### why docker is important?
how docker make our work faster and easier?
1. imagine someone join our team without docker
2. he takes hours to setup his machine for the required environment. such as installing databases, software's, packages etc...

![Pasted image 20260603150923.png](../../Attachments/Pasted%20image%2020260603150923.png) ![Pasted image 20260603151034.png](../../Attachments/Pasted%20image%2020260603151034.png)

### mange containers like a pro
* choosing lightweight image
* how to pull image into local machine
* how to run it, and convert it into container
* how to run, manage and delete container
* how to debug container

![Pasted image 20260603151916.png](../../Attachments/Pasted%20image%2020260603151916.png)
![Pasted image 20260603151933.png](../../Attachments/Pasted%20image%2020260603151933.png)
![Pasted image 20260603150245.png](../../Attachments/Pasted%20image%2020260603150245.png)
![Pasted image 20260603152107.png](../../Attachments/Pasted%20image%2020260603152107.png)
so, where we get those images such as database, OS, webserver, MySQL instances. We will use GitHub like repository manger called [Docker Hub](https://hub.docker.com/). It is basically an app store for Docker images.

#### Checks whether docker client and server is running properly
```bash
docker version
```
#### Pull latest image from Docker Hub
```bash
docker pull nginx:latest
```
#### List all locally stored(downloaded) Images
```bash
docker images
```
#### Show list of all running or stopped containers
```bash
docker ps -a
```
#### Run locally downloaded image as container - different ways
it will run the **image inside a container**. we can see container name, id inside the docker desktop app.
```bash
docker run nginx:latet
```
to run container in the **detached mode**, where it do not show logs on the screen. it is recommended to run images in **detached mode**
```bash
docker run -d nginx:latest
```
every time we run an image, docker always create a new container with new identity, but if we don't want to do so
```bash
docker start id_of_the_stopped_container
```
if we run multiple containers, sometime there is a conflict of running on same ports. Because containers have there own server and ports. and host system communicate with containers through those ports. For example assign 8080 to one container and 801 to another container. So to map each container on different port we do this:
```bash
docker run -d -p 8080:80 nginx:latest
```
we can verify through opening in browser:
https://localhost:8080
run same container with the name, detached mode, and mapped port
```bash
docker run -d --name nginx-local -p 8080:80 <image-name-or-id>
```
then if we need to run 2nd time, do this:
```bash
docker start nginx-local
```
stop re-used container:
```bash
docker stop nginx-local
```
see logs of that named container:
```bash
docker logs -f nginx-local
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
stop Named container:
```bash
docker stop nginx-local
```

#### removing Container(s) or Image(s)
1. in docker desktop we can simply remove containers and images by pressing delete button in **Actions** menu.
2. First **Stop the container** from running
```bash
docker stop NAME
```
3. write container name to **remove** it forcefully, if it is running
```bash
docker rm -f NAME
```
It removes all containers 
```bash
docker container prune
```
4. After stopping and deleting the container, we remove them Image. for example if another containers are using this image, that might be running, so we use `-f` flag to forcefully remove the image.
```bash
docker rmi -f image-name
```
remove all un-used images after confirmation
```bash
docker image prune
```
### running shell inside container
```bash
docker run NAME
```

```bash
docker exec -it NAME /bin/sh
```
