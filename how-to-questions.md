> Q. How to install docker?
<details><summary>Ans.</summary>
<p>
  <a href="https://docs.aws.amazon.com/AmazonECS/latest/developerguide/docker-basics.html">AWS Doc</a>

```
###########################################
# AWS EC2
###########################################
# Uninstall any older version of dockers:

$ sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
$ sudo yum update -y
$ sudo amazon-linux-extras install docker
$ sudo service docker start
$ sudo usermod -a -G docker ec2-user
$ docker info

###########################################
# Ubuntu 20.4
###########################################
$ sudo apt update -y
$ sudo apt install apt-transport-https \
                   ca-certificates \
                   curl \
                   gnupg-agent \
                   software-properties-common
# Add the gpg key
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
# Verify the key
$ sudo apt-key fingerprint 0EBFCD88
# add the docker repository
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
# update
$ sudo apt-get update
# Install the three docker packages
$ sudo apt install docker-ce docker-ce-cli containerd.io
# Add ubuntu user to docker group to be able to run docker
$ sudo usermod ubuntu -aG docker
```
</p>
</details>
--------

> Q. How to run a docker image?
<details><summary>Ans.</summary>
<p>  

```
$ docker run <image-name>
  
#Steps involved to run a docker image:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "image-name" image from the Docker Hub, if not present in local.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable.
 4. The Docker daemon streams any outputs to the Docker client, which can be seen on terminal.
```
</p>
</details>
--------

> Q. How to see running docker containers?
<details><summary>Ans.</summary>
<p>  
  
```
#https://docs.docker.com/engine/reference/commandline/container_ls/
$ docker container ls
OR
$ docker ps
```
</p>
</details>
--------

> Q. How to see both running and stopped docker containers?
<details><summary>Ans.</summary>
<p>  
  
```
#https://docs.docker.com/engine/reference/commandline/container_ls/
$ docker container ls -a
OR
$ docker ps -a
```
</p>
</details>
--------

> Q. How to run a docker container with interactive shell?
<details><summary>Ans.</summary>
<p>  
  
```
#without a terminal or tty
$ docker run -i alpine

#with a terminal or tty
$ docker run -it alpine
```
</p>
</details>
--------

> Q. How to run a persistent docker container
that doesnt exit immediately after "docker run" command completes?
<details><summary>Ans.</summary>
<p>  
  
```
#By using a daemon/detached flag
$ docker run -dt alpine

#This will generate a hash which can be used to track the cotainer
#CONTAINER ID   IMAGE         COMMAND     CREATED          STATUS                      PORTS     NAMES
#ac932f7e2efb   alpine        "/bin/sh"   6 minutes ago    Up 6 minutes                          lucid_greider
```
</p>
</details>
--------

> Q. How to provide user specific name to a  docker container?
<details><summary>Ans.</summary>
<p>  
  
```
#By using --name flag
$ docker run -dt --name myContainer alpine

#This will generate a hash which can be used to track the cotainer
#CONTAINER ID   IMAGE         COMMAND     CREATED          STATUS                      PORTS     NAMES
#83c822b310b2   alpine        "/bin/sh"   3 seconds ago    Up 3 seconds                          myContainer
```
</p>
</details>
--------

> Q. How to ensure docker container restarts in case
host reboots?
<details><summary>Ans.</summary>
<p>  
  
```
#By using a --restart flag
$ docker run -dt --name myContainer alpine --restart always
$ docker run -dt --name myContainer alpine --restart unless-stopped
$ docker run -dt --name myContainer alpine --restart on-failure

#default value is no
$ docker run -dt --name myContainer alpine --restart no
```
</p>
</details>
--------

> Q. How to ensure docker container is automatically removed
from list of containers once it stops?
<details><summary>Ans.</summary>
<p>  
  
```
#By using a --rm flag
$ docker run -it --name myContainer --rm alpine
```
</p>
</details>
--------

> Q. How to start a stopped container? How to restart a container?
<details><summary>Ans.</summary>
<p>  
  
```
$ docker start <stoppedContainerName>
$ docker restart <stoppedContainerName>
```
</p>
</details>
--------

> Q. How to get an interactive tty shell if a container is already started?
<details><summary>Ans.</summary>
<p>  
  
```
#Ubuntu
$ docker exec -it <startedContainerName> bash

#Alpine
$ docker exec -it <startedContainerName> ash
```

</p>
</details>
--------

> Q. How to execute a command on an already running container?
<details><summary>Ans.</summary>
<p>  
  
```
$ docker exec <runningContainerName> <command>
$ docker exec myContainer ls -larth
```
</p>
</details>
--------

> Q. How to copy a file from container to local and vice versa?
<details><summary>Ans.</summary>
<p>  
  
```
#Docker Container To Local
$ docker cp <startedContainerName>:<filePathOnContaner> <localPathOnSystem>
#
$ docker cp myContainer:/etc/nginx/conf.d/default.conf /tmp/


#Local to Docker Container
$ docker cp <localPathOnSystem> <startedContainerName>:<filePathOnContaner>
#
$ docker cp /tmp/default.conf myContainer:/etc/nginx/conf.d/default.conf 
```

</p>
</details>
--------

> Q. How to remove stopped container?
<details><summary>Ans.</summary>
<p>  
  
```
#Remove a single stopped docker container
$ docker rm <containerName>

#Remove all stopped containers
$ docker container prune 

```

</p>
</details>
--------

> Q. How to rename a running container?
<details><summary>Ans.</summary>
<p>  
  
```
$ docker rename <oldContainerName> <newContainerName>

$ docker rename myContainer nginxContainer

```

</p>
</details>
--------

> Q. How to check container performance like cpu, memory etc.?
<details><summary>Ans.</summary>
<p>  
  
```
#To see stats of all containers
$ docker stats

$To see stats of a given container
$ docker stats containerName
```

</p>
</details>
--------

> Q. How to find the IP address of a docker container?
<details><summary>Ans.</summary>
<p>  
  
```
#using docker inspect
$ docker inspect <containerName> | grep IP
```

</p>
</details>
--------

> Q. How to run a docker container on port 5555 on host mapped to 55 on container?
<details><summary>Ans.</summary>
<p>  
  
```
#using -p flag
$ docker run -p 5555:55 --name <containerName> -dt <imageName>

#If the container is already running then the image needs to be copied first and then relaunched
# Lets say nginx was already running on one container myContainer
#you can launch myContainer02 with above config

$ docker commit myContainer baseNginxImage
$ docker run -p 5555:55 --name myContainer02 -dt baseNginxImage

#Additionally run the actual nginx process as a foreground process
$ docker exec -dt myContainer02 nginx -g 'pid /tmp/nginx.pid; daemon off;'
#Additionally copy a sample file to run from nginx
$ docker cp <localIndex.html> <container>:<pathToNginxIndex.html>

#Curl at this point on local host or docker container should return same response
curl localhost:5555
curl $(docker inspect <containerName> | grep  \"IPAddress\"| head -1| awk -F":" '{print $2}'| sed "s/[\",]//g"):55
```

</p>
</details>
--------
