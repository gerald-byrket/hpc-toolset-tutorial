## Docker Tips

Some things you might find useful while using this setup:

### Docker Documentation

https://docs.docker.com

### Install & Start Docker

https://docs.docker.com/engine/install/

**NOTE: You'll need to make sure the account you're running docker with is in the 'docker' group**

### Install Docker Compose  

https://docs.docker.com/compose/install/

### Verify working Docker

```
docker info
```

**This should display your system info along with Docker-specific info.  If there are any errors, stop/start Docker**

### Error when starting up tutorial containers

If you get this error when starting the tutorial   

```
ERROR: Couldn't connect to Docker daemon at http+docker://localunixsocket - is it running?

or  

ERROR: Couldn't connect to Docker daemon at http+docker://localhost - is it running?
```

Try stopping and starting Docker (restart doesn't usually fix the problem).  Commands for this differ depending on operating system.

If the error persists, try:

```
export DOCKER_HOST=127.0.0.1
```

NOTE: this is only necessary on some systems so don't use it if the previous command works

**Sometimes restarting your operating system is the only solution.**

### Windows Errors  

NOTE: Windows users should get several pop-up messages from Docker Desktop during this process asking to allow local system access to the Docker containers.  Please click the "Share it" button:
![](windows_sharing.PNG)

If you have notifications blocked, you may not see these pop-ups and the authorization will eventually time out.  If this happens, you will get this type of error message:    

```
Error response from daemon: user declined directory sharing C:\Users\path_to_my_folder
```
Open Docker Desktop, navigate to Settings - Resources, and click on File Sharing.  Then add the directory where you've cloned the HPC Toolset Tutorial and click "Apply & Restart"

Re-run:  
```
./hpcts start  
```

If this doesn't work, please run:  
```
./hpcts cleanup  
./hpcts start  
```


### Docker Troubleshooting

Linux: https://docs.docker.com/engine/install/linux-postinstall/  
MacOS - Docker Desktop: https://docs.docker.com/docker-for-mac/troubleshoot/  
Windows - Docker Desktop:  https://docs.docker.com/docker-for-windows/troubleshoot/  

### Display Docker processes

```
docker ps -a
```

### Display Tutorial Container Logs

```
docker-compose logs -f
```

### Display Docker containers

```
docker container list
```

### Display Docker images

```
docker image list
```

### Display Docker volumes

```
docker volume list
```

### Shutting down the tutorial containers

**NOTE: This is the preferred method to stop/start or tear down the tutorial setup as the containers rely on each other and stopping, starting or deleting them individually usually has unintended side effects**

To tear down all containers and remove the volumes:   

```
./hpcts stop
```

To tear down all containers, remove volumes, and remove the container images (next time you run start they will be re-downloaded):  

```
./hpcts cleanup
```

### Starting everything up again

```
./hpcts start
```

### Deleting Docker containers/images/volumes manually

If you really want to clean up images and start fresh:  

```
docker image list
docker image rm XX (XX=image id)  
docker container list  
docker container rm XX (XX=container id)  
docker volume list  
docker volume rm XX (XX=volume id)
```

If you're getting an error about volumes in use but there is nothing running, stop docker, manually delete the files, and start docker again.  These commands are different depending on the operating system so we recommend using your favorite search provider to locate instructions for this.


### Finding IP address of container

```
$ docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' coldfront
172.27.0.10
```
[Back to Start](../README.md)
